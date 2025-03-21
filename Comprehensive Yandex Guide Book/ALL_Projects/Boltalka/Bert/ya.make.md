```cmake
RECURSE(  # Recursively include build configurations from the specified directories
    bin  # Include the build configuration from the `bin` directory
    clever_negatives  # Include the build configuration from the `clever_negatives` directory
    lib  # Include the build configuration from the `lib` directory
    ut/cpu  # Include the build configuration from the `ut/cpu` directory (CPU-specific unit tests)
    ut/gpu  # Include the build configuration from the `ut/gpu` directory (GPU-specific unit tests)
    yt_apply  # Include the build configuration from the `yt_apply` directory (YT-related functionality)
)
```
