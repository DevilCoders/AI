```cmake
# Define a Python 3 library target
PY3_LIBRARY()

# Specify the owner of the target (e.g., a group or team)
OWNER(
    # The owner is the group "alice_downloaders"
    g:alice_downloaders
)

# Specify the Python source files for this library
PY_SRCS(
    # The source file for the library, which contains configuration settings
    config.py
)

# End of the configuration
END()
```
