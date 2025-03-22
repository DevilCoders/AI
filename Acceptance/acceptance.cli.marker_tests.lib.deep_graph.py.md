```python
# coding: utf-8
# Specifies the encoding of the file as UTF-8 to ensure proper handling of Unicode characters.

import json
# Imports the `json` module, which provides functions to work with JSON data (e.g., parsing and serializing).

import vh
# Imports the `vh` module, which is likely a custom or third-party module for handling data or virtual files.

from alice.acceptance.cli.marker_tests.lib import common
# Imports the `common` module from the `alice.acceptance.cli.marker_tests.lib` package.
# This module likely contains shared utilities or functions for the marker tests.

from alice.acceptance.cli.marker_tests.lib import lazy_helpers
# Imports the `lazy_helpers` module from the `alice.acceptance.cli.marker_tests.lib` package.
# This module likely contains helper functions for lazy evaluation or comparison of test results.

from alice.acceptance.cli.marker_tests.lib import op
# Imports the `op` module from the `alice.acceptance.cli.marker_tests.lib` package.
# This module likely contains operations or functions for processing data or performing tasks.

from library.python import resource
# Imports the `resource` module from the `library.python` package.
# This is likely a custom or third-party module for resource management.

def compare_and_assert(requests_vh_table, reference_requests, global_options):
    # Defines a function named `compare_and_assert` that compares actual requests with reference requests and asserts the result.
    # The function takes three arguments:
    # - `requests_vh_table`: A table or dataset containing actual requests.
    # - `reference_requests`: A list or dataset containing reference requests for comparison.
    # - `global_options`: An object or dictionary containing global configuration options (e.g., YT token).

    actual_requests = op.MR_TABLE_TO_JSON_OP(
        # Calls the `MR_TABLE_TO_JSON_OP` function from the `op` module to convert the `requests_vh_table` into JSON format.
        # This function likely processes a MapReduce table and converts it into a JSON-compatible structure.

        _inputs={
            'table': requests_vh_table,
            # Specifies the input table (`requests_vh_table`) to be processed.
        },
        _options={
            'yt-token': global_options.yt_token,
            # Provides the YT token from `global_options` for authentication or access to YT services.
            'output-columns': ['VinsResponse', 'RequestId', 'SetraceUrl', 'SessionId', 'SessionSequence']
            # Specifies the columns to include in the output JSON.
        },
    )

    reference_requests_data = vh.data_from_str(
        # Calls the `data_from_str` function from the `vh` module to create a virtual data object from the `reference_requests`.
        # This function likely converts the reference requests into a format suitable for comparison.

        json.dumps(reference_requests).encode('utf-8'),
        # Converts the `reference_requests` into a JSON string and encodes it as UTF-8 bytes.
        name='marker tests context data',
        # Assigns a name to the virtual data object for identification.
        data_type='json',
        # Specifies that the data type is JSON.
    )

    (_, _, _, fail_flag) = lazy_helpers.compare_results(reference_requests_data, actual_requests)
    # Calls the `compare_results` function from the `lazy_helpers` module to compare the `reference_requests_data` and `actual_requests`.
    # The function returns a tuple, and the fourth element (`fail_flag`) indicates whether the comparison failed.

    lazy_helpers.assert_test_result(fail_flag)
    # Calls the `assert_test_result` function from the `lazy_helpers` module to assert the test result based on the `fail_flag`.
    # If `fail_flag` indicates a failure, this function will raise an assertion error.
```

