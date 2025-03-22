```json
{
    "result": {
        // Contains the summary result of the checking process.
        "description": "checks non emptiness of meta",
        // Describes the purpose of the checker, which is to check if the `meta` field is non-empty.

        "message": "stats of test downloading\nvins responses: 2\nnot empty metas: 2\n\nstats of stable downloading\nvins responses: 3\nnot empty metas: 3\n\ntest downloading is ok\n",
        // Provides a detailed message summarizing the results of the checking process.
        // Includes statistics for both test and stable downloading, such as:
        // - Number of Vins responses.
        // - Number of responses with non-empty `meta`.
        // Also includes a conclusion about the test and stable downloading.

        "name": "meta_checker",
        // Specifies the name of the checker (`meta_checker`).

        "verdict": true
        // Indicates the overall verdict of the checking process.
        // `true` means the test downloading is valid.
    },
    "row_dumps": [
        // Contains the results of processing each row of data.
        [
            true,
            // Indicates that the first row is valid (`true`).
            null
            // No message is provided since the row is valid.
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
            true,
            // Indicates that the fourth row is valid (`true`).
            null
            // No message is provided since the row is valid.
        ]
    ]
}
```
