```sql
-- Set the maximum row weight to 64MB to handle large data rows
PRAGMA yt.MaxRowWeight = "64M";

-- Enable ANSI-style handling for "IN" clauses with empty or nullable collections
PRAGMA AnsiInForEmptyOrNullableItemsCollections;

-- Define input tables for raw logs
$raw_success = {{input1->table_quote()}};  -- Table containing successfully processed logs
$raw_errors = {{input2->table_quote()}};   -- Table containing logs with errors

-- Define output tables for parsed and processed data
$unpacked_success = {{output1->table_quote()}};  -- Table for parsed successful logs
$unpacked_errors = {{output2->table_quote()}};   -- Table for parsed error logs
$error_stat = {{output3->table_quote()}};        -- Table for computed error statistics

-- Configuration for parsing Protobuf messages
$config = AsAtom(@@{...}@@);
$udf = YQL::Udf(AsAtom("Protobuf.Parse"), YQL::Void(), YQL::Void(), $config);

-- Define a subquery to unpack Protobuf messages
DEFINE SUBQUERY $unpack_proto($input) AS
    SELECT *
    FROM (
        SELECT Error AS FetchedError, $udf(FetchedResult) AS Packed
        FROM concat($input)  -- Concatenate all input rows
        WITH SCHEMA Struct<FetchedResult:String?, UsedBetas:String?, Error:String?>
    ) FLATTEN COLUMNS;  -- Flatten the result structure
END DEFINE;

-- Parse and store successful logs
INSERT INTO $unpacked_success WITH TRUNCATE
SELECT * FROM $unpack_proto($raw_success);

-- Parse and store error logs
INSERT INTO $unpacked_errors WITH TRUNCATE
SELECT * FROM $unpack_proto($raw_errors);
COMMIT;

-- Python code to classify and categorize errors
$code = @@
import collections
import json
import re
import cyson  # Import a custom parser for structured logs

def get_source_error_type(VinsResponse):
    """Extract error type from VinsResponse JSON field."""
    try:
        vins = VinsResponse
        if vins is not None:
            meta = json.loads(vins)['directive']['payload']['response'].get('meta', [])
            for meta_item in meta:
                if meta_item['type'] == 'error':
                    return 'vins_sources_error_' + meta_item['error_type']
    except (KeyError, ValueError) as e:
        return 'vins_sources_error_traceback'

def get_error_type(error):
    """Classify errors based on predefined patterns."""
    if not error:
        return None
    error = error.decode('utf-8')
    modified_error = re.sub('[a-f0-9]{1,8}-[a-f0-9]{1,8}-[a-f0-9]{1,8}-[a-f0-9]{1,8}', 'MESSAGEID', error)
    modified_error = re.sub('cpp:[0-9]+', 'cpp:#', modified_error)
    for (key, value) in [
        ('(NAlice::NUniproxy::NHelpers::TUniproxyInteractionError)', 'uniproxy_error'),
        ('(Poco::Net::NoMessageException)', 'uniproxy_error'),
        ('(NScraperOverYT::TBinaryHolderFail)', 'downloader_error'),
        ('(NScraperOverYT::TWebUnanswerFail)', 'tunneler_error'),
    ]:
        if modified_error.startswith(key):
            return modified_error.replace(key, value)
    return 'unknown_error_' + modified_error.replace(' ', '_')

def get_error_group(error):
    """Extract error category from raw error message."""
    if not error:
        return None
    error = error.decode('utf-8')
    return error[:error.index('error')] + 'error'
@@;

-- Register Python functions as YQL UDFs
$get_source_error_type = Python3::get_source_error_type(Callable<(String?) -> String?>, $code);
$get_error_type = Python3::get_error_type(Callable<(String?) -> String>, $code);
$get_error_group = Python3::get_error_group(Callable<(String?) -> String?>, $code);

-- Extract and classify errors into the selected error table
INSERT INTO @selected_errors
SELECT
    $get_source_error_type(VinsResponse) AS metric,
    $get_error_group($get_source_error_type(VinsResponse)) AS `group`,
    SetraceUrl AS setrace_url,
    Basket AS basket
FROM $unpacked_success
UNION ALL
SELECT
    $get_error_type(FetchedError) AS metric,
    $get_error_group($get_error_type(FetchedError)) AS `group`,
    SetraceUrl AS setrace_url,
    Basket AS basket
FROM $unpacked_errors;
COMMIT;

-- Define a subquery to calculate error percentage per basket
DEFINE SUBQUERY $group_percent($group_name) AS
SELECT
    basket,
    'download_error_percent' AS `group`,
    $group_name AS metric,
    1.0 * COUNT_IF(group == $group_name AND metric IS NOT NULL) / COUNT(*) AS value
FROM @selected_errors
GROUP BY basket;
END DEFINE;

-- Define a subquery to count absolute occurrences of each error per basket
DEFINE SUBQUERY $group_absolute($group_name) AS
SELECT
    basket,
    'download_error_absolute' AS `group`,
    $group_name AS metric,
    COUNT_IF(group == $group_name AND metric IS NOT NULL) AS value
FROM @selected_errors
GROUP BY basket;
END DEFINE;

-- Define error categories for statistics calculation
$download_groups = ['downloader_error', 'mm_unanswer_error', 'uniproxy_error', 'tunneler_error', 'unknown_error'];

-- Insert computed error statistics into the final table
INSERT INTO $error_stat WITH TRUNCATE
SELECT * FROM $group_percent('downloader_error')
UNION ALL
SELECT * FROM $group_absolute('downloader_error')
UNION ALL
SELECT * FROM $group_percent('mm_unanswer_error')
UNION ALL
SELECT * FROM $group_absolute('mm_unanswer_error')
UNION ALL
SELECT * FROM $group_percent('uniproxy_error')
UNION ALL
SELECT * FROM $group_absolute('uniproxy_error')
UNION ALL
SELECT * FROM $group_percent('tunneler_error')
UNION ALL
SELECT * FROM $group_absolute('tunneler_error')
UNION ALL
SELECT * FROM $group_percent('unknown_error')
UNION ALL
SELECT * FROM $group_absolute('unknown_error')
UNION ALL
-- Compute additional error details with top Setrace URLs
SELECT basket, 'download_error_details' AS `group`, metric, COUNT(*) as value,
    Yson::From(AsDict(AsTuple(
        'setrace_urls',
        TOP_BY(setrace_url, Random(setrace_url), 10)
    ))) AS additional_info
FROM @selected_errors
GROUP BY basket, metric
HAVING metric IS NOT NULL;
```
