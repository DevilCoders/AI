# Emoji Classifier
This project provides a TensorFlow-based model for classifying emojis based on input embeddings. It includes a classifier model and a configuration loader to parse JSON configuration files.

## Overview
The Emoji Classifier is a C++ library that uses TensorFlow to predict the most appropriate emoji for a given pair of query and reply embeddings. It includes:

- A **classifier model** (`TEmojiClassifierModel`) that loads a TensorFlow model and makes predictions.
- A **configuration loader** that parses JSON files to load model and emoji configurations.
- A **classifier** (`TEmojiClassifier`) that wraps the model and provides a simple interface for predictions.

## Components
### 1. `TEmojiClassifierModel`

- **Purpose**: Loads a TensorFlow model and makes predictions based on input embeddings.
- **Key Features**:
  - Loads model configuration from a JSON file.
  - Processes query and reply embeddings to generate prediction scores.
  - Provides the embedding size used by the model.

### 2. `TEmojiClassifier`
- **Purpose**: Wraps the `TEmojiClassifierModel` and provides a higher-level interface for predicting emojis.
- **Key Features**:
  - Loads emoji configurations from a JSON file.
  - Predicts the most appropriate emoji for a given pair of embeddings.

### 3. ```Configuration Loader```
- **Purpose**: Parses JSON files to load model and emoji configurations.
- **Key Features**:
  - Validates JSON input streams.
  - Extracts configuration parameters such as input/output node names and embedding size.

## Build Instructions
To build the project, follow these steps:

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```

## Build the library
The dependencies for building the Emoji Classifier library are listed in the PEERDIR section of the ya.make file. Here’s a detailed explanation of the dependencies and how to ensure they are installed:

- Run the following command to build the library:
```ya make```

### Include the library in your project
- Add the following to your ```ya.make``` file:

```cmake
PEERDIR(
    <path-to-emoji-classifier>
)
```

### Dependency Tree
Emoji Classifier
├── TensorFlow Neural Network Model (alice/nlu/libs/tf_nn_model)
├── JSON Library (library/cpp/json)
├── TensorFlow
├── C++ Compiler (g++ or clang++)
└── Yandex Build System (ya)

---

### Required Dependencies
- TensorFlow Neural Network Model (```alice/nlu/libs/tf_nn_model```)
    - ```Purpose```: Provides the base TensorFlow model functionality used by ```TEmojiClassifierModel```
    - ```Installation```:
        - Ensure the ```alice/nlu/libs/tf_nn_model``` library is available in your workspace
        - If you’re working in a ```Yandex environment```, this library is typically part of the ```Alice NLU project```. You may need to ```clone``` or ```include it``` in your ```build configuration```
- JSON Library (```library/cpp/json```):
    - ```Purpose```: Provides JSON parsing functionality for loading configuration files
    - ```Installation```: 
        - The ```library/cpp/json``` library is part of the ```Yandex C++``` libraries. Ensure it is available in your workspace
        - If you’re using ```ya``` (Yandex build system), this library is usually included by default. If not, you may need to add it to your ```PEERDIR```
- TensorFlow:
    - ```Purpose```: The underlying machine learning framework used by the model
    - ```Installation```: 
        - Ensure TensorFlow is installed and properly configured in your environment
        - If you’re using a prebuilt TensorFlow model, ensure the model files are accessible
- C++ Compiler:
    - ```Purpose```: Required to compile the C++ code
    - ```Installation```:
        - Ensure you have a compatible C++ compiler (e.g., ```g++``` or ```clang++```)
        - Install the compiler if it’s not already available on your system
- Yandex Build System (```ya```):
    - ```Purpose```: Used to build the project
    - ```Installation```: 
        - Ensure the ```ya``` build system is ```installed``` and ```configured``` on your machine
        - Follow the official Yandex documentation to set up ```ya``` if it’s not already installed

## Install Dependencies
Ensure the following dependencies are installed:
- ```TensorFlow Neural Network Model```: Available in ```alice/nlu/libs/tf_nn_model```
- ```JSON Library```: Available in ```library/cpp/json```
- ```TensorFlow```: Install TensorFlow by following the [official guide] **https://www.tensorflow.org/install**
- ```C++ Compiler```: Install ```g++``` or ```clang++```
- Yandex Build System (```ya```): Ensure ```ya``` is ```installed``` and ```configured```

---

1. TensorFlow Neural Network Model (```alice/nlu/libs/tf_nn_model```)
```Purpose```: Provides the base ```TensorFlow model``` functionality used by ```TEmojiClassifierModel```.
```Installation```:
- This library is ```part``` of the ```Alice NLU project```.
- Ensure the ```library``` is available in your workspace.
- If missing, clone the repository: ```git clone <alice-nlu-repo-url>```
- Add the library to your ```PEERDIR``` in the ```ya.make``` file:
```cmake
PEERDIR(
    alice/nlu/libs/tf_nn_model
)
```

2. JSON Library (```library/cpp/json```)
```Purpose```: Provides JSON parsing functionality for loading configuration files.
```Installation```:
- This library is ```part``` of the ```Yandex C++ libraries```
- Ensure the ```library``` is available in your workspace
- If missing, clone the repository: ```git clone <yandex-cpp-lib-repo-url>```
- Add the library to your ```PEERDIR``` in the ```ya.make``` file:
```cmake
PEERDIR(
    library/cpp/json
)
```

3. TensorFlow
```Purpose```: The underlying machine learning framework used by the model.
```Installation```:
- Follow the official TensorFlow installation guide for your platform:
- TensorFlow 
    - Installation Guide: https://www.tensorflow.org/install
- Ensure ```TensorFlow``` is installed and properly configured in your environment.
- Verify the installation: ```python3 -c "import tensorflow as tf; print(tf.__version__)"```

4. C++ Compiler
```Purpose```: Required to ```compile the C++ code```.
```Installation```:
- Install a compatible C++ compiler (e.g., ```g++``` or ```clang++```)
- On Ubuntu/Debian:
```shell
sudo apt update
sudo apt install g++
```
or

```shell
sudo apt update
sudo apt install clang++
```

- Verify the installation:
```shell
g++ --version
```

or

```shell
clang++ --version
```

### Additional Tools
- ```CMake``` (optional): For ```building``` the project ```outside``` of the ```ya``` environment
    - Install CMake: ```sudo apt install cmake```shell
    - Verify the installation: ```cmake --version```shell

## How to Ensure Dependencies Are Installed
1. Check Your Workspace:
    - Ensure the required libraries (```alice/nlu/libs/tf_nn_model``` and ```library/cpp/json```) are available in your workspace
    - If they are missing, clone or download them from the appropriate repositories
2. Install TensorFlow:
    - If TensorFlow is not already installed, follow the official TensorFlow installation guide for your platform:
    - https://www.tensorflow.org/install
3. Set Up the Build Environment:
    - Ensure the ```ya``` build system is ```installed``` and ```configured```
    - Run ```ya make``` in the project directory to ```verify``` that ```all dependencies``` are resolved
4. Verify Compiler:
    - Ensure a ```C++ compiler``` is ```installed``` and ```accessible``` in your environment
    - Test by running ```g++ --version``` or ```clang++ --version``` in your terminal (Linux e.g. Ubuntu)
