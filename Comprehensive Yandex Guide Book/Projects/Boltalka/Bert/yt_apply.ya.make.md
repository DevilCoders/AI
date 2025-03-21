```cmake
PROGRAM()  # Define a new build target for creating an executable program

SRCS(  # Specify the source files to be compiled for this program
	main.cpp  # Include the main.cpp file as the primary source file
)

IF (USE_GPU)  # Check if the USE_GPU flag is enabled
    CFLAGS(-DUSE_GPU)  # Add a compiler flag to define USE_GPU for conditional compilation
ENDIF()  # End the conditional block

PEERDIR(  # Specify directories of dependencies that this program relies on
    alice/boltalka/generative/service/server/handlers  # Include handlers for the generative service
    dict/mt/libs/nn/ynmt/extra  # Include extra utilities for YNMT
    mapreduce/yt/client  # Include the YT (Yandex Table) client library
    mapreduce/yt/interface  # Include the YT interface library
    library/cpp/getopt/small  # Include the small getopt library for command-line argument parsing
)

END()  # End the definition of the build target
```
