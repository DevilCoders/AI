```cmake
PROGRAM()  # Define a new build target for creating an executable program

SRCS(  # Specify the source files to be compiled for this program
	main.cpp  # Include the main.cpp file as the primary source file
)

IF (USE_GPU)  # Check if the USE_GPU flag is enabled
    CFLAGS(-DUSE_GPU)  # Add a compiler flag to define USE_GPU for conditional compilation
ENDIF()  # End the conditional block

PEERDIR(  # Specify directories of dependencies that this program relies on
	alice/boltalka/bert/lib  # Include the BERT library as a dependency
)

END()  # End the definition of the build target
```
