# BERT-Based Text Processing Pipeline

This project implements a BERT-based text processing pipeline for tasks such as tokenization, preprocessing, and inference. It integrates with Yandex Table (YT) for distributed data processing and supports both CPU and GPU backends.

# Project Structure
### 1. Build Configuration Files
- ```ya.make```: Defines build targets, dependencies, and conditional compilation flags.

## Key Directives
- ```PROGRAM()```: Defines an executable target
- ```SRCS()```: Lists source files to compile
- ```PEERDIR()```: Specifies dependencies (e.g., libraries or other modules)
- ```IF (USE_GPU)```: Conditionally adds GPU-specific compiler flags
- ```RECURSE()```: Recursively includes build configurations from subdirectories

## 2. Source Code
#### Header files
- ```main.h```: Declares functions, classes, and constants used in the project

#### Includes
- ```YT client```, ```BERT wrapper```, ```tokenizer```, and ```other``` utilities.

#### Aliases:
- Simplifies usage of complex types (e.g., ```TBertWrapper```, ```TRegressionHead```)

### Source Files
- ```main.cpp```: Implements the main logic for processing text data using BERT

#### Key Functions
- ```Tokenize```: Tokenizes input strings using a BERT segmenter
- ```PreprocessSamples```: Converts samples into tokenized data for BERT input
- ```Run```: Processes batches of data using the BERT model
- ```ConsumeResults```: Writes processed results to a YT table

#### Classes
- ```TYNMTApplier```: Implements the ```IBertApplier``` interface for applying ```YNMT``` with ```BERT```
- ```SessionFilter```: Filters and processes sessions of text data
- ```NegativesSampler```: Samples negative examples for training or evaluation

## 3. Unit Tests
- ```ut/cpu``` and ```ut/gpu```: Contains unit tests for CPU and GPU backends

#### Test Setup
- Defines ```sample inputs``` with ```BERT-style``` tokens
- ```Preprocesses samples``` and ```runs the BERT model```

#### Assertions
- Compares results against expected values with a defined precision (```PRECISION```)

#### Build Configuration
- Includes ```dependencies``` for ```CPU``` and ```GPU``` tests
- Specifies ```YT configurations``` for ```GPU``` tests

## 4. YT Configuration
- ```gpu_yt_spec.yson```: Defines settings for running tasks on Yandex Table

#### Key Settings
- Cluster: ```hahn```
- Pool: ```dialogs```
- GPU Limits: ```1 GPU``` per task
- Layers: ```GPU driver``` and ```Ubuntu base```

## 5. Helper Functions and Structs
- ```SafeAsString```: Safely converts a YT node to a string
- ```TRow```: Combines a row of data with its processing future
- ```TWriter```: Defines a type alias for a YT table writer

# Code Review
### Strengths
1. Clear and Concise Comments:
    - Each function, class, and key variable is well-documented
    - Comments explain the purpose, parameters, and return values
2. Modular Design:
    - The code is organized into reusable functions and classes
    - Build configurations are modular and support both ```CPU``` and ```GPU``` backends
3. Unit Tests:
    - Comprehensive tests verify the correctness of the code
    - Tests are organized into ```CPU``` and ```GPU``` backends
4. Integration with YT:
    - The pipeline integrates seamlessly with Yandex Table for distributed processing
    - Configuration files are well-documented and easy to modify

### Areas for Improvement
1. Consistency:
    - Ensure all functions and classes have consistent commenting styles
2. Detailed Explanations:
    - Add more detailed explanations for complex logic or algorithms
3. Documentation:
    - Include a high-level overview of the project in the ```README.md```

# Usage
### Building the Project
1. Clone the repository
2. Navigate to the project directory
3. Run the build command:
```ya make```

### Running the Pipeline
1. Prepare input data in a YT table
2. Run the pipeline with the following command
```./main --input <input_table> --output <output_table> --folder <model_folder>```

#### Options
- ```--input```: Path to the input YT table
- ```--output```: Path to the output YT table
- ```--folder```: Path to the model folder
- ```--batchsize```: Maximum batch size (```default: 256```)
- ```--maxinputlength```: Maximum input length (```default: 127```)
- ```--contextlen```: Context length (```default: 3```)
- ```--truncateasdialogue```: Truncate input as dialogue (```default: false```)

### Running Unit Tests
1. Navigate to the ```ut/cpu``` or ```ut/gpu``` directory
2. Run the tests:
```ya make -t```
