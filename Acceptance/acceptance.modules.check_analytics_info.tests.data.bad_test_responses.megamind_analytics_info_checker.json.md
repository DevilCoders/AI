```json
{
    "result": {
        // Contains the summary result of the checking process.
        "description": "checks presence of megamind_analytics_info and original_utterance",
        // Describes the purpose of the checker, which is to check if `megamind_analytics_info` and `original_utterance` are present.

        "message": "stats of test downloading:\nvins responses: 4\nmegamind analytics info: 3\noriginal utterance: 2\n\nstats of stable downloading:\nvins responses: 5\nmegamind analytics info: 5\noriginal utterance: 5\n\nmegamind analytics info is not present in every response of test downloading\noriginal utterance is not present in megamind analytics info of test downloading\n",
        // Provides a detailed message summarizing the results of the checking process.
        // Includes statistics for both test and stable downloading, such as:
        // - Number of Vins responses.
        // - Number of responses containing `megamind_analytics_info`.
        // - Number of responses containing `original_utterance`.
        // Also includes a conclusion about the test and stable downloading.

        "name": "megamind_analytics_info_checker",
        // Specifies the name of the checker (`megamind_analytics_info_checker`).

        "verdict": false
        // Indicates the overall verdict of the checking process.
        // `false` means the test downloading is invalid due to missing `megamind_analytics_info` or `original_utterance`.
    },
    "row_dumps": [
        // Contains the results of processing each row of data.
        [
            false,
            // Indicates that the first row is invalid (`false`).
            "original utterance is present in stable response but absent in test"
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
            "megamind analytics info is present in stable response but absent in test"
            // Provides a message explaining why the row is invalid.
        ],
        [
            true,
            // Indicates that the fifth row is valid (`true`).
            null
            // No message is provided since the row is valid.
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
