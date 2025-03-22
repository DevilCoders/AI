```python
# Import the 'os' module for interacting with the operating system (e.g., environment variables).
import os

# Import the 'time' module for working with timestamps.
import time

# Import the 'click' module for creating command-line interfaces.
import click

# Import the 'vh' module, which is likely a framework for defining and executing data pipelines.
import vh

# Import the 'check_analytics_info' function from the 'alice.acceptance.runners.check_analytics_info' module.
from alice.acceptance.runners.check_analytics_info import run as check_analytics_info

# Import the 'init_config' function from the 'alice.acceptance.runners.config' module.
from alice.acceptance.runners.config import init_config


# Define a dictionary mapping module keys to their corresponding functions.
# This allows for dynamic execution of different modules based on configuration.
ACC_MODULES = {
    'check_analytics_info': check_analytics_info,  # Maps 'check_analytics_info' to its function.
}


# Define a function to run modules in the order specified by the configuration.
def run_in_config_order(config):
    # Initialize an empty list to store the 'after' dependencies for each module.
    prev_after_arr = []
    # Iterate over each group of modules in the acceptance order.
    for group in config.acceptance_order:
        # Initialize an empty list to store the 'after' dependencies for the current group.
        after_arr = []
        # Iterate over each module key in the current group.
        for module_key in group:
            # Check if the module key is valid and exists in the ACC_MODULES dictionary.
            if module_key and module_key in ACC_MODULES:
                # Append the result of building the module's graph to the 'after_arr' list.
                after_arr.append(
                    ACC_MODULES[module_key].build_graph(config, prev_after_arr)
        # Update 'prev_after_arr' with the 'after_arr' of the current group.
        prev_after_arr = after_arr


# Define the main command-line interface using the 'click' module.
@click.command()
# Add an option for specifying the user configuration file.
@click.option(
    '--user-config', default='~/.alice_acceptance/config.yaml',
    help='User config filepath',
)
# Add an option to disable execution (dry-run mode).
@click.option('--no-exec', is_flag=True, default=False)
def main(user_config, no_exec):
    # Initialize the configuration using the specified user configuration file.
    config = init_config(user_config)
    # Run the modules in the order specified by the configuration.
    run_in_config_order(config)

    # Get the current timestamp.
    ts = int(time.time())
    # Execute the pipeline using the 'vh.run' function.
    vh.run(
        start=not no_exec,  # Start the pipeline unless 'no-exec' is True.
        global_options={
            'yql_token': config.yql.token,  # YQL token for authentication.
            'user_oauth': config.alice_common.ya_plus_robot_token,  # OAuth token for authentication.
            'cache_sync': ts,  # Timestamp for cache synchronization.
            'soy_token': config.soy.token,  # SOY token for authentication.
        },
        yt_proxy=config.yt.proxy,  # YT (Yandex Table) proxy to use.
        yt_token_secret=config.yt.token,  # YT token for authentication.
        mr_account=config.yt.mr_account,  # MR (MapReduce) account to use.
        quota=config.nirvana.quota,  # Quota for the Nirvana service.
        project=config.nirvana.project,  # Nirvana project to use.
        label=config.nirvana.label,  # Label for the Nirvana job.
        oauth_token=os.environ.get('NIRVANA_TOKEN') or None,  # Nirvana OAuth token from environment.
    )


# Entry point for the script.
if __name__ == '__main__':
    # Execute the main function when the script is run.
    main()
```
