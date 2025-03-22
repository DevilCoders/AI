```json
{
    "result": {
        // Contains the summary result of the checking process.
        "description": "checks non emptiness of meta",
        // Describes the purpose of the checker, which is to check if the `meta` field is non-empty.

        "message": "stats of test downloading\nvins responses: 5\nnot empty metas: 5\n\nstats of stable downloading\nvins responses: 4\nnot empty metas: 1\n\ntest downloading is ok but some stable downloading vins responses has empty meta\n",
        // Provides a detailed message summarizing the results of the checking process.
        // Includes statistics for both test and stable downloading, such as:
        // - Number of Vins responses.
        // - Number of responses with non-empty `meta`.
        // Also includes a conclusion about the test and stable downloading.

        "name": "meta_checker",
        // Specifies the name of the checker (`meta_checker`).

        "verdict": true
        // Indicates the overall verdict of the checking process.
        // `true` means the test downloading is valid, but there are issues with the stable downloading.
    },
    "row_dumps": [
        // Contains the results of processing each row of data.
        [
            false,
            // Indicates that the first row is invalid (`false`).
            "meta is present in test response but absent in stable"
            // Provides a message explaining why the row is invalid.
        ],
        [
            true,
            // Indicates that the second row is valid (`true`).
            null
            // No message is provided since the row is valid.
        ],
        [
            true,
            // Indicates that the third row is valid (`true`).
            "vins response from stable downloading is empty"
            // Provides a message indicating that the stable response is missing.
        ],
        [
            false,
            // Indicates that the fourth row is invalid (`false`).
            "meta is present in test response but absent in stable"
            // Provides a message explaining why the row is invalid.
        ],
        [
            false,
            // Indicates that the fifth row is invalid (`false`).
            "meta is present in test response but absent in stable"
            // Provides a message explaining why the row is invalid.
        ],
        [
            true,
            // Indicates that the sixth row is valid (`true`).
            null
            // No message is provided since the row is valid.
        ]
    ]
}
```
