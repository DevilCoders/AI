```json
{
    "result": {
        // Contains the summary result of the checking process.
        "description": "checks presence of megamind_analytics_info and original_utterance",
        // Describes the purpose of the checker, which is to check if `megamind_analytics_info` and `original_utterance` are present.

        "message": "stats of test downloading:\nvins responses: 2\nmegamind analytics info: 2\noriginal utterance: 2\n\nstats of stable downloading:\nvins responses: 3\nmegamind analytics info: 3\noriginal utterance: 3\n\ntest downloading is ok\n",
        // Provides a detailed message summarizing the results of the checking process.
        // Includes statistics for both test and stable downloading, such as:
        // - Number of Vins responses.
        // - Number of responses containing `megamind_analytics_info`.
        // - Number of responses containing `original_utterance`.
        // Also includes a conclusion about the test and stable downloading.

        "name": "megamind_analytics_info_checker",
        // Specifies the name of the checker (`megamind_analytics_info_checker`).

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
