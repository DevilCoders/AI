```python
# coding: utf-8
# Specifies the encoding of the file as UTF-8 to ensure proper handling of Unicode characters.

import json
# Imports the `json` module, which provides functions to work with JSON data (e.g., parsing and serializing).

import logging
# Imports the `logging` module, which provides functions for logging messages (e.g., errors, warnings).

import math
# Imports the `math` module, which provides mathematical functions and constants.

import tempfile
# Imports the `tempfile` module, which provides functions for creating temporary files and directories.

import vh
# Imports the `vh` module, which is likely a custom or third-party module for handling data or virtual files.

def _get_payload_item(mm_response, name, def_value=None):
    # Defines a helper function named `_get_payload_item` that retrieves a specific item from a nested dictionary.
    # The function takes three arguments:
    # - `mm_response`: A dictionary containing the response data.
    # - `name`: The key of the item to retrieve.
    # - `def_value`: The default value to return if the item is not found (defaults to `None`).

    # NOTE(a-square): in case someone might search 'directive', try the longer path first
    # Attempts to retrieve the item from the nested path 'directive.payload.name' first.
    # If not found, tries to retrieve it directly from the top level of `mm_response`.
    item = mm_response.get('directive', {}).get('payload', {}).get(name) or mm_response.get(name)

    return def_value if item is None else item
    # Returns the retrieved item if found, otherwise returns the default value (`def_value`).

def _get_new_analytics_info(mm_response):
    # Defines a helper function named `_get_new_analytics_info` that extracts analytics information from the response.
    # The function takes one argument:
    # - `mm_response`: A dictionary containing the response data.

    store = _get_payload_item(mm_response, 'megamind_analytics_info').get('analytics_info')
    # Retrieves the 'analytics_info' dictionary from the 'megamind_analytics_info' field using `_get_payload_item`.

    if not store:
        # Checks if the 'analytics_info' dictionary is empty or not found.
        return None
        # Returns `None` if no analytics information is available.

    items = list(store.items())
    # Converts the 'analytics_info' dictionary into a list of key-value pairs.

    assert len(items) == 1
    # Asserts that there is exactly one key-value pair in the 'analytics_info' dictionary.
    # Raises an `AssertionError` if this condition is not met.

    scenario_name, analytics_info = items[0]
    # Unpacks the single key-value pair into `scenario_name` and `analytics_info`.

    return scenario_name, analytics_info
    # Returns the scenario name and its corresponding analytics information.

def parse_comparable_data(mm_response):
    # Defines a function named `parse_comparable_data` that parses and extracts comparable data from a response.
    # The function takes one argument:
    # - `mm_response`: A JSON string or dictionary containing the response data.

    if not mm_response:
        # Checks if `mm_response` is empty or falsy.
        return (None, None)
        # Returns a tuple of `(None, None)` if `mm_response` is empty.

    mm_response = json.loads(mm_response)
    # Parses the `mm_response` JSON string into a Python dictionary.

    response = _get_payload_item(mm_response, 'response', {})
    # Retrieves the 'response' field from `mm_response` using `_get_payload_item`.
    # If not found, defaults to an empty dictionary.

    scenario_name, analytics_info = _get_new_analytics_info(mm_response)
    # Extracts the scenario name and analytics information using `_get_new_analytics_info`.

    intent = None
    # Initializes `intent` to `None`.

    if analytics_info:
        # Checks if `analytics_info` is not empty.
        intent = (
            analytics_info.get('scenario_analytics_info', {}).get('intent') or
            analytics_info.get('semantic_frame', {}).get('name')
        )
        # Attempts to retrieve the intent from either 'scenario_analytics_info' or 'semantic_frame' in `analytics_info`.

    intent = intent or scenario_name
    # If `intent` is still `None`, uses the `scenario_name` as the intent.

    if not intent:
        # Checks if `intent` is still `None` after all attempts.
        logging.error('No analytics_info or no intent in response: %r')
        # Logs an error message indicating that no intent or analytics information was found.

    directives = response.get('directives', [])
    # Retrieves the 'directives' list from the `response` dictionary.
    # If not found, defaults to an empty list.

    directives_result = ', '.join('{}:{}'.format(d['type'], d['name']) for d in directives)
    # Formats each directive in the 'directives' list as 'type:name' and joins them into a single string.

    return ({
        'intent': intent,
        # Adds the extracted intent to the result dictionary.
        'directives': directives_result,
        # Adds the formatted directives string to the result dictionary.
    }, mm_response)
    # Returns a tuple containing:
    # - A dictionary with the parsed intent and directives.
    # - The original `mm_response` dictionary.
```

