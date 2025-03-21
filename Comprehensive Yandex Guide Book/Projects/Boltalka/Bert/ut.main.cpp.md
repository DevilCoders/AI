```cpp
#include <library/cpp/testing/unittest/registar.h>  // Include the Yandex Unit Test framework
#include <dict/mt/libs/nn/ynmt/test_utils/test_backend.h>  // Include utilities for creating a test backend

#include <alice/boltalka/bert/lib/main.h>  // Include the main BERT library for preprocessing and running models

constexpr double PRECISION = 1e-3;  // Define a precision constant for floating-point comparisons

Y_UNIT_TEST_SUITE(TestBoltalkaBert) {  // Define a test suite for the Boltalka BERT functionality
    Y_UNIT_TEST(Test) {  // Define a unit test case
        // Define a set of sample inputs with BERT-style tokens
        TVector<TString> samples = {
            "[CLS] [SEP] [SEP] привет [SEP] привет [SEP]",  // Sample 1
            "[CLS] [SEP] привет [SEP] как дела [SEP] неплохо [SEP]",  // Sample 2
            "[CLS] [SEP] что такое дебют [SEP] и что такое идея [SEP] я не знаю [SEP]",  // Sample 3
            "[CLS] нет [SEP] ну ладно , как хотите [SEP] нет [SEP] а что ? [SEP]",  // Sample 4
            "[CLS] нет [SEP] ну ладно , как хотите [SEP] нет [SEP] как же нет , когда да [SEP]",  // Sample 5
            "[CLS] нет [SEP] ну ладно , как хотите [SEP] нет [SEP] яблоки вкусные [SEP]",  // Sample 6
        };

        // Preprocess the samples into tokenized data
        auto data = PreprocessSamples(
            samples,  // Input samples
            128,  // Maximum input length
            "start.trie",  // Path to the start trie file
            "cont.trie",  // Path to the continuation trie file
            "vocab.txt"  // Path to the vocabulary file
        );

        // Run the BERT model on the preprocessed data
        TVector<float> results = Run<float>(
            data,  // Preprocessed tokenized data
            samples,  // Original samples (for reference)
            32,  // Maximum batch size
            128,  // Maximum input length
            "boltalka-bert-mse.npz",  // Path to the model weights file
            NDict::NMT::NYNMT::NTesting::CreateTestBackend()  // Create a test backend for processing
        );

        // Assert that the results match the expected values with the defined precision
        UNIT_ASSERT_DOUBLES_EQUAL(1.81228, results[0], PRECISION);  // Check result for sample 1
        UNIT_ASSERT_DOUBLES_EQUAL(1.37753, results[1], PRECISION);  // Check result for sample 2
        UNIT_ASSERT_DOUBLES_EQUAL(1.05803, results[2], PRECISION);  // Check result for sample 3
        UNIT_ASSERT_DOUBLES_EQUAL(1.56769, results[3], PRECISION);  // Check result for sample 4
        UNIT_ASSERT_DOUBLES_EQUAL(1.96784, results[4], PRECISION);  // Check result for sample 5
        UNIT_ASSERT_DOUBLES_EQUAL(0.416829, results[5], PRECISION);  // Check result for sample 6
    }
}
```
