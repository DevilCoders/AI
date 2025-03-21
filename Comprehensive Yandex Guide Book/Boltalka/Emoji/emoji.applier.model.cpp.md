```cpp
#include "model.h"  
// Include the header file `model.h`, which likely contains the definition of the `TEmojiClassifierModel` class or related functionality.
// This is necessary for the `TEmojiClassifier` class to use the model for predictions.

#include <alice/nlu/libs/tf_nn_model/tensor_helpers.h>  
// Include the header file for tensor helpers from the Alice NLU library.
// This likely provides utility functions for working with tensors, which are used in neural network models.

#include <library/cpp/json/json_reader.h>  
// Include the JSON reader library to parse JSON data.
// This is used to load and parse configuration files, such as the emoji configuration.
```

```cpp
namespace NNlg {  
// Define a namespace `NNlg` to encapsulate the code and avoid naming conflicts.

namespace {  
// Start an anonymous namespace to limit the scope of the following code to this file.

TEmojiClassifierModel::TConfig LoadConfig(IInputStream* jsonConfigStream) {  
    // Define a function `LoadConfig` that takes a pointer to an input stream (`jsonConfigStream`) and returns a `TConfig` object.
    // This function is responsible for loading and parsing a JSON configuration file.

    Y_ENSURE(jsonConfigStream);  
    // Ensure that the `jsonConfigStream` pointer is not null. If it is null, the program will terminate with an error.

    NJson::TJsonValue jsonConfig;  
    // Create an object `jsonConfig` of type `TJsonValue` to store the parsed JSON data.

    const bool readCorrectly = NJson::ReadJsonTree(jsonConfigStream, &jsonConfig);  
    // Attempt to parse the JSON data from `jsonConfigStream` into `jsonConfig`.
    // `ReadJsonTree` returns `true` if parsing is successful, otherwise `false`.

    Y_ENSURE(readCorrectly);  
    // Ensure that the JSON parsing was successful. If not, the program will terminate with an error.

    TEmojiClassifierModel::TConfig config;  
    // Create an object `config` of type `TConfig` to store the configuration parameters.

    config.InputNode = jsonConfig["input_node"].GetStringSafe();  
    // Extract the value of the `input_node` field from the JSON and store it in `config.InputNode`.
    // `GetStringSafe()` ensures the field is treated as a string.

    config.OutputNode = jsonConfig["output_node"].GetStringSafe();  
    // Extract the value of the `output_node` field from the JSON and store it in `config.OutputNode`.

    config.EmbeddingSize = jsonConfig["embedding_size"].GetUIntegerSafe();  
    // Extract the value of the `embedding_size` field from the JSON and store it in `config.EmbeddingSize`.
    // `GetUIntegerSafe()` ensures the field is treated as an unsigned integer.

    return config;  
    // Return the `config` object containing the parsed configuration.
}

} // namespace  
// End of the anonymous namespace.


TEmojiClassifierModel::TEmojiClassifierModel(IInputStream* model, IInputStream* jsonConfigStream)  
    // Define the constructor for the `TEmojiClassifierModel` class.
    // It takes two parameters:
    // 1. `model`: A pointer to an input stream containing the model data.
    // 2. `jsonConfigStream`: A pointer to an input stream containing the model configuration.

    : TTfNnModel(model)  
    // Initialize the base class `TTfNnModel` with the `model` stream.
    // This assumes `TTfNnModel` is a base class that handles TensorFlow model loading.

    , Config(LoadConfig(jsonConfigStream))  
    // Initialize the `Config` member variable by calling the `LoadConfig` function.
    // `LoadConfig` parses the `jsonConfigStream` and returns a `TConfig` object.

{
    SetInputNodes({Config.InputNode});  
    // Set the input nodes of the TensorFlow model using the `InputNode` value from `Config`.

    SetOutputNodes({Config.OutputNode});  
    // Set the output nodes of the TensorFlow model using the `OutputNode` value from `Config`.

    EstablishSessionIfNotYet();  
    // Establish a TensorFlow session if it hasn't been established yet.
    // This prepares the model for making predictions.
}


TVector<float> TEmojiClassifierModel::Predict(const TVector<float>& queryEmbedding, const TVector<float>& replyEmbedding) const {  
    // Define the `Predict` method of the `TEmojiClassifierModel` class.
    // It takes two parameters:
    // 1. `queryEmbedding`: A vector of floats representing the embedding of the query.
    // 2. `replyEmbedding`: A vector of floats representing the embedding of the reply.
    // The method returns a vector of floats representing the prediction scores.

    Y_ENSURE(queryEmbedding.size() == Config.EmbeddingSize);  
    // Ensure that the size of the `queryEmbedding` vector matches the `EmbeddingSize` specified in the configuration.
    // If not, the program will terminate with an error.

    Y_ENSURE(replyEmbedding.size() == Config.EmbeddingSize);  
    // Ensure that the size of the `replyEmbedding` vector matches the `EmbeddingSize` specified in the configuration.
    // If not, the program will terminate with an error.

    NNeuralNet::TTensorList inputs = {tf::Tensor(tf::DT_FLOAT, {1ll, static_cast<long long>(Config.EmbeddingSize * 2)})};  
    // Create a list of input tensors (`inputs`) for the TensorFlow model.
    // The tensor is of type `float` and has a shape of `[1, EmbeddingSize * 2]`.
    // This tensor will store both the `queryEmbedding` and `replyEmbedding`.

    auto&& input = inputs[0].matrix<float>();  
    // Get a reference to the matrix representation of the first tensor in `inputs`.

    for (size_t i = 0; i < Config.EmbeddingSize; ++i) {  
        // Iterate over the elements of the embeddings.

        input(0, i) = queryEmbedding[i];  
        // Copy the `i`-th element of `queryEmbedding` into the first half of the input tensor.

        input(0, i + Config.EmbeddingSize) = replyEmbedding[i];  
        // Copy the `i`-th element of `replyEmbedding` into the second half of the input tensor.
    }

    const auto result = CreateWorker()->Process(inputs);  
    // Pass the input tensors to the TensorFlow model for processing.
    // `CreateWorker()` creates a worker to handle the TensorFlow session, and `Process()` runs the model.

    return NVins::ConvertTensorTo2DimTable<float>(result[0])[0];  
    // Convert the output tensor into a 2D table of floats and return the first row.
    // This represents the prediction scores for each emoji.
}


size_t TEmojiClassifierModel::GetEmbeddingSize() const {  
    // Define the `GetEmbeddingSize` method of the `TEmojiClassifierModel` class.
    // It returns the size of the embeddings used by the model.

    return Config.EmbeddingSize;  
    // Return the `EmbeddingSize` value from the `Config` object.
}

} // namespace NNlg  
// End of the `NNlg` namespace.
```