```python
def create_diff(reference_data, downloaded_data):
    # Defines a function named `create_diff` that compares reference data with downloaded data and identifies differences.
    # The function takes two arguments:
    # - `reference_data`: A dictionary containing the expected reference data.
    # - `downloaded_data`: A dictionary containing the actual downloaded data.

    missed = {}
    # Initializes an empty dictionary named `missed` to store entries that are present in `reference_data` but missing in `downloaded_data`.

    diff = {}
    # Initializes an empty dictionary named `diff` to store entries where the reference data and downloaded data differ.

    for key in reference_data.keys():
        # Iterates over each key in the `reference_data` dictionary.

        # If statements order is important
        if reference_data[key].get('xfail'):
            # Checks if the current entry in `reference_data` has an 'xfail' key (indicating it is expected to fail).
            continue
            # Skips this entry if it is marked as 'xfail'.

        elif key not in downloaded_data:
            # Checks if the current key is missing in the `downloaded_data` dictionary.
            missed[key] = {
                'expected': reference_data[key],
                'downloaded': None,
            }
            # Adds the missing entry to the `missed` dictionary with:
            # - 'expected': The value from `reference_data`.
            # - 'downloaded': `None` (since the data is missing).

        elif reference_data[key] == downloaded_data[key]['downloaded']:
            # Checks if the value in `reference_data` matches the 'downloaded' value in `downloaded_data`.
            continue
            # Skips this entry if the values match.

        else:
            # If the values do not match, this block executes.
            diff[key] = {'expected': reference_data[key]}
            # Adds the expected value from `reference_data` to the `diff` dictionary.

            diff[key].update(downloaded_data[key])
            # Updates the `diff` entry with the corresponding data from `downloaded_data`.

    return diff, missed
    # Returns a tuple containing:
    # - `diff`: A dictionary of entries where the reference and downloaded data differ.
    # - `missed`: A dictionary of entries that are missing in the downloaded data.
```

