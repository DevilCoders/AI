```cmake
PY3_PROGRAM()  # Define a new build target for creating a Python 3 executable program

OWNER(  # Specify the owners or maintainers of this build target
    nzinov  # Individual owner (e.g., a developer)
    g:alice_boltalka  # Group owner (e.g., a team or organization)
)

PY_SRCS(TOP_LEVEL generate_negatives.py)  # Specify the Python source files to include in the build
# TOP_LEVEL indicates that the file is in the root directory of the project
# `generate_negatives.py` is the main Python script to be included

PY_MAIN(generate_negatives)  # Specify the entry point (main module) for the Python program
# This tells the build system which script to run when the program is executed

PEERDIR(  # Specify directories of dependencies that this program relies on
    yt/python/client  # Include the YT Python client library as a dependency
    alice/boltalka/tools/dssm_preprocessing/preprocessing/lib  # Include the DSSM preprocessing library as a dependency
)

END()  # End the definition of the build target
```
