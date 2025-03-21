```json
{
    cluster = hahn;  # Specify the YT cluster to use (e.g., "hahn")
    pool = "dialogs";  # Specify the YT pool to use (e.g., "dialogs")
    cypress_root = "//home/dialogs/ytexec-cache";  # Specify the root path in Cypress (YT's file system) for caching
    "coordinate_upload" = %false;  # Disable coordinated upload of files (e.g., layers) to YT

    "operation_spec" = {  # Define specifications for the YT operation
        "scheduling_tag_filter" = "porto";  # Use the "porto" scheduling tag for resource allocation
        "pool_trees" = [  # Specify the pool trees to use for resource allocation
            "gpu_geforce_1080ti";  # Use the GPU pool tree for NVIDIA GeForce 1080 Ti GPUs
        ];
        "pool" = "research_gpu";  # Specify the pool to use within the pool tree (e.g., "research_gpu")
    };

    "task_spec" = {  # Define specifications for the YT task
        "gpu_limit" = 1;  # Set the GPU limit to 1 (i.e., use 1 GPU per task)
        "layer_paths" = [  # Specify the paths to the layers required for the task
            "//porto_layers/delta/gpu/driver/418.67";  # Path to the GPU driver layer (version 418.67)
            "//porto_layers/ubuntu-xenial-base.tar.xz";  # Path to the base Ubuntu Xenial layer
        ];
    };
}
```