```python
@vh.lazy((vh.File, vh.File, vh.File, bool), reference_requests=vh.File, downloaded_requests=vh.File)
# Decorates the `compare_results` function with `vh.lazy`, indicating it is a lazy-evaluated function.
# Specifies that the function takes two `vh.File` inputs (`reference_requests` and `downloaded_requests`)
# and returns a tuple of three `vh.File` objects and a boolean.

def compare_results(reference_requests, downloaded_requests):
    # Defines a function named `compare_results` that compares reference requests with downloaded requests.
    # The function takes two arguments:
    # - `reference_requests`: A file containing the expected reference requests.
    # - `downloaded_requests`: A file containing the actual downloaded requests.

    with open(reference_requests) as f:
        # Opens the `reference_requests` file in read mode.
        reference_requests = json.load(f)
        # Loads the JSON data from the file into a Python object (e.g., a list of dictionaries).

    with open(downloaded_requests) as f:
        # Opens the `downloaded_requests` file in read mode.
        downloaded_requests = json.load(f)
        # Loads the JSON data from the file into a Python object (e.g., a list of dictionaries).

    full_results = {r['request_id']: {'expected': r} for r in reference_requests}
    # Creates a dictionary named `full_results` where each key is a `request_id` from `reference_requests`.
    # Each value is a dictionary containing the expected request data under the key 'expected'.

    reference_data = {r['request_id']: r['expected'] for r in reference_requests}
    # Creates a dictionary named `reference_data` where each key is a `request_id` from `reference_requests`.
    # Each value is the 'expected' data from the corresponding request.

    downloaded_data = {}
    # Initializes an empty dictionary named `downloaded_data` to store processed downloaded requests.

    for dr in downloaded_requests:
        # Iterates over each downloaded request in `downloaded_requests`.

        req_id = dr['RequestId']
        # Extracts the 'RequestId' from the current downloaded request.

        response = dr['VinsResponse']
        # Extracts the 'VinsResponse' from the current downloaded request.

        extra = {
            'setrace_url': dr['SetraceUrl'],
            'session_id': dr['SessionId'],
            'session_sequence': dr['SessionSequence'],
        }
        # Creates a dictionary named `extra` to store additional metadata from the downloaded request.

        compare_data, response = parse_comparable_data(response)
        # Parses the 'VinsResponse' using the `parse_comparable_data` function.
        # Returns:
        # - `compare_data`: A dictionary containing parsed intent and directives.
        # - `response`: The original response data.

        if compare_data is None:
            # Checks if `compare_data` is `None` (indicating no data was recognized).
            extra['message'] = 'Nothing has been recognised, Vins response missed'
            # Adds an error message to the `extra` dictionary.

        full_results[req_id]['downloaded'] = response
        # Adds the downloaded response data to the `full_results` dictionary under the current `req_id`.

        downloaded_data[req_id] = {
            'downloaded': compare_data,
            'extra': extra,
        }
        # Adds the parsed `compare_data` and `extra` metadata to the `downloaded_data` dictionary under the current `req_id`.

    with tempfile.NamedTemporaryFile(delete=False, mode='wt') as full_results_output:
        # Creates a temporary file to store the `full_results` data.
        json.dump(full_results, full_results_output, sort_keys=True, ensure_ascii=False)
        # Writes the `full_results` dictionary to the temporary file in JSON format.

    diff, missed = create_diff(reference_data, downloaded_data)
    # Calls the `create_diff` function to compare `reference_data` and `downloaded_data`.
    # Returns:
    # - `diff`: A dictionary of entries where the reference and downloaded data differ.
    # - `missed`: A dictionary of entries that are missing in the downloaded data.

    with tempfile.NamedTemporaryFile(delete=False, mode='wt') as diff_output:
        # Creates a temporary file to store the `diff` data.
        json.dump(diff, diff_output, sort_keys=True, ensure_ascii=False)
        # Writes the `diff` dictionary to the temporary file in JSON format.

    with tempfile.NamedTemporaryFile(delete=False, mode='wt') as missed_output:
        # Creates a temporary file to store the `missed` data.
        json.dump(missed, missed_output, sort_keys=True, ensure_ascii=False)
        # Writes the `missed` dictionary to the temporary file in JSON format.

    fails_quota = math.ceil(len(reference_requests) * 0.01)
    # Calculates the maximum allowed number of missed requests as 1% of the total reference requests.
    # Uses `math.ceil` to round up to the nearest integer.

    fail_flag = False
    # Initializes `fail_flag` to `False`.

    if diff or len(missed) > fails_quota:
        # Checks if there are any differences (`diff`) or if the number of missed requests exceeds the quota.
        fail_flag = True
        # Sets `fail_flag` to `True` if either condition is met.

    return (diff_output.name, missed_output.name, full_results_output.name, fail_flag)
    # Returns a tuple containing:
    # - The path to the temporary file storing the `diff` data.
    # - The path to the temporary file storing the `missed` data.
    # - The path to the temporary file storing the `full_results` data.
    # - The `fail_flag` indicating whether the test failed.

@vh.lazy(bool, fail_flag=bool)
# Decorates the `assert_test_result` function with `vh.lazy`, indicating it is a lazy-evaluated function.
# Specifies that the function takes a boolean input (`fail_flag`) and returns a boolean.

def assert_test_result(fail_flag):
    # Defines a function named `assert_test_result` that asserts whether the test results passed or failed.
    # The function takes one argument:
    # - `fail_flag`: A boolean indicating whether the test failed.

    assert not fail_flag, 'Test results failed, see diff in "compare_results" cube :)'
    # Asserts that `fail_flag` is `False`. If `fail_flag` is `True`, raises an `AssertionError` with a message.

    return fail_flag
    # Returns the `fail_flag` value.
```
