```python
# coding: utf-8  
# Specifies the encoding of the script as UTF-8.  
# This ensures that the script can handle non-ASCII characters.

import attrdict  
# Imports the `attrdict` library, which provides a dictionary-like object that allows attribute-style access to its keys.  
# For example, `conf_dict.key` instead of `conf_dict['key']`.

import attr  
# Imports the `attr` library, which is used to define classes with minimal boilerplate.  
# It provides decorators like `@attr.s` to simplify class creation.

import yaml  
# Imports the `yaml` module, which provides functions for working with YAML files.  
# YAML is a human-readable data serialization format often used for configuration files.

import vh  
# Imports the `vh` module, which is likely a custom or third-party library used in the project.  
# The specific functionality of `vh` is not clear from this snippet.

def init_config(config_path):  
    # Defines a function named `init_config` that takes one argument: `config_path`.  
    # This function is used to initialize and load a configuration from a YAML file.

    with open(config_path) as f:  
        # Opens the file specified by `config_path` in read mode.  
        # The `with` statement ensures the file is properly closed after reading.

        conf_dict = yaml.safe_load(f.read())  
        # Reads the content of the file and parses it as YAML using `yaml.safe_load`.  
        # The result is a Python dictionary (`conf_dict`) containing the configuration data.

    return attrdict.AttrDict(conf_dict)  
    # Converts the `conf_dict` dictionary into an `AttrDict` object.  
    # This allows for attribute-style access to the configuration keys (e.g., `conf.key` instead of `conf['key']`).

@attr.s  
# Decorates the following class with `@attr.s`, which is a shorthand for `attr.attrs`.  
# This decorator automatically adds special methods (e.g., `__init__`, `__repr__`) to the class, reducing boilerplate code.
```

```python
class GlobalOptions:  
    # Defines a class named `GlobalOptions`.  
    # This class is used to store and manage global configuration options for the application.

    cache_sync = attr.ib()  
    # Defines a class attribute `cache_sync` using `attr.ib()`.  
    # This attribute is likely used to control cache synchronization behavior.  
    # The `attr.ib()` function creates an attribute with default metadata for the `attr` library.

    yt_token = attr.ib()  
    # Defines a class attribute `yt_token` using `attr.ib()`.  
    # This attribute is likely used to store the YT (Yandex.Tank or Yandex Table) authentication token.

    yt_proxy = attr.ib()  
    # Defines a class attribute `yt_proxy` using `attr.ib()`.  
    # This attribute is likely used to store the YT cluster proxy URL.

    yt_pool = attr.ib()  
    # Defines a class attribute `yt_pool` using `attr.ib()`.  
    # This attribute is likely used to specify the YT pool for resource allocation.

    mr_account = attr.ib()  
    # Defines a class attribute `mr_account` using `attr.ib()`.  
    # This attribute is likely used to specify the MapReduce (MR) quota account.

    mr_output_ttl = attr.ib()  
    # Defines a class attribute `mr_output_ttl` using `attr.ib()`.  
    # This attribute is likely used to specify the time-to-live (TTL) for MapReduce output data.

    mr_output_path = attr.ib()  
    # Defines a class attribute `mr_output_path` using `attr.ib()`.  
    # This attribute is likely used to specify the output path for MapReduce results.

    yql_token = attr.ib()  
    # Defines a class attribute `yql_token` using `attr.ib()`.  
    # This attribute is likely used to store the YQL (Yandex Query Language) authentication token.

    arcanum_token = attr.ib()  
    # Defines a class attribute `arcanum_token` using `attr.ib()`.  
    # This attribute is likely used to store the Arcanum authentication token.  
    # Arcanum is a code review tool used at Yandex.

    uniproxy_url = attr.ib()  
    # Defines a class attribute `uniproxy_url` using `attr.ib()`.  
    # This attribute is likely used to store the URL for the uniproxy service.

    vins_url = attr.ib()  
    # Defines a class attribute `vins_url` using `attr.ib()`.  
    # This attribute is likely used to store the URL for the Vins (Voice INterface Service) or Megamind service.

    ya_plus_token = attr.ib()  
    # Defines a class attribute `ya_plus_token` using `attr.ib()`.  
    # This attribute is likely used to store the Yandex.Plus authentication token.  
    # Yandex.Plus is a subscription service offering additional features.
```

```python
global_options = GlobalOptions(  
    # Creates an instance of the `GlobalOptions` class and assigns it to the variable `global_options`.  
    # The attributes of the class are initialized using the `vh.add_global_option` function.

    cache_sync=vh.add_global_option('cache_sync', 'integer', default=0),  
    # Initializes the `cache_sync` attribute using `vh.add_global_option`.  
    # The option is named 'cache_sync', has a type of 'integer', and a default value of `0`.

    yt_token=vh.add_global_option('yt-token', vh.Secret, required=True),  
    # Initializes the `yt_token` attribute using `vh.add_global_option`.  
    # The option is named 'yt-token', has a type of `vh.Secret` (indicating sensitive data), and is required.

    yt_proxy=vh.add_global_option('yt-proxy', 'string', required=True),  
    # Initializes the `yt_proxy` attribute using `vh.add_global_option`.  
    # The option is named 'yt-proxy', has a type of 'string', and is required.

    yt_pool=vh.add_global_option('yt-pool', 'string', default=None),  
    # Initializes the `yt_pool` attribute using `vh.add_global_option`.  
    # The option is named 'yt-pool', has a type of 'string', and a default value of `None`.

    mr_account=vh.add_global_option('mr-account', 'string', required=True),  
    # Initializes the `mr_account` attribute using `vh.add_global_option`.  
    # The option is named 'mr-account', has a type of 'string', and is required.

    mr_output_ttl=vh.add_global_option('mr-output-ttl', 'integer', required=True),  
    # Initializes the `mr_output_ttl` attribute using `vh.add_global_option`.  
    # The option is named 'mr-output-ttl', has a type of 'integer', and is required.

    mr_output_path=vh.add_global_option('mr-output-path', 'string', default=''),  
    # Initializes the `mr_output_path` attribute using `vh.add_global_option`.  
    # The option is named 'mr-output-path', has a type of 'string', and a default value of an empty string.

    yql_token=vh.add_global_option('yql-token', vh.Secret, required=True),  
    # Initializes the `yql_token` attribute using `vh.add_global_option`.  
    # The option is named 'yql-token', has a type of `vh.Secret`, and is required.

    arcanum_token=vh.add_global_option('arcanum-token', vh.Secret, required=True),  
    # Initializes the `arcanum_token` attribute using `vh.add_global_option`.  
    # The option is named 'arcanum-token', has a type of `vh.Secret`, and is required.

    uniproxy_url=vh.add_global_option('uniproxy-url', 'string', required=True),  
    # Initializes the `uniproxy_url` attribute using `vh.add_global_option`.  
    # The option is named 'uniproxy-url', has a type of 'string', and is required.

    vins_url=vh.add_global_option('vins-url', 'string', default=''),  
    # Initializes the `vins_url` attribute using `vh.add_global_option`.  
    # The option is named 'vins-url', has a type of 'string', and a default value of an empty string.

    ya_plus_token=vh.add_global_option('ya-plus-token', vh.Secret, required=True),  
    # Initializes the `ya_plus_token` attribute using `vh.add_global_option`.  
    # The option is named 'ya-plus-token', has a type of `vh.Secret`, and is required.
)
```
