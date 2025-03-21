```python
# coding: utf-8  
# Specifies the encoding of the script as UTF-8.  
# This ensures that the script can handle non-ASCII characters.

import json  
# Imports the `json` module, which provides functions for working with JSON data.  
# This includes parsing JSON strings and converting Python objects to JSON.

import os  
# Imports the `os` module, which provides functions for interacting with the operating system.  
# This includes file and directory operations, environment variables, and more.

import subprocess  
# Imports the `subprocess` module, which allows the script to spawn new processes and interact with them.  
# This is useful for running external commands or scripts.

import uuid  
# Imports the `uuid` module, which provides functions for generating universally unique identifiers (UUIDs).  
# UUIDs are often used to create unique keys or identifiers.

import click  
# Imports the `click` library, which is used for creating command-line interfaces (CLIs).  
# It simplifies the process of defining and parsing command-line arguments and options.

from google.protobuf import json_format  
# Imports the `json_format` module from the `google.protobuf` package.  
# This module provides utilities for converting Protocol Buffers (protobuf) messages to and from JSON.

from library.python import resource  
# Imports the `resource` module from the `library.python` package.  
# This module is likely used for managing and accessing resources, such as configuration files or data.

import yt.wrapper as yt  
# Imports the `yt.wrapper` module and aliases it as `yt`.  
# This module is used for interacting with YT (Yandex.Tank or Yandex Table), a distributed data processing system.

from yt.wrapper import yson  
# Imports the `yson` module from `yt.wrapper`.  
# YSON is a data serialization format used by YT, similar to JSON.

from search.scraper_over_yt.mapper.lib.proto import voice_output_pb2  
# Imports the `voice_output_pb2` module from the `search.scraper_over_yt.mapper.lib.proto` package.  
# This module likely contains Protocol Buffers definitions for voice output data.

PRODUCTION_FLAGS = json.dumps(json.loads(resource.find('flags_production.json')))  
# Loads the contents of the `flags_production.json` resource file using the `resource.find` function.  
# The JSON data is parsed into a Python object using `json.loads`, then converted back to a JSON string using `json.dumps`.  
# The result is stored in the `PRODUCTION_FLAGS` variable.

def prepare_reducer(key, values):  
    # Defines a function named `prepare_reducer` that takes two arguments: `key` and `values`.  
    # This function is used to prepare data for a reduce operation in YT.

    values = list(values)  
    # Converts the `values` iterator into a list.  
    # This allows for sorting and other list operations.

    values.sort(key=lambda t: -t['session_sequence'])  
    # Sorts the `values` list in descending order based on the `session_sequence` field.  
    # The `lambda t: -t['session_sequence']` function extracts the `session_sequence` value and negates it for descending order.

    yield {'session_requests': values, 'session_id': key['session_id']}  
    # Yields a dictionary containing the sorted `values` and the `session_id` from the `key`.  
    # This dictionary represents the prepared data for the reduce operation.

def run_reduce(reducer, input_table, output_table, reduce_by):  
    # Defines a function named `run_reduce` that takes four arguments:  
    # - `reducer`: The reducer function to apply.  
    # - `input_table`: The input table in YT.  
    # - `output_table`: The output table in YT.  
    # - `reduce_by`: The fields to reduce by.

    with yt.TempTable() as sorted_table:  
        # Creates a temporary table in YT using `yt.TempTable()`.  
        # The temporary table is used to store intermediate results during the reduce operation.

        yt.run_sort(input_table, sorted_table, sort_by=reduce_by)  
        # Runs a sort operation on the `input_table` and stores the result in `sorted_table`.  
        # The `sort_by` parameter specifies the fields to sort by.

        yt.run_reduce(reducer, sorted_table, output_table, reduce_by=reduce_by)  
        # Runs a reduce operation on the `sorted_table` using the `reducer` function.  
        # The result is stored in the `output_table`.  
        # The `reduce_by` parameter specifies the fields to reduce by.
```

