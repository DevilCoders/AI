```json
{
    "result": {
        // Contains the summary result of the checking process.
        "description": "checks non emptiness of meta",
        // Describes the purpose of the checker, which is to check if the `meta` field is non-empty.

        "message": "stats of test downloading\nvins responses: 4\nnot empty metas: 1\n\nstats of stable downloading\nvins responses: 5\nnot empty metas: 5\n\nmeta is not present in every response of test downloading\n",
        // Provides a detailed message summarizing the results of the checking process.
        // Includes statistics for both test and stable downloading, such as:
        // - Number of Vins responses.
        // - Number of responses with non-empty `meta`.
        // Also includes a conclusion about the test and stable downloading.

        "name": "meta_checker",
        // Specifies the name of the checker (`meta_checker`).

        "verdict": false
        // Indicates the overall verdict of the checking process.
        // `false` means the test downloading is invalid due to missing `meta` in some responses.
    },
    "row_dumps": [
        // Contains the results of processing each row of data.
        [
            false,
            // Indicates that the first row is invalid (`false`).
            "meta is present in stable response but absent in test"
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
            "vins response from test downloading is empty"
            // Provides a message indicating that the test response is missing.
        ],
        [
            false,
            // Indicates that the fourth row is invalid (`false`).
            "meta is present in stable response but absent in test"
            // Provides a message explaining why the row is invalid.
        ],
        [
            false,
            // Indicates that the fifth row is invalid (`false`).
            "meta is present in stable response but absent in test"
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