```python
def build_common_subgraph(data_dir, global_options, config, use_linked_resources):
    # Defines a function named `build_common_subgraph` that builds a common subgraph for marker tests.
    # The function takes four arguments:
    # - `data_dir`: The directory containing test data files.
    # - `global_options`: An object or dictionary containing global configuration options.
    # - `config`: An object or dictionary containing configuration settings (e.g., YT proxy).
    # - `use_linked_resources`: A boolean flag indicating whether to use linked resources or local files.

    all_requests = []
    # Initializes an empty list named `all_requests` to store all processed test requests.

    if use_linked_resources:
        # Checks if the `use_linked_resources` flag is `True`.

        for test_json_request in common.concat_json_files_from_resources(resource.iterkeys('/marker_tests/data')):
            # Iterates over JSON files loaded from linked resources using `resource.iterkeys`.
            # `concat_json_files_from_resources` concatenates the contents of these JSON files.

            all_requests.extend(common.compose_context_request(test_json_request))
            # Processes each JSON request using `compose_context_request` and adds the results to `all_requests`.

    else:
        # If `use_linked_resources` is `False`, this block executes.

        for test_json_request in common.concat_json_files(common.all_json_files(data_dir)):
            # Iterates over JSON files found in the specified `data_dir` using `all_json_files`.
            # `concat_json_files` concatenates the contents of these JSON files.

            all_requests.extend(common.compose_context_request(test_json_request))
            # Processes each JSON request using `compose_context_request` and adds the results to `all_requests`.

    json_out = vh.data_from_str(
        # Calls the `data_from_str` function from the `vh` module to create a virtual data object from `all_requests`.
        # This function likely converts the list of requests into a format suitable for further processing.

        json.dumps(all_requests).encode('utf-8'),
        # Converts the `all_requests` list into a JSON string and encodes it as UTF-8 bytes.
        name='marker tests data',
        # Assigns a name to the virtual data object for identification.
        data_type='json',
        # Specifies that the data type is JSON.
    )

    cache_sync_out = op.SINGLE_OPTION_TO_JSON(
        # Calls the `SINGLE_OPTION_TO_JSON` function from the `op` module to convert a single option into JSON format.
        # This function likely processes a configuration option for cache synchronization.

        _options={'input': vh.OptionExpr('{"timestamp": "${global.cache_sync}"}')}
        # Specifies the input option as a JSON string with a placeholder for the cache sync timestamp.
    )['output']
    # Extracts the `output` field from the result of the `SINGLE_OPTION_TO_JSON` function.

    input_table = op.JSON_TO_MR_TABLE_OP(
        # Calls the `JSON_TO_MR_TABLE_OP` function from the `op` module to convert the JSON data into a MapReduce table.
        # This function likely processes the JSON data and prepares it for MapReduce operations.

        _inputs={
            'json': json_out,
            # Specifies the JSON data (`json_out`) as the input to be processed.
        },
        _options={
            'yt-token': global_options.yt_token,
            # Provides the YT token from `global_options` for authentication or access to YT services.
            'mr-account': global_options.mr_account,
            # Specifies the MapReduce account from `global_options`.
            'mr-default-cluster': config.yt.proxy,  # global_options.yt_proxy, https://paste.yandex-team.ru/899252
            # Specifies the default MapReduce cluster using the YT proxy from `config`.
            'mr-output-ttl': global_options.mr_output_ttl,
            # Specifies the TTL (Time to Live) for the MapReduce output from `global_options`.
        },
        _dynamic_options=cache_sync_out,
        # Provides the cache sync output as dynamic options for the MapReduce operation.
    )['new_table']
    # Extracts the `new_table` field from the result of the `JSON_TO_MR_TABLE_OP` function.

    return (all_requests, input_table)
    # Returns a tuple containing:
    # - `all_requests`: The list of all processed test requests.
    # - `input_table`: The MapReduce table created from the JSON data.
```