```python
def unpack_mapper(row):  
    # Defines a function named `unpack_mapper` that takes one argument: `row`.  
    # This function is used to unpack and process a row of data from a YT table.

    proto_content = yson.yson_types.get_bytes(row['FetchedResult'])  
    # Extracts the binary content of the `FetchedResult` field from the `row` dictionary.  
    # The `get_bytes` function ensures the content is treated as bytes.

    voice_output = voice_output_pb2.TVoiceOutput.FromString(proto_content)  
    # Deserializes the binary content (`proto_content`) into a `TVoiceOutput` protobuf message.  
    # The `FromString` method is used to parse the binary data.

    voice_output_dict = json_format.MessageToDict(voice_output, including_default_value_fields=True)  
    # Converts the `TVoiceOutput` protobuf message into a Python dictionary using `json_format.MessageToDict`.  
    # The `including_default_value_fields=True` parameter ensures that fields with default values are included in the dictionary.

    voice_output_dict['Error'] = row['Error']  
    # Adds the `Error` field from the `row` dictionary to the `voice_output_dict`.  
    # This ensures that any error information is preserved in the output.

    yield voice_output_dict  
    # Yields the processed dictionary as part of the generator function.  
    # This allows the function to be used in a streaming or iterative context.

@click.command()  
# Decorates the following function with `click.command()`, turning it into a Click command-line interface (CLI) command.

@click.option('--input', required=True, help='Input table path')  
# Adds a command-line option `--input` that is required.  
# The `help` text describes the option as the path to the input table.

@click.option('--output', required=True, help='Output table path')  
# Adds a command-line option `--output` that is required.  
# The `help` text describes the option as the path to the output table.

@click.option('--yt-proxy', required=True, envvar='YT_PROXY', help='YT cluster proxy, envvar: YT_PROXY')  
# Adds a command-line option `--yt-proxy` that is required.  
# The `envvar` parameter specifies that the value can also be provided via the `YT_PROXY` environment variable.  
# The `help` text describes the option as the YT cluster proxy.

@click.option('--yt-token', required=True, envvar='YT_TOKEN', help='Yt token, envvar: YT_TOKEN')  
# Adds a command-line option `--yt-token` that is required.  
# The `envvar` parameter specifies that the value can also be provided via the `YT_TOKEN` environment variable.  
# The `help` text describes the option as the YT token.

@click.option('--mr-account', default='alice-dev', show_default=True, help='Yt quota account')  
# Adds a command-line option `--mr-account` with a default value of `alice-dev`.  
# The `show_default=True` parameter ensures the default value is displayed in the help text.  
# The `help` text describes the option as the YT quota account.

@click.option('--oauth-token', envvar='ALICE_OAUTH_TOKEN',  
              help='OAuth token for scenarios with authorization, envvar: ALICE_OAUTH_TOKEN')  
# Adds a command-line option `--oauth-token`.  
# The `envvar` parameter specifies that the value can also be provided via the `ALICE_OAUTH_TOKEN` environment variable.  
# The `help` text describes the option as the OAuth token for authorization scenarios.

@click.option('--experiments', default='', help='Additional experiments. Format: exp1=val,exp2=val2')  
# Adds a command-line option `--experiments` with a default value of an empty string.  
# The `help` text describes the option as additional experiments in the format `exp1=val,exp2=val2`.

@click.option('--uniproxy-fetcher-mode', default='auto',  
              type=click.Choice(['voice', 'text', 'auto']),  
              show_default=True,  
              help='Fetcher type for uniproxy requests.')  
# Adds a command-line option `--uniproxy-fetcher-mode` with a default value of `auto`.  
# The `type` parameter restricts the input to one of the choices: `voice`, `text`, or `auto`.  
# The `show_default=True` parameter ensures the default value is displayed in the help text.  
# The `help` text describes the option as the fetcher type for uniproxy requests.

@click.option('--uniproxy-url', default='wss://beta.uniproxy.alice.yandex.net/alice-uniproxy-hamster/uni.ws',  
              show_default=True, help='Uniproxy url')  
# Adds a command-line option `--uniproxy-url` with a default value of `wss://beta.uniproxy.alice.yandex.net/alice-uniproxy-hamster/uni.ws`.  
# The `show_default=True` parameter ensures the default value is displayed in the help text.  
# The `help` text describes the option as the URL for the uniproxy service.

@click.option('--megamind-url', default='http://vins.hamster.alice.yandex.net/speechkit/app/pa/',  
              show_default=True, help='Megamind url')  
