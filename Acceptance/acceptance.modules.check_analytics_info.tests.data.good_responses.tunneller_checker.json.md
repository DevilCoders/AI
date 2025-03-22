```json
{
    "result": {
        // Contains the summary result of the checking process.
        "description": "checks emptiness, base64 correctness of tunneller raw responses",
        // Describes the purpose of the checker, which is to check if tunneller raw responses are non-empty and valid Base64.

        "message": "stats of test downloading:\nvins responses: 2\ntunneller responses: 4\nempty tunneller responses: 0\nundecodable tunneller responses: 0\ngood tunneller responses: 4\nmean tunneller responses 2.00\n\nstats of stable downloading:\nvins responses: 3\ntunneller responses: 9\nempty tunneller responses: 0\nundecodable tunneller responses: 0\ngood tunneller responses: 9\nmean tunneller responses 3.00\n\nmean of tunneller responses of test downloading (2.00) differs more than 0.02 comparing to stable downloading (3.00) by abs value\n",
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
        // `false` means the test downloading is invalid due to differences in tunneller responses compared to stable downloading.
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
            false,
            // Indicates that the second row is invalid (`false`).
            "amount of tunneller responses (1) in test response not equals to amount (3) in stable response"
            // Provides a message explaining why the row is invalid.
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
