```cpp
#pragma once  // Ensure the file is included only once during compilation

#include <util/string/split.h>  // Include utilities for splitting strings

#include <util/generic/algorithm.h>  // Include generic algorithms (e.g., sorting, searching)
#include <util/generic/array_ref.h>  // Include a lightweight reference to arrays
#include <util/generic/reserve.h>  // Include utilities for reserving memory in containers
#include <util/string/join.h>  // Include utilities for joining strings
#include <util/system/info.h>  // Include system information utilities (e.g., CPU count)

#include <library/cpp/float16/float16.h>  // Include support for 16-bit floating-point numbers
#include <library/cpp/getopt/last_getopt.h>  // Include the last_getopt library for command-line argument parsing

#include <dict/mt/libs/nn/ynmt_backend/gpu/backend.h>  // Include the GPU backend for YNMT
#include <dict/mt/libs/nn/ynmt_backend/cpu/backend.h>  // Include the CPU backend for YNMT

#include <dict/mt/libs/nn/ynmt/config_helper/model_reader.h>  // Include utilities for reading YNMT model configurations

#include <dict/mt/libs/nn/ynmt/extra/encoder_head.h>  // Include the encoder head for YNMT

#include <kernel/bert/bert_wrapper.h>  // Include the BERT wrapper for applying BERT models
#include <kernel/bert/tokenizer.h>  // Include the BERT tokenizer for text tokenization

#include <type_traits>  // Include utilities for type traits (e.g., type checking, type transformations)

using NBertApplier::TBertWrapper;  // Alias for the BERT wrapper class
using NDict::NMT::NYNMT::TRegressionHead;  // Alias for the regression head class
```

```cpp
// Function to tokenize a string using a BERT segmenter
TVector<TUtf32String> Tokenize(const TString& s, THolder<NBertApplier::TBertSegmenter>& segmenter) {
    // Convert the input string from UTF-8 to UTF-32 for tokenization
    TUtf32String w32Sentence = TUtf32String::FromUtf8(s);
    // Use the BERT segmenter to split the UTF-32 string into tokens
    return segmenter->Split(w32Sentence);
}

// Function to preprocess samples into token IDs for BERT input
TVector<TVector<int>> PreprocessSamples(
    const TVector<TString>& samples,  // Input samples as a vector of strings
    size_t maxInputLength,  // Maximum input length for BERT (excluding special tokens)
    const TString& startTrieFilename,  // Filename for the start trie (tokenization)
    const TString& contTrieFilename,  // Filename for the continuation trie (tokenization)
    const TString& vocabFilename) {  // Filename for the vocabulary (token-to-ID conversion)
    // Reserve space in the result vector to avoid reallocations
    TVector<TVector<int>> result(Reserve(samples.size()));

    // Initialize a BERT segmenter for tokenization
    THolder<NBertApplier::TBertSegmenter> segmenter(new NBertApplier::TBertSegmenter(startTrieFilename, contTrieFilename));
    // Initialize a BERT ID converter for converting tokens to IDs
    THolder<NBertApplier::TBertIdConverter> converter(new NBertApplier::TBertIdConverter(vocabFilename));

    // Iterate over each sample in the input
    for (auto& sample : samples) {
        // Tokenize the sample into UTF-32 strings
        TVector<TUtf32String> tokens = Tokenize(sample, segmenter);
        // Limit the number of tokens to `maxInputLength - 2` (to leave space for special tokens)
        size_t num_tokens = Min(tokens.size(), maxInputLength - 2);
        // Resize the tokens vector to the allowed length
        tokens.resize(num_tokens);
        // Convert tokens to token IDs using the BERT ID converter
        auto tokenIds = converter->Convert(tokens);
        // Add the token IDs to the result vector
        result.emplace_back(tokenIds.begin(), tokenIds.end());
    }
    // Return the preprocessed token IDs
    return result;
}

// Template function declaration (incomplete in the provided code)
template <typename TFloatType>
```

```cpp
// Define an abstract base class for BERT appliers
class IBertApplier {
public:
    // Pure virtual function to process a batch of tokenized inputs
    virtual TVector<TFloatType> ProcessBatch(const TConstArrayRef<TVector<int>>& batch) = 0;

    // Virtual destructor to ensure proper cleanup of derived classes
    virtual ~IBertApplier() = default;
};

// Function to create a backend (CPU or GPU) for BERT processing
NDict::NMT::NYNMT::TBackendPtr CreateBackend(bool useCpu,  // Flag to indicate whether to use CPU
                                              int deviceIndex,  // Index of the GPU device to use (if not using CPU)
                                              TMaybe<size_t> numThreads) {  // Optional number of threads for CPU backend
    if (useCpu) {  // If using CPU
        return NDict::NMT::NYNMT::CreateCpuBackend(numThreads);  // Create a CPU backend with the specified number of threads
    }
    // If using GPU, create a GPU backend with the specified device index
    return new NDict::NMT::NYNMT::TGpuBackend(deviceIndex);
}

// Template function declaration (incomplete in the provided code)
template <typename TFloatType>
```