# Adds a command-line option `--megamind-url` with a default value of `http://vins.hamster.alice.yandex.net/speechkit/app/pa/`.  
# The `show_default=True` parameter ensures the default value is displayed in the help text.  
# The `help` text describes the option as the URL for the Megamind service.

@click.option('--asr-chunk-size', default='-1', show_default=True,  
              help='Asr chunk size')  
# Adds a command-line option `--asr-chunk-size` with a default value of `-1`.  
# The `show_default=True` parameter ensures the default value is displayed in the help text.  
# The `help` text describes the option as the chunk size for ASR (Automatic Speech Recognition).

@click.option('--asr-chunk-delay-ms', default='0', show_default=True,  
              help='Asr chunk delay between chunks in milliseconds')  
# Adds a command-line option `--asr-chunk-delay-ms` with a default value of `0`.  
# The `show_default=True` parameter ensures the default value is displayed in the help text.  
# The `help` text describes the option as the delay between ASR chunks in milliseconds.

@click.option('--flags', default=PRODUCTION_FLAGS, show_default=True,  
              help='Downloader feature flags, json-list format')  
# Adds a command-line option `--flags` with a default value of `PRODUCTION_FLAGS`.  
# The `show_default=True` parameter ensures the default value is displayed in the help text.  
# The `help` text describes the option as the downloader feature flags in JSON-list format.

@click.option('--no-prepare', default=False, is_flag=True)  
# Adds a command-line option `--no-prepare` that is a flag (boolean).  
# The default value is `False`, and the flag is set to `True` when the option is provided.

