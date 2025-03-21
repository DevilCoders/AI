```cmake
UNITTEST()  # Define a new build target for unit tests

OWNER(  # Specify the owners or maintainers of this build target
    nzinov  # Individual owner (e.g., a developer)
    g:alice_boltalka  # Group owner (e.g., a team or organization)
)

SIZE(MEDIUM)  # Specify the size of the unit test (e.g., MEDIUM for moderate runtime and resource usage)

PEERDIR(  # Specify directories of dependencies that this unit test relies on
    dict/mt/libs/nn/ynmt/test_utils/cpu  # Include CPU-specific test utilities for YNMT
)

INCLUDE(${ARCADIA_ROOT}/alice/boltalka/bert/ut/ya.make.inc)  # Include additional build configuration from the specified path

END()  # End the definition of the build target
```
