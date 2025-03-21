```cpp
#include <util/stream/file.h>  // Include the file stream utilities for file I/O operations
#include <util/string/strip.h>  // Include string utilities for stripping whitespace from strings
#include <alice/boltalka/bert/lib/main.h>  // Include the main library for BERT-related functionality
```
```cpp
// Function to read samples from a file and return them as a vector of strings
TVector<TString> ReadSamples(const TString& filename) {  // Define a function that takes a filename as input
    TIFStream file(filename);  // Create an input file stream to read from the specified file
    TVector<TString> result;  // Create a vector to store the resulting strings
    TString str;  // Declare a temporary string to hold each line read from the file
    while (file.ReadLine(str))  // Read each line from the file until the end of the file is reached
        result.push_back(StripString(str));  // Strip whitespace from the line and add it to the result vector
    return result;  // Return the vector of stripped strings
}

// Template function to run a process and report results
template <typename TFloatType>  // Define a template function that works with any floating-point type
void RunAndReport(const TVector<TVector<int>>& data,  // Input data as a vector of vectors of integers
         const TVector<TString>& samples,  // Vector of strings representing samples
         int maxBatchSize,  // Maximum batch size for processing
         int maxInputLength,  // Maximum input length for processing
         TMaybe<int> numThreads,  // Optional number of threads to use (may or may not be specified)
         const TString& weightsFilename,  // Filename for the weights file
         bool useCpu,  // Flag to indicate whether to use the CPU (true) or GPU (false)
         int deviceIndex) {  // Index of the device to use (e.g., GPU index)
    // Run the process with the provided parameters and store the results
    TVector<TFloatType> results = Run<TFloatType>(data, samples, maxBatchSize, maxInputLength, numThreads, weightsFilename, useCpu, deviceIndex);
    for (const auto& el : results) {  // Iterate over the results vector
        Cout << el << Endl;  // Print each result to the standard output followed by a newline
    }
}
```

```cpp
int main(int argc, char* argv[]) {  // Main function, entry point of the program
    size_t maxBatchSize;  // Variable to store the maximum batch size for processing
    size_t maxInputLength;  // Variable to store the maximum input length for processing
    TString samplesFilename;  // Variable to store the filename for input queries
    TString weightsFilename;  // Variable to store the filename for model weights
    TString startTrieFilename;  // Variable to store the filename for the start trie (tokenization)
    TString contTrieFilename;  // Variable to store the filename for the continuation trie (tokenization)
    TString vocabFilename;  // Variable to store the filename for the vocabulary
    bool useCPU = false;  // Flag to indicate whether to use the CPU (default is false, meaning GPU is used)
    bool useFp16 = false;  // Flag to indicate whether to use FP16 precision (default is false, meaning FP32 is used)
    int deviceIndex = 0;  // Variable to store the GPU device index (default is 0)
    TMaybe<int> numThreads;  // Optional variable to store the number of threads for CPU processing

    auto opts = NLastGetopt::TOpts::Default();  // Create a default options parser object
    opts.AddLongOption("input")  // Add an option for the input queries file
        .StoreResult(&samplesFilename)  // Store the result in the `samplesFilename` variable
        .Required()  // Mark this option as required
        .Help("file with the input queries");  // Provide help text for this option
    opts.AddLongOption("weights")  // Add an option for the model weights file
        .StoreResult(&weightsFilename)  // Store the result in the `weightsFilename` variable
        .Required()  // Mark this option as required
        .Help("path to a file with the model weights");  // Provide help text for this option
    opts.AddLongOption("starttrie")  // Add an option for the start trie file
        .StoreResult(&startTrieFilename)  // Store the result in the `startTrieFilename` variable
        .Required()  // Mark this option as required
        .Help("path to a file with a start trie for tokenization");  // Provide help text for this option
    opts.AddLongOption("conttrie")  // Add an option for the continuation trie file
        .StoreResult(&contTrieFilename)  // Store the result in the `contTrieFilename` variable
        .Required()  // Mark this option as required
        .Help("path to a file with a start trie for tokenization");  // Provide help text for this option
    opts.AddLongOption("vocab")  // Add an option for the vocabulary file
        .StoreResult(&vocabFilename)  // Store the result in the `vocabFilename` variable
        .Required()  // Mark this option as required
        .Help("path to a file with a vocabulary");  // Provide help text for this option
    opts.AddLongOption("cpu")  // Add an option to enable CPU usage
        .NoArgument()  // This option does not take an argument
        .StoreValue(&useCPU, true);  // Set `useCPU` to true if this option is provided
    opts.AddLongOption("fp16")  // Add an option to enable FP16 precision
        .NoArgument()  // This option does not take an argument
        .Help("load a model with FP16 weights (use dict/mt/make/tools/tfnn/convert_to_fp16 to convert an existing FP32 model)")  // Provide help text for this option
        .StoreValue(&useFp16, true);  // Set `useFp16` to true if this option is provided
    opts.AddLongOption("device")  // Add an option to specify the GPU device index
        .Help("when using GPU, selects the index of GPU to use")  // Provide help text for this option
        .StoreResult(&deviceIndex);  // Store the result in the `deviceIndex` variable
    opts.AddLongOption("threads")  // Add an option to specify the number of threads for CPU processing
        .Help("when using CPU, sets the thread count for OpenMP/MKL")  // Provide help text for this option
        .Handler1T<int>([&](int value) {  // Define a handler to store the thread count
            numThreads = value;  // Store the provided value in `numThreads`
        });
    opts.AddLongOption("batchsize")  // Add an option to specify the maximum batch size
        .StoreResult(&maxBatchSize)  // Store the result in the `maxBatchSize` variable
        .DefaultValue(32);  // Set a default value of 32 if this option is not provided
    opts.AddLongOption("maxinputlength")  // Add an option to specify the maximum input length
        .StoreResult(&maxInputLength)  // Store the result in the `maxInputLength` variable
        .DefaultValue(127);  // Set a default value of 127 if this option is not provided

    NLastGetopt::TOptsParseResult res(&opts, argc, argv);  // Parse the command-line arguments using the defined options

    auto samples = ReadSamples(samplesFilename);  // Read the input queries from the specified file
    if (samples.size() == 0)  // Check if no samples were read
        return 0;  // Exit the program if there are no samples to process

    auto data = PreprocessSamples(  // Preprocess the samples using the provided tokenization files
        samples,
        maxInputLength,
        startTrieFilename,
        contTrieFilename,
        vocabFilename);

    if (useFp16) {  // Check if FP16 precision is enabled
        RunAndReport<TFloat16>(data, samples, maxBatchSize, maxInputLength, numThreads, weightsFilename, useCPU, deviceIndex);  // Run the process with FP16 precision
    } else {  // If FP16 is not enabled
        RunAndReport<float>(data, samples, maxBatchSize, maxInputLength, numThreads, weightsFilename, useCPU, deviceIndex);  // Run the process with FP32 precision
    }

    return 0;  // Exit the program with a success status
}
```
