```cmake
# Recursively includes the `lib`, `so`, and `tools` directories in the build process
RECURSE(
    lib   # Likely contains core library code
    so    # Possibly shared object files or compiled binaries
    tools # Additional tools, scripts, or utilities
)

# Recursively includes the `tests` directory **only for test builds**
RECURSE_FOR_TESTS(tests)
```
