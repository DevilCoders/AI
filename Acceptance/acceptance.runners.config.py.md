```python
# Import the 'os' module for interacting with the operating system (e.g., file paths).
import os

# Import the 'attr' module for defining classes with attributes.
import attr

# Import the 'attrdict' module for creating dictionary-like objects with attribute access.
import attrdict

# Import the 'vh' module, which is likely a framework for defining and executing data pipelines.
import vh

# Import the 'yaml' module for working with YAML files.
import yaml

# Import the 'always_merger' function from the 'deepmerge' module for merging dictionaries.
from deepmerge import always_merger as dict_merger

# Import the 'resource' module from the 'library.python' package for accessing resources.
from library.python import resource


# Define a class 'GlobalOptions' using the 'attr.s' decorator.
# This class represents global configuration options for the pipeline.
@attr.s
class GlobalOptions:
    # Define an attribute for the YQL token.
    yql_token = attr.ib()
    # Define an attribute for the Yandex Plus OAuth token.
    ya_plus_token = attr.ib()
    # Define an attribute for cache synchronization.
    cache_sync = attr.ib()
    # Define an attribute for the SOY token.
    soy_token = attr.ib()


# Define a function to initialize the configuration.
def init_config(user_config_path):
    # Load the base configuration from a YAML file embedded in the resources.
    conf_dict = yaml.safe_load(resource.find('/config.yaml'))
    # Expand the '~' in the user configuration path to the user's home directory.
    expand = os.path.expanduser('~')
    user_config_path = user_config_path.replace('~', expand)
    # Check if the user configuration file exists.
    if os.path.exists(user_config_path):
        # Open and load the user configuration file.
        with open(user_config_path) as f:
            # Merge the base configuration with the user configuration.
            conf_dict = dict_merger.merge(conf_dict, yaml.safe_load(f))
    # Convert the merged dictionary to an 'AttrDict' for attribute-style access.
    return attrdict.AttrDict(conf_dict)


# Define a global 'GlobalOptions' object with options for the pipeline.
global_options = GlobalOptions(
    # Add a global option for the YQL token as a secret.
    yql_token=vh.add_global_option('yql_token', vh.Secret, required=True),
    # Add a global option for the Yandex Plus OAuth token as a secret.
    ya_plus_token=vh.add_global_option('user_oauth', vh.Secret, required=True),
    # Add a global option for cache synchronization as an integer.
    cache_sync=vh.add_global_option('cache_sync', 'integer', required=True),
    # Add a global option for the SOY token as a secret.
    soy_token=vh.add_global_option('soy_token', 'secret', required=True),
)
```