```python
def build_graph_with_scraper(data_dir, global_options, config, use_linked_resources, scraper_mode):
    # Defines a function named `build_graph_with_scraper` that builds a graph for marker tests using a scraper.
    # The function takes five arguments:
    # - `data_dir`: The directory containing test data files.
    # - `global_options`: An object or dictionary containing global configuration options.
    # - `config`: An object or dictionary containing configuration settings (e.g., YT proxy, scraper settings).
    # - `use_linked_resources`: A boolean flag indicating whether to use linked resources or local files.
    # - `scraper_mode`: A string indicating the scraper mode (e.g., 'test' or 'soy_test').

    all_requests, input_table = build_common_subgraph(data_dir, global_options, config, use_linked_resources)
    # Calls the `build_common_subgraph` function to process test data and build a common subgraph.
    # Returns:
    # - `all_requests`: A list of all processed test requests.
    # - `input_table`: A MapReduce table containing the processed data.

    downloaded_results = op.DEEP_DOWNLOADER_OP(
        # Calls the `DEEP_DOWNLOADER_OP` function from the `op` module to download results using a scraper.
        # This function likely performs deep downloading of data from specified URLs.

        _inputs={
            'input': input_table,
            # Specifies the input table (`input_table`) to be processed by the scraper.
        },
        _options={
            'VinsUrl': global_options.vins_url,
            # Specifies the Vins URL from `global_options` for the scraper.
            'UniproxyUrl': global_options.uniproxy_url,
            # Specifies the Uniproxy URL from `global_options` for the scraper.
            'uniproxy-fetcher-mode': 'auto',
            # Sets the Uniproxy fetcher mode to 'auto'.
            'oauth': global_options.ya_plus_token,
            # Provides the OAuth token from `global_options` for authentication.
            'yt-token': global_options.yt_token,
            # Provides the YT token from `global_options` for YT access.
            'yql-token': global_options.yql_token,
            # Provides the YQL token from `global_options` for YQL access.
            'arcanum_token': global_options.arcanum_token,
            # Provides the Arcanum token from `global_options` for Arcanum access.
            'input_cluster': config.yt.proxy,
            # Specifies the input cluster using the YT proxy from `config`.
            'mr-account': global_options.mr_account,
            # Specifies the MapReduce account from `global_options`.
            'mr-output-ttl': global_options.mr_output_ttl,
            # Specifies the TTL (Time to Live) for the MapReduce output from `global_options`.
            'mr-output-path': global_options.mr_output_path,
            # Specifies the output path for the MapReduce results from `global_options`.
            'yt-pool': global_options.yt_pool,
            # Specifies the YT pool from `global_options`.
            'cache_sync': global_options.cache_sync,
            # Specifies the cache sync setting from `global_options`.
            'AsrChunkSize': config.alice.asr_chunk_size,
            # Specifies the ASR (Automatic Speech Recognition) chunk size from `config`.
            'scraper-timeout': config.alice.scraper_timeout,
            # Specifies the scraper timeout setting from `config`.
            'ScraperOverYtPool': config.alice.scraper_pool,
            # Specifies the scraper pool setting from `config`.
            'experiments': common.prepare_experiments(config.alice.experiments),
            # Prepares and specifies the experiments configuration from `config`.
            'Scraper-token': config.soy.token,
            # Specifies the scraper token from `config`.
            'Scraper-contour': {'test': '6', 'soy_test': '2'}.get(scraper_mode),
            # Specifies the scraper contour based on the `scraper_mode` argument.
            # Maps 'test' to '6' and 'soy_test' to '2'.
        },
    )

    uniproxy_out = downloaded_results['output']
    # Extracts the `output` field from the result of the `DEEP_DOWNLOADER_OP` function.
    # This contains the downloaded results from the scraper.

    compare_and_assert(uniproxy_out, all_requests, global_options)
    # Calls the `compare_and_assert` function to compare the downloaded results (`uniproxy_out`) with the expected results (`all_requests`).
    # Asserts that the results match, raising an error if they do not.
```

```python
def build_graph(data_dir, global_options, config, use_linked_resources, scraper_mode):
    # Defines a function named `build_graph` that builds a graph for marker tests.
    # The function takes five arguments:
    # - `data_dir`: The directory containing test data files.
    # - `global_options`: An object or dictionary containing global configuration options.
    # - `config`: An object or dictionary containing configuration settings (e.g., YT proxy, scraper settings).
    # - `use_linked_resources`: A boolean flag indicating whether to use linked resources or local files.
    # - `scraper_mode`: A string indicating the scraper mode (e.g., 'test' or 'soy_test').

    build_graph_with_scraper(data_dir, global_options, config, use_linked_resources, scraper_mode)
    # Calls the `build_graph_with_scraper` function to build the graph using a scraper.
    # This function handles the entire process of building the graph, including downloading and comparing results.
```
