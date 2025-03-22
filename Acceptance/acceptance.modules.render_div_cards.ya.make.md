```cmake
# Recursively include the specified directories in the build process
RECURSE (
    # Include the "bin" directory, which typically contains executable scripts or binaries
    bin
    # Include the "bin_vanadium" directory, which may contain additional binaries or scripts
    bin_vanadium
    # Include the "lib" directory, which typically contains library code or modules
    lib
    # Include the "upload" directory, which may contain files or scripts related to uploading data
    upload
)
```
