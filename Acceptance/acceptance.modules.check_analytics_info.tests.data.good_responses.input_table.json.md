```json
[
  {
    "test.VinsResponse": "{\"directive\": {\"payload\": {\"megamind_analytics_info\": {\"tunneller_raw_responses\": {\"alice.vins\": {\"responses\": [\"CAESCgoDa2VrEgNsb2w==\", \"CAESCgoDbG9sEgNrZWs=\"]}, \"megamind\": {\"responses\": [\"CAESCgoDa2VrEgNsb2w=\"]}}, \"original_utterance\": \"keklol\"}, \"response\": {\"meta\": [3, 2, 1]}}}}",
    // Represents the test Vins response for the first row.
    // Contains `megamind_analytics_info` with `tunneller_raw_responses` for `alice.vins` and `megamind`.
    // Both `alice.vins` and `megamind` responses are valid Base64 strings.
    // The `original_utterance` field is set to "keklol".
    // The `meta` field in the response contains a list of integers `[3, 2, 1]`.

    "stable.VinsResponse": "{\"directive\": {\"payload\": {\"megamind_analytics_info\": {\"tunneller_raw_responses\": {\"alice.vins\": {\"responses\": [\"CAESCgoDbG9sEgNrZWs=\", \"CAESCgoDa2VrEgNsb2w==\"]}, \"megamind\": {\"responses\": [\"CAESCgoDa2VrEgNsb2w=\"]}}, \"original_utterance\": \"lolkek\"}, \"response\": {\"meta\": [1, 2, 3]}}}}"
    // Represents the stable Vins response for the first row.
    // Contains `megamind_analytics_info` with `tunneller_raw_responses` for `alice.vins` and `megamind`.
    // Both `alice.vins` and `megamind` responses are valid Base64 strings.
    // The `original_utterance` field is set to "lolkek".
    // The `meta` field in the response contains a list of integers `[1, 2, 3]`.
  },
  {
    "test.VinsResponse": "{\"directive\": {\"payload\": {\"megamind_analytics_info\": {\"tunneller_raw_responses\": {\"alice.vins\": {\"responses\": [\"CAESCQoDNDIwEgI2OQ==\"]}}, \"original_utterance\": \"lolkek\"}, \"response\": {\"meta\": [123]}}}}",
    // Represents the test Vins response for the second row.
    // Contains `megamind_analytics_info` with `tunneller_raw_responses` for `alice.vins`.
    // The `alice.vins` response is a valid Base64 string.
    // The `megamind` response is missing.
    // The `original_utterance` field is set to "lolkek".
    // The `meta` field in the response contains a list with a single integer `[123]`.

    "stable.VinsResponse": "{\"directive\": {\"payload\": {\"megamind_analytics_info\": {\"tunneller_raw_responses\": {\"alice.vins\": {\"responses\": [\"CAESCgoDbG9sEgNrZWs=\", \"CAESCgoDa2VrEgNsb2w==\"]}, \"megamind\": {\"responses\": [\"CAESCgoDa2VrEgNsb2w=\"]}}, \"original_utterance\": \"lolkek\"}, \"response\": {\"meta\": [1, 2, 3]}}}}"
    // Represents the stable Vins response for the second row.
    // Contains `megamind_analytics_info` with `tunneller_raw_responses` for `alice.vins` and `megamind`.
    // Both `alice.vins` and `megamind` responses are valid Base64 strings.
    // The `original_utterance` field is set to "lolkek".
    // The `meta` field in the response contains a list of integers `[1, 2, 3]`.
  },
  {
    "test.VinsResponse": null,
    // Represents the test Vins response for the third row.
    // The test response is `null`, indicating it is missing or invalid.

    "stable.VinsResponse": "{\"directive\": {\"payload\": {\"megamind_analytics_info\": {\"tunneller_raw_responses\": {\"alice.vins\": {\"responses\": [\"CAESCgoDbG9sEgNrZWs=\", \"CAESCgoDa2VrEgNsb2w==\"]}, \"megamind\": {\"responses\": [\"CAESCgoDa2VrEgNsb2w=\"]}}, \"original_utterance\": \"lolkek\"}, \"response\": {\"meta\": [1, 2, 3]}}}}"
    // Represents the stable Vins response for the third row.
    // Contains `megamind_analytics_info` with `tunneller_raw_responses` for `alice.vins` and `megamind`.
    // Both `alice.vins` and `megamind` responses are valid Base64 strings.
    // The `original_utterance` field is set to "lolkek".
    // The `meta` field in the response contains a list of integers `[1, 2, 3]`.
  },
  {
    "test.VinsResponse": null,
    // Represents the test Vins response for the fourth row.
    // The test response is `null`, indicating it is missing or invalid.

    "stable.VinsResponse": null
    // Represents the stable Vins response for the fourth row.
    // The stable response is `null`, indicating it is missing or invalid.
  }
]
```
