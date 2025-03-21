```cpp
#include <alice/boltalka/generative/service/server/handlers/bert_factor_request_handler.h>  // Include the BERT factor request handler for the generative service
#include <mapreduce/yt/interface/client.h>  // Include the YT (Yandex Table) client interface for interacting with YT
#include <library/cpp/getopt/last_getopt.h>  // Include the last_getopt library for parsing command-line arguments
#include <util/string/cast.h>  // Include utilities for string casting and conversion
#include <dict/mt/libs/nn/ynmt/extra/encoder_head.h>  // Include the encoder head for YNMT (Yandex Neural Machine Translation)
```

```cpp
using namespace NYT;  // Use the NYT namespace to simplify access to Yandex Table (YT) classes and functions
using namespace NGenerativeBoltalka;  // Use the NGenerativeBoltalka namespace for generative Boltalka functionality
using NDict::NMT::NYNMT::TRegressionHead;  // Use the TRegressionHead class from the YNMT namespace for regression tasks

// Function to safely convert a YT node to a string
TString SafeAsString(const NYT::TNode& node) {
    return node.IsString() ? node.AsString() : "";  // Return the node's string value if it is a string, otherwise return an empty string
}

// Define a struct to hold a row of data and its associated future result
struct TRow {
    TNode Row;  // The row data as a YT node
    NThreading::TFuture<TBertRequestHandler<TRegressionHead>::TResult> Future;  // A future representing the result of processing the row
};

// Define a type alias for a YT table writer that writes YT nodes
using TWriter = TIntrusivePtr<NYT::TTableWriter<NYT::TNode>>;  // A smart pointer to a YT table writer for YT nodes
```

```cpp
// Function to consume and process results from a vector of rows
void ConsumeResults(TVector<TRow>& rows,  // A vector of rows containing data and their associated futures
                    TWriter writer) {  // A YT table writer to write the processed results
    for (auto& el : rows) {  // Iterate over each row in the vector
        // Retrieve the result from the future and store it in the row as "bert_score"
        el.Row["bert_score"] = static_cast<double>(el.Future.GetValueSync()[0]);
        // Add the updated row to the YT table writer
        writer->AddRow(el.Row);
    }
    rows.clear();  // Clear the vector of rows after processing
}
```

```cpp
int main(int argc, char* argv[]) {  // Main function, entry point of the program
    size_t maxBatchSize;  // Variable to store the maximum batch size for processing
    size_t maxInputLength;  // Variable to store the maximum input length for processing
    size_t contextLen;  // Variable to store the context length for processing
    bool truncateAsDialogue;  // Flag to indicate whether to truncate input as dialogue
    TString folder;  // Variable to store the path to the model folder
    TString inputTable;  // Variable to store the path to the input table
    TString outputTable;  // Variable to store the path to the output table

    auto opts = NLastGetopt::TOpts::Default();  // Create a default options parser object
    opts.AddLongOption("input")  // Add an option for the input table
        .StoreResult(&inputTable)  // Store the result in the `inputTable` variable
        .Required()  // Mark this option as required
        .Help("Input table");  // Provide help text for this option
    opts.AddLongOption("output")  // Add an option for the output table
        .StoreResult(&outputTable)  // Store the result in the `outputTable` variable
        .Required()  // Mark this option as required
        .Help("Output table");  // Provide help text for this option
    opts.AddLongOption("folder")  // Add an option for the model folder
        .StoreResult(&folder)  // Store the result in the `folder` variable
        .Required()  // Mark this option as required
        .Help("Model folder");  // Provide help text for this option
    opts.AddLongOption("batchsize")  // Add an option for the maximum batch size
        .StoreResult(&maxBatchSize)  // Store the result in the `maxBatchSize` variable
        .DefaultValue(256);  // Set a default value of 256 if this option is not provided
    opts.AddLongOption("maxinputlength")  // Add an option for the maximum input length
        .StoreResult(&maxInputLength)  // Store the result in the `maxInputLength` variable
        .DefaultValue(127);  // Set a default value of 127 if this option is not provided
    opts.AddLongOption("contextlen")  // Add an option for the context length
        .StoreResult(&contextLen)  // Store the result in the `contextLen` variable
        .DefaultValue(3);  // Set a default value of 3 if this option is not provided
    opts.AddLongOption("truncateasdialogue")  // Add an option to truncate input as dialogue
        .StoreResult(&truncateAsDialogue)  // Store the result in the `truncateAsDialogue` variable
        .DefaultValue(false);  // Set a default value of false if this option is not provided

    NLastGetopt::TOptsParseResult res(&opts, argc, argv);  // Parse the command-line arguments using the defined options

    // Define a constant structure for BERT output parameters with default values for MSE (Mean Squared Error)
const TBertOutputParams defaultMseParams = {
        1.0,  // Scale: Multiplies the model's output by this value
        0.0,  // Bias: Adds this value to the model's output
        false,  // IsTargetCe: Indicates whether the target is cross-entropy (false for MSE)
        false,  // DoBinarization: Indicates whether to binarize the output (false for no binarization)
        0.0  // BinarizeThreshold: Threshold for binarization (not used when DoBinarization is false)
    };
```

```cpp
// TODO: Support optional head (a placeholder for future functionality)
// Initialize the BERT request handler with the specified parameters
TBertRequestHandler<TRegressionHead> handler(
    folder,  // Path to the model folder
    maxBatchSize,  // Maximum batch size for processing
    maxInputLength,  // Maximum input length for BERT
    0,  // Number of extra tokens (not used here)
    contextLen,  // Context length for processing
    truncateAsDialogue,  // Flag to indicate whether to truncate input as dialogue
    {{0, defaultMseParams}}  // Output parameters for the regression head (using default MSE parameters)
);

NYT::Initialize(argc, argv);  // Initialize the YT (Yandex Table) client with command-line arguments

auto client = CreateClient("hahn");  // Create a YT client for the "hahn" cluster
auto reader = client->CreateTableReader<TNode>(inputTable);  // Create a reader for the input table
auto writer = client->CreateTableWriter<TNode>(outputTable);  // Create a writer for the output table

TVector<TRow> rows;  // Vector to store rows of data and their associated futures

for (auto& cursor : *reader) {  // Iterate over each row in the input table
    auto& row = cursor.GetRow();  // Get the current row as a YT node
    TVector<TString> sample;  // Vector to store the sample (context + reply)
    sample.reserve(contextLen + 1);  // Reserve space for the context and reply
    for (size_t i = 0; i < contextLen; ++i) {  // Iterate over the context length
        // Extract the context from the row and add it to the sample
        sample.emplace_back(SafeAsString(row["context_" + ToString(contextLen - i - 1)]));
    }
    sample.emplace_back(SafeAsString(row["reply"]));  // Extract the reply from the row and add it to the sample
    rows.push_back({row, handler.ProcessSample(sample)});  // Process the sample and store the row with its future result
    if (rows.size() >= maxBatchSize) {  // If the batch size is reached
        ConsumeResults(rows, writer);  // Process and write the results
    }
}
ConsumeResults(rows, writer);  // Process and write any remaining rows

writer->Finish();  // Finalize the output table writer

return 0;  // Exit the program with a success status
}
```
