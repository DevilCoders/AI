```cmake
SRCS(  # Specify the source files to be included in the build
	../main.cpp  # Include the main.cpp file from the parent directory
)

DATA(  # Specify additional data files required for the build
	sbr://1429884427  # Reference to a data file in the Sandbox Resource Base (SBR)
	sbr://1429944589  # Reference to another data file in SBR
	sbr://1429946448  # Reference to another data file in SBR
	sbr://1429947801  # Reference to another data file in SBR
)

PEERDIR(  # Specify directories of dependencies that this build target relies on
	alice/boltalka/bert/lib  # Include the BERT library as a dependency
	dict/mt/libs/nn/ynmt/test_utils/cpu  # Include CPU-specific test utilities for YNMT as a dependency
)
```
