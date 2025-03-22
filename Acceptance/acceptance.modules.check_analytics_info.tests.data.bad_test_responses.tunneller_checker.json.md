```json
{
    "result": {
        // Contains the summary result of the checking process.
        "description": "checks emptiness, base64 correctness of tunneller raw responses",
        // Describes the purpose of the checker, which is to check if tunneller raw responses are non-empty and valid Base64.

        "message": "stats of test downloading:\nvins responses: 4\ntunneller responses: 8\nempty tunneller responses: 1\nundecodable tunneller responses: 1\ngood tunneller responses: 6\nmean tunneller responses 2.00\n\nstats of stable downloading:\nvins responses: 5\ntunneller responses: 15\nempty tunneller responses: 0\nundecodable tunneller responses: 0\ngood tunneller responses: 15\nmean tunneller responses 3.00\n\namount empty tunneller responses of test downloading is not 0\namount undecodable tunneller responses of test downloading is not 0\n",
        // Provides a detailed message summarizing the results of the checking process.
        // Includes statistics for both test and stable downloading, such as:
        // - Number of Vins responses.
        // - Number of tunneller responses.
        // - Number of empty tunneller responses.
        // - Number of undecodable tunneller responses.
        // - Number of good tunneller responses.
        // - Mean number of tunneller responses per Vins response.
        // Also includes a conclusion about the test and stable downloading.

        "name": "tunneller_checker",
        // Specifies the name of the checker (`tunneller_checker`).

        "verdict": false
        // Indicates the overall verdict of the checking process.
        // `false` means the test downloading is invalid due to empty or undecodable tunneller responses.
    },
    "row_dumps": [
        // Contains the results of processing each row of data.
        [
            false,
            // Indicates that the first row is invalid (`false`).
            "amount of good tunneller responses (2) in test response not equals to amount (3) in stable response"
            // Provides a message explaining why the row is invalid.
        ],
        [
            false,
            // Indicates that the second row is invalid (`false`).
            "amount of tunneller responses (2) in test response not equals to amount (3) in stable response"
            // Provides a message explaining why the row is invalid.
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
            "amount of tunneller responses (0) in test response not equals to amount (3) in stable response"
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
