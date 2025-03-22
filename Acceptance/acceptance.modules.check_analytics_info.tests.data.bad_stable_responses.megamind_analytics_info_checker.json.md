```json
{
    "result": {
        // Contains the summary result of the checking process.
        "description": "checks presence of megamind_analytics_info and original_utterance",
        // Describes the purpose of the checker.

        "message": "stats of test downloading:\nvins responses: 5\nmegamind analytics info: 5\noriginal utterance: 5\n\nstats of stable downloading:\nvins responses: 4\nmegamind analytics info: 3\noriginal utterance: 2\n\ntest downloading is ok but some stable downloading vins responses has no megamind analytics info or original utterance\n",
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
        // `true` means the test downloading is valid, but there are issues with the stable downloading.
    },
    "row_dumps": [
        // Contains the results of processing each row of data.
        [
            false,
            // Indicates that the first row is invalid (`false`).
            "original utterance is present in test response but absent in stable"
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
            "megamind analytics info is present in test response but absent in stable"
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