@click.option('--prepare-only', default=False, is_flag=True)  
# Adds a command-line option `--prepare-only` that is a flag (boolean).  
# The default value is `False`, and the flag is set to `True` when the option is provided.
```

```python
def main(input, output, yt_proxy, yt_token, mr_account, oauth_token, experiments, uniproxy_fetcher_mode,  
         uniproxy_url, megamind_url, asr_chunk_size, asr_chunk_delay_ms, flags, no_prepare, prepare_only):  
    # Defines the `main` function, which serves as the entry point of the program.  
    # The function takes multiple parameters, including input/output paths, YT configuration, and various options.

    yt.config['proxy']['url'] = yt_proxy  
    # Sets the YT proxy URL in the `yt.config` dictionary.  
    # This specifies the YT cluster to connect to.

    yt.config['token'] = yt_token  
    # Sets the YT token in the `yt.config` dictionary.  
    # This is used for authentication when interacting with the YT cluster.

    tmp_tables_dir = '//home/%s/%s/tmp' % (mr_account, os.environ['USER'])  
    # Constructs a temporary directory path in YT for storing intermediate tables.  
    # The path is based on the `mr_account` (quota account) and the current user's username.

    yt.config['remote_temp_tables_directory'] = tmp_tables_dir  
    # Sets the `remote_temp_tables_directory` in `yt.config` to the constructed temporary directory path.  
    # This ensures that temporary tables are stored in the specified location.

    with os.popen('ya dump root') as f:  
        # Executes the command `ya dump root` to retrieve the root directory of the Arcadia repository.  
        # The `os.popen` function runs the command and returns a file-like object for reading its output.

        arc_root = f.read()  
        # Reads the output of the `ya dump root` command, which is the path to the Arcadia root directory.  
        # The result is stored in the `arc_root` variable.

    fetcher_path = os.path.join(arc_root, 'search/scraper_over_yt/mapper/mapper')  
    # Constructs the path to the `mapper` binary within the Arcadia repository.  
    # The binary is located in the `search/scraper_over_yt/mapper` directory.

    binary_path = os.path.join(arc_root, 'alice/acceptance/modules/request_generator/scrapper/bin/downloader_inner')  
    # Constructs the path to the `downloader_inner` binary within the Arcadia repository.  
    # The binary is located in the `alice/acceptance/modules/request_generator/scrapper/bin` directory.

    with yt.TempTable() as reduced_for_downloader:  
        # Creates a temporary table in YT using `yt.TempTable()`.  
        # The temporary table is used to store intermediate results during the reduce operation.

        if no_prepare:  
            # Checks if the `no_prepare` flag is set to `True`.  
            # If true, skips the preparation step and uses the input table directly.

            reduced_for_downloader = input  
            # Sets `reduced_for_downloader` to the input table path, bypassing the reduce operation.

        else:  
            # If `no_prepare` is `False`, proceeds with the preparation step.

            if prepare_only:  
                # Checks if the `prepare_only` flag is set to `True`.  
                # If true, prepares the data and writes it directly to the output table.

                reduced_for_downloader = output  
                # Sets `reduced_for_downloader` to the output table path, skipping the download step.

            run_reduce(prepare_reducer, input, reduced_for_downloader, ['session_id'])  
            # Runs the reduce operation using the `prepare_reducer` function.  
            # The input table is reduced and the result is stored in `reduced_for_downloader`.  
            # The reduce operation is performed on the `session_id` field.

        if prepare_only:  
            # Checks if the `prepare_only` flag is set to `True`.  
            # If true, exits the function after preparing the data.

            return  
            # Exits the function early, skipping the download and mapping steps.

        downloaded_table = tmp_tables_dir + '/' + str(uuid.uuid4())  
        # Generates a unique path for the downloaded table by appending a UUID to the temporary directory path.

        fetcher_cmd = [  
            # Constructs the command to run the fetcher binary.  
            fetcher_path, 'deep_uniproxy',  
            # Specifies the fetcher binary and the `deep_uniproxy` mode.  
            '--input-path', reduced_for_downloader,  
            # Specifies the input table path for the fetcher.  
            '--output-path', downloaded_table,  
            # Specifies the output table path for the fetcher.  
            '--uniproxy-url', uniproxy_url,  
            # Specifies the URL for the uniproxy service.  
            '--vins-url', megamind_url,  
            # Specifies the URL for the Megamind service.  
            '--asr-chunk-size', asr_chunk_size,  
            # Specifies the chunk size for ASR (Automatic Speech Recognition).  
            '--asr-chunk-delay-ms', asr_chunk_delay_ms,  
            # Specifies the delay between ASR chunks in milliseconds.  
            '--binary-path', binary_path,  
            # Specifies the path to the `downloader_inner` binary.  
            '--binary-params', json.dumps({  
                # Specifies the parameters for the `downloader_inner` binary as a JSON string.  
                'process_id': 'dummy_downloader',  
                # Sets a dummy process ID.  
                'oauth_token': oauth_token,  
                # Specifies the OAuth token for authorization.  
                'experiments': experiments,  
                # Specifies additional experiments.  
                'fetcher_mode': uniproxy_fetcher_mode,  
                # Specifies the fetcher mode (e.g., `voice`, `text`, or `auto`).  
                'retry_profile': 'music_video_search',  
                # Specifies the retry profile for the downloader.  
                # 'downloader_flags': json.loads(flags),  
                # (Commented out) Specifies the downloader flags as a JSON object.  
                'downloader_flags': flags,  
                # Specifies the downloader flags as a JSON string.  
            }),  
            '--flags', flags,  
            # Specifies the downloader feature flags.  
        ]  
        print(' '.join(fetcher_cmd))  
        # Prints the constructed fetcher command for debugging purposes.

        with subprocess.Popen(fetcher_cmd, stdout=subprocess.PIPE) as p:  
            # Runs the fetcher command as a subprocess.  
            # The `subprocess.Popen` function spawns the process and captures its output.

            print(p.stdout.read())  
            # Reads and prints the output of the fetcher command.

            p.wait()  
            # Waits for the fetcher command to complete.

        error_suffix = '.error'  
        # Defines a suffix for error tables.

        yt.run_map(unpack_mapper, downloaded_table, output)  
        # Runs a map operation on the downloaded table using the `unpack_mapper` function.  
        # The result is written to the output table.

        yt.run_map(unpack_mapper, downloaded_table + error_suffix, output + error_suffix)  
        # Runs a map operation on the error table using the `unpack_mapper` function.  
        # The result is written to the error output table.

        yt.remove(downloaded_table)  
        # Deletes the downloaded table from YT.

        yt.remove(downloaded_table + error_suffix)  
        # Deletes the error table from YT.


if __name__ == '__main__':  
    # Checks if the script is being run as the main program.  
    # This ensures that the `main` function is only called when the script is executed directly.

    main()  
    # Calls the `main` function to start the program.
```