```cpp
// Define a class for applying YNMT with BERT
class TYNMTApplier: public IBertApplier<TFloatType> {
public:
    // Constructor to initialize the YNMT applier
    TYNMTApplier(int maxBatchSize,  // Maximum batch size for processing
                 int maxInputLength,  // Maximum input length for BERT
                 const TString& modelPath,  // Path to the model file
                 NDict::NMT::NYNMT::TBackendPtr backend)  // Backend (CPU or GPU) for processing
        : MaxInputLength(maxInputLength)  // Initialize the maximum input length
        , ModelBlob(TBlob::FromFile(modelPath))  // Load the model from the specified file
        , Backend(backend)  // Initialize the backend
        , InitEnv(Backend.Backend.Get(), {}, false, false)  // Initialize the environment for the backend
        , Bert(maxBatchSize, maxInputLength, 0)  // Initialize the BERT wrapper
    {
        // Create a regression head for the model
        auto head = MakeHolder<TRegressionHead<TFloatType>>(
            maxBatchSize,  // Maximum batch size
            InitEnv,  // Initialization environment
            NDict::NMT::NYNMT::ReadModelProtoWithMeta(ModelBlob));  // Read the model protobuf
        // Initialize the BERT wrapper with the model and regression head
        Bert.Initialize(ModelBlob, InitEnv, Backend, std::move(head));
    }

    // Override the ProcessBatch function to process a batch of tokenized inputs
    TVector<TFloatType> ProcessBatch(const TConstArrayRef<TVector<int>>& batch) override {
        NBertApplier::TBertInput bertInput(batch.size(), MaxInputLength);  // Create a BERT input object
        for (const auto& sample : batch) {  // Iterate over each sample in the batch
            bertInput.Add(sample);  // Add the sample to the BERT input
        }
        return Bert.ProcessBatch(bertInput);  // Process the batch and return the results
    }

private:
    int MaxInputLength;  // Maximum input length for BERT
    TBlob ModelBlob;  // Blob containing the model data
    NDict::NMT::NYNMT::TBackendWithMemory Backend;  // Backend with memory management
    NDict::NMT::NYNMT::TInitializationEnvironment InitEnv;  // Initialization environment for the backend
    TBertWrapper<TFloatType, TRegressionHead> Bert;  // BERT wrapper for processing
};

// Template function to run BERT processing
template <typename TFloatType>
TVector<TFloatType> Run(const TVector<TVector<int>>& data,  // Input data as tokenized vectors
         const TVector<TString>& samples,  // Original samples (for reference)
         int maxBatchSize,  // Maximum batch size for processing
         int maxInputLength,  // Maximum input length for BERT
         const TString& weightsFilename,  // Path to the model weights file
         NDict::NMT::NYNMT::TBackendPtr backend) {  // Backend (CPU or GPU) for processing
    THolder<IBertApplier<TFloatType>> bertApplier;  // Create a holder for the BERT applier
    bertApplier.Reset(new TYNMTApplier<TFloatType>(maxBatchSize, maxInputLength, weightsFilename, backend));  // Initialize the applier

    typename TRegressionHead<TFloatType>::TResult allResults;  // Store all results from processing

    // Warmup the BERT applier with a small batch
    TConstArrayRef<TVector<int>> warmupBatch(data.begin(), data.begin() + Min<size_t>(data.size(), maxBatchSize));
    bertApplier->ProcessBatch(warmupBatch);

    // Process the data in batches
    for (auto i = 0U; i < (samples.size() - 1) / maxBatchSize + 1; ++i) {
        size_t start = i * maxBatchSize;  // Calculate the start index of the batch
        auto end = Min(start + maxBatchSize, data.size());  // Calculate the end index of the batch

        const int batchSize = end - start;  // Calculate the batch size
        Y_ENSURE(batchSize <= maxBatchSize, "Maximum batch size exceeded: " << batchSize << " > " << maxBatchSize);  // Ensure the batch size is valid

        TConstArrayRef<TVector<int>> batch(data.begin() + start, data.begin() + end);  // Create a batch from the data

        auto result = bertApplier->ProcessBatch(batch);  // Process the batch
        allResults.insert(allResults.end(), result.begin(), result.end());  // Append the results to the overall results
    }

    return allResults;  // Return all results
}

// Overloaded template function to run BERT processing with backend creation
template <typename TFloatType>
TVector<TFloatType> Run(const TVector<TVector<int>>& data,  // Input data as tokenized vectors
         const TVector<TString>& samples,  // Original samples (for reference)
         int maxBatchSize,  // Maximum batch size for processing
         int maxInputLength,  // Maximum input length for BERT
         TMaybe<size_t> numThreads,  // Optional number of threads for CPU backend
         const TString& weightsFilename,  // Path to the model weights file
         bool useCpu,  // Flag to indicate whether to use CPU
         int deviceIndex) {  // Index of the GPU device to use (if not using CPU)
    // Call the Run function with the created backend
    return Run<TFloatType>(data, samples, maxBatchSize, maxInputLength, weightsFilename, CreateBackend(useCpu, deviceIndex, numThreads));
}
```
