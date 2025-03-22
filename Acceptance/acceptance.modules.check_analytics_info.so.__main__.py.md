```python
import click
# Imports the `click` module, which provides a framework for creating command-line interfaces.

import yt.wrapper as yt
# Imports the `yt.wrapper` module, which provides utilities for working with YT (Yandex Table).

from nile.api.v1 import (
    clusters,
    Record
)
# Imports the `clusters` and `Record` classes from the `nile.api.v1` module.
# - `clusters`: Provides access to YT clusters.
# - `Record`: Represents a single row of data in a table.

from qb2.api.v1 import typing
# Imports the `typing` module from `qb2.api.v1`, which provides type annotations for schema definitions.

from alice.acceptance.modules.check_analytics_info.lib.checkers import (
    MegamindAnalyticsInfoChecker,
    TunnellerChecker,
    MetaChecker
)
# Imports the checker classes (`MegamindAnalyticsInfoChecker`, `TunnellerChecker`, `MetaChecker`) from the `checkers` module.

schema_diff_table = {
    'RequestId': typing.Optional[typing.String],
    'stable.VinsResponse': typing.Optional[typing.String],
    'test.VinsResponse': typing.Optional[typing.String],
}
# Defines the schema for the `diff_table`, which includes optional fields for `RequestId`, `stable.VinsResponse`, and `test.VinsResponse`.

SCHEMA_RESULT_TABLE = {
    'description': typing.Optional[typing.String],
    'message': typing.Optional[typing.String],
    'name': typing.Optional[typing.String],
    'verdict': bool
}
# Defines the schema for the `result_table`, which includes optional fields for `description`, `message`, and `name`, and a required boolean field for `verdict`.

@click.command()
# Decorates the `main` function as a Click command-line interface command.

@click.option('--input-table')
# Adds a command-line option `--input-table` to specify the input table path.

@click.option('--result-table')
# Adds a command-line option `--result-table` to specify the result table path.

@click.option('--diff-table')
# Adds a command-line option `--diff-table` to specify the diff table path.

@click.option('--yql-token')
# Adds a command-line option `--yql-token` to specify the YQL token for authentication.

def main(input_table, result_table, diff_table, yql_token):
    # Defines the `main` function, which is the entry point of the script.
    # The function takes four arguments:
    # - `input_table`: The path to the input table.
    # - `result_table`: The path to the result table.
    # - `diff_table`: The path to the diff table.
    # - `yql_token`: The YQL token for authentication.

    cluster = clusters.yql.Hahn(yql_token=yql_token)
    # Creates a YQL cluster instance for the `hahn` cluster using the provided YQL token.

    yt.config.config['proxy']['url'] = 'hahn'
    # Configures the YT proxy URL to 'hahn'.

    job = cluster.job()
    # Creates a job instance for the cluster.

    checkers = [
        MegamindAnalyticsInfoChecker(),
        TunnellerChecker(),
        MetaChecker()
    ]
    # Initializes a list of checker instances (`MegamindAnalyticsInfoChecker`, `TunnellerChecker`, `MetaChecker`).

    diff_rows = []
    # Initializes an empty list named `diff_rows` to store processed rows.

    for rec in job.table(input_table).read():
        # Iterates over each row in the input table.

        d = rec.to_dict()
        # Converts the row (a `Record` object) into a dictionary.

        for checker in checkers:
            # Iterates over each checker in the `checkers` list.

            verdict, message = checker.process_row(d)
            # Processes the row using the `process_row` method of the checker.
            # Returns a tuple containing:
            # - `verdict`: A boolean indicating whether the row is valid.
            # - `message`: A descriptive message if the row is invalid.

            verdict_col = '{}_verdict'.format(checker.NAME)
            # Generates a column name for the verdict (e.g., `megamind_analytics_info_checker_verdict`).

            message_col = '{}_message'.format(checker.NAME)
            # Generates a column name for the message (e.g., `megamind_analytics_info_checker_message`).

            d[verdict_col] = verdict
            # Adds the verdict to the dictionary under the generated column name.

            d[message_col] = message
            # Adds the message to the dictionary under the generated column name.

            schema_diff_table[verdict_col] = bool
            # Adds the verdict column to the `schema_diff_table` schema with a boolean type.

            schema_diff_table[message_col] = typing.Optional[typing.String]
            # Adds the message column to the `schema_diff_table` schema with an optional string type.

        diff_rows.append(Record.from_dict(d))
        # Converts the dictionary back into a `Record` object and appends it to the `diff_rows` list.

    if yt.exists(diff_table):
        # Checks if the `diff_table` already exists in YT.
        yt.remove(diff_table)
        # Removes the existing `diff_table`.

    if yt.exists(result_table):
        # Checks if the `result_table` already exists in YT.
        yt.remove(result_table)
        # Removes the existing `result_table`.

    cluster.write(diff_table, diff_rows, schema=schema_diff_table)
    # Writes the `diff_rows` list to the `diff_table` using the `schema_diff_table` schema.

    results = (Record.from_dict(checker.dump_result()) for checker in checkers)
    # Generates a list of `Record` objects from the `dump_result` method of each checker.

    cluster.write(result_table, results, schema=SCHEMA_RESULT_TABLE)
    # Writes the `results` list to the `result_table` using the `SCHEMA_RESULT_TABLE` schema.

    job.run()
    # Runs the job to execute the operations.

    assert all(r['verdict'] for r in results), 'analytics_info check failed'
    # Asserts that all results have a `verdict` of `True`. If any result has a `verdict` of `False`, raises an `AssertionError`.


if __name__ == '__main__':
    # Checks if the script is being run directly (not imported as a module).
    main()
    # Calls the `main` function to execute the script.
```
