```cmake
LIBRARY()  # Define a new build target for creating a library

OWNER(  # Specify the owners or maintainers of this build target
    nzinov  # Individual owner (e.g., a developer)
    g:alice_boltalka  # Group owner (e.g., a team or organization)
)

SRCS(  # Specify the source files to be included in the library
    main.h  # Include the main.h file as part of the library
)

IF (USE_GPU)  # Check if the USE_GPU flag is enabled
    CFLAGS(-DUSE_GPU)  # Add a compiler flag to define USE_GPU for conditional compilation
ENDIF()  # End the conditional block

PEERDIR(  # Specify directories of dependencies that this library relies on
    dict/mt/libs/nn/ynmt/config_helper  # Include the YNMT config helper library
    dict/mt/libs/nn/ynmt/extra  # Include the YNMT extra utilities library
    dict/mt/libs/nn/ynmt_backend/cpu  # Include the YNMT CPU backend library
    dict/mt/libs/nn/ynmt_backend/gpu  # Include the YNMT GPU backend library
    kernel/bert  # Include the BERT kernel library
    library/cpp/float16  # Include the float16 library for half-precision floating-point support
    library/cpp/getopt/small  # Include the small getopt library for command-line argument parsing
)

END()  # End the definition of the build target
```
