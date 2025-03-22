```python
# Import the 'vh' module, which is likely a framework for defining and executing data pipelines.
import vh

# Import specific operations from the 'alice.acceptance.runners.common_operations' module.
# These operations are used to build the pipeline.
from alice.acceptance.runners.common_operations import (
    build_arcadia_project_op,  # Operation to build Arcadia projects.
    get_mr_table_op,           # Operation to retrieve MR (MapReduce) tables.
    ue2e_downloader_op,        # Operation to download data for end-to-end testing.
    yql_2_op                   # Operation to execute YQL (Yandex Query Language) queries.
)

# Import global configuration options from the 'alice.acceptance.runners.config' module.
from alice.acceptance.runners.config import global_options

# Define a custom operation with a unique ID for checking analytics info.
check_analytics_info_op = vh.op(id='9d3bd383-2873-437d-9044-5a67abd7dd98')

# Define a constant for the TTL (Time-To-Live) of MR (MapReduce) output tables.
MR_OUTPUT_TTL = 10

# Define a YQL query to concatenate successful responses and valid error responses.
# This query filters valid errors and combines them with successful responses.
YQL_CONCAT_SUCC_AND_VALID_ERROR_RESPONSES = '''$good_error_responses = (
SELECT
    *
FROM
    {{input2}}
WHERE
    FetchedError LIKE '%Retries for tunneller validation are over.%'
);

$good_with_good_error_responses = (
SELECT
    *
FROM (
        SELECT
            *
        FROM
            {{input1}}
    UNION ALL
        SELECT
            *
        FROM
            $good_error_responses
)
);

INSERT INTO {{output1}}
    SELECT
        *
    FROM $good_with_good_error_responses;

$script = @@
from yql.typing import *

def assert_ratio(
    good: Optional[Uint64],
    bad: Optional[Uint64]) -> Bool:
    MAX_ERROR_SHARE = 0.005
    value = bad / (bad + good) < MAX_ERROR_SHARE
    assert value
    return value
@@;

$assert_ratio = Python3::assert_ratio($script);

$bad = (
SELECT
        *
    FROM
        {{input2}} AS errors
    LEFT ONLY JOIN
        $good_error_responses AS good_errors
    USING
        (RequestId)
);

$good_count = SELECT COUNT(*) FROM $good_with_good_error_responses;
$bad_count = SELECT COUNT(*) FROM $bad;

SELECT
    $assert_ratio(
        $good_count,
        $bad_count
    )
'''


# Define the main function to build the data processing pipeline.
def build_graph(config, _after=None):
    # Build the 'run_python_udf' binary from the Arcadia project.
    run_python_udf_bin = build_arcadia_project_op(
        _name='build run python udf',  # Name of the operation.
        _options={
            'arcadia_url': 'arcadia:/arc/trunk/arcadia',  # URL of the Arcadia repository.
            'arcadia_revision': config.check_analytics_info.revision,  # Revision of the Arcadia project.
            'build_type': 'release',  # Type of build (release or debug).
            'targets': 'yql/tools/run_python_udf',  # Target to build.
            'arts': 'yql/tools/run_python_udf/run_python_udf',  # Output artifact.
        },
    )

    # Build the 'check_analytics_info' shared object (SO) from the Arcadia project.
    check_analytics_info_so = build_arcadia_project_op(
        _name='build checker analytics_info',  # Name of the operation.
        _options={
            'arcadia_url': 'arcadia:/arc/trunk/arcadia',  # URL of the Arcadia repository.
            'arcadia_revision': config.check_analytics_info.revision,  # Revision of the Arcadia project.
            'build_type': 'release',  # Type of build (release or debug).
            'targets': 'alice/acceptance/modules/check_analytics_info/so',  # Target to build.
            'arts': 'alice/acceptance/modules/check_analytics_info/so/libcheck_analytics_info.so',  # Output artifact.
        },
    )

    # Retrieve the input table for the pipeline.
    input_table = get_mr_table_op(
        _name='get input table',  # Name of the operation.
        _options={
            'cluster': config.yt.proxy,  # YT (Yandex Table) cluster to use.
            'creationMode': 'NO_CHECK',  # Mode for table creation.
            'table': config.check_analytics_info.input_table,  # Input table name.
            'yt-token': vh.get_yt_token_secret(),  # YT token for authentication.
        },
    )

    # Download test data using the 'ue2e_downloader_op' operation.
    downloader_test_table = ue2e_downloader_op(
        _name='test downloader',  # Name of the operation.
        _inputs={
            'evaluation_set': input_table['outTable'],  # Input table for evaluation.
        },
        _options={
            'uniproxy_url': config.check_analytics_info.uniproxy_url,  # URL of the uniproxy service.
            'vins_url': config.check_analytics_info.test_vins_url,  # URL of the test VINS service.
            'oauth': global_options.ya_plus_token,  # OAuth token for authentication.
            'arcanum_token': config.alice_common.arcanum_robot_token,  # Arcanum token for authentication.
            'yt-token': vh.get_yt_token_secret(),  # YT token for authentication.
            'yql-token': global_options.yql_token,  # YQL token for authentication.
            'Scraper-token': global_options.soy_token,  # Scraper token for authentication.
            'input_cluster': config.yt.proxy,  # YT cluster for input data.
            'ScraperOverYtPool': config.alice_common.scraper_over_yt_pool,  # Scraper pool for YT.
            'mr-account': vh.get_mr_account(),  # MR account for MapReduce jobs.
            'experiments': config.check_analytics_info.experiments,  # Experiments to enable.
            'mr-output-ttl': MR_OUTPUT_TTL,  # TTL for MR output tables.
            'cache_sync': global_options.cache_sync,  # Cache synchronization settings.
            'retry-profile': 'no_retry',  # Retry profile for the operation.
        },
    )

    # Download stable data using the 'ue2e_downloader_op' operation.
    downloader_stable_table = ue2e_downloader_op(
        _name='stable downloader',  # Name of the operation.
        _inputs={
            'evaluation_set': input_table['outTable'],  # Input table for evaluation.
        },
        _options={
            'uniproxy_url': config.check_analytics_info.uniproxy_url,  # URL of the uniproxy service.
            'vins_url': config.check_analytics_info.stable_vins_url,  # URL of the stable VINS service.
            'oauth': global_options.ya_plus_token,  # OAuth token for authentication.
            'arcanum_token': config.alice_common.arcanum_robot_token,  # Arcanum token for authentication.
            'yt-token': vh.get_yt_token_secret(),  # YT token for authentication.
            'yql-token': global_options.yql_token,  # YQL token for authentication.
            'Scraper-token': global_options.soy_token,  # Scraper token for authentication.
            'input_cluster': config.yt.proxy,  # YT cluster for input data.
            'ScraperOverYtPool': config.alice_common.scraper_over_yt_pool,  # Scraper pool for YT.
            'mr-account': vh.get_mr_account(),  # MR account for MapReduce jobs.
            'experiments': config.check_analytics_info.experiments,  # Experiments to enable.
            'mr-output-ttl': MR_OUTPUT_TTL,  # TTL for MR output tables.
            'cache_sync': global_options.cache_sync,  # Cache synchronization settings.
            'retry-profile': 'no_retry',  # Retry profile for the operation.
        },
    )

    # Concatenate successful and valid error responses for the test data.
    concat_test_table = yql_2_op(
        _name='concat test successful and valid error responses',  # Name of the operation.
        _inputs={
            'input1': downloader_test_table['downloader_results'],  # Successful responses.
            'input2': downloader_test_table['downloader_errors'],  # Error responses.
        },
        _options={
            'request': YQL_CONCAT_SUCC_AND_VALID_ERROR_RESPONSES,  # YQL query to execute.
            'py_version': 'Python2',  # Python version for UDFs (User-Defined Functions).
            'syntax_version': 'v1',  # Syntax version for YQL.
            'mr-default-cluster': config.yt.proxy,  # Default YT cluster for MR jobs.
            'mr-account': vh.get_mr_account(),  # MR account for MapReduce jobs.
            'yt-token': vh.get_yt_token_secret(),  # YT token for authentication.
            'yql-token': global_options.yql_token,  # YQL token for authentication.
            'mr-output-ttl': MR_OUTPUT_TTL,  # TTL for MR output tables.
        },
    )

    # Concatenate successful and valid error responses for the stable data.
    concat_stable_table = yql_2_op(
        _name='concat stable successful and valid error responses',  # Name of the operation.
        _inputs={
            'input1': downloader_stable_table['downloader_results'],  # Successful responses.
            'input2': downloader_stable_table['downloader_errors'],  # Error responses.
        },
        _options={
            'request': YQL_CONCAT_SUCC_AND_VALID_ERROR_RESPONSES,  # YQL query to execute.
            'py_version': 'Python2',  # Python version for UDFs.
            'syntax_version': 'v1',  # Syntax version for YQL.
            'mr-default-cluster': config.yt.proxy,  # Default YT cluster for MR jobs.
            'mr-account': vh.get_mr_account(),  # MR account for MapReduce jobs.
            'yt-token': vh.get_yt_token_secret(),  # YT token for authentication.
            'yql-token': global_options.yql_token,  # YQL token for authentication.
            'mr-output-ttl': MR_OUTPUT_TTL,  # TTL for MR output tables.
        },
    )

    # Join the test and stable responses into a single table.
    joined_test_and_stable_table = yql_2_op(
        _name='join test and stable responses',  # Name of the operation.
        _inputs={
            'input1': concat_test_table['output1'],  # Test responses.
            'input2': concat_stable_table['output1'],  # Stable responses.
        },
        _options={
            'request': '''INSERT INTO {{output1}}
    SELECT test.RequestId AS RequestId, test.VinsResponse, stable.VinsResponse
        FROM {{input1}} AS test
    FULL JOIN
        {{input2}} AS stable
    USING (RequestId)''',  # YQL query to join tables.
            'py_version': 'Python2',  # Python version for UDFs.
            'syntax_version': 'v1',  # Syntax version for YQL.
            'mr-default-cluster': config.yt.proxy,  # Default YT cluster for MR jobs.
            'mr-account': vh.get_mr_account(),  # MR account for MapReduce jobs.
            'yt-token': vh.get_yt_token_secret(),  # YT token for authentication.
            'yql-token': global_options.yql_token,  # YQL token for authentication.
            'mr-output-ttl': MR_OUTPUT_TTL,  # TTL for MR output tables.
        },
    )

    # Execute the custom operation to check analytics info.
    check_analytics_info_op(
        _name='check analytics info',  # Name of the operation.
        _inputs={
            'input_table': joined_test_and_stable_table['output1'],  # Input table for checking.
            'runner': run_python_udf_bin['ARCADIA_PROJECT'],  # Binary for running Python UDFs.
            'so': check_analytics_info_so['ARCADIA_PROJECT'],  # Shared object for checking analytics.
        },
        _options={
            'yt-token': vh.get_yt_token_secret(),  # YT token for authentication.
            'mr-account': vh.get_mr_account(),  # MR account for MapReduce jobs.
            'max-ram': 2000,  # Maximum RAM for the operation.
            'yql-token': global_options.yql_token,  # YQL token for authentication.
        },
    )
```
