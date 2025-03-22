```python
# Importing the built-in JSON module for handling JSON data
import json  
# Importing the built-in OS module for interacting with the operating system
import os  

# Importing the pytest framework for testing
import pytest  

# Importing specific checker classes from the module responsible for analytics checks
from alice.acceptance.modules.check_analytics_info.lib.checkers import (  
    MegamindAnalyticsInfoChecker,  # Checker for Megamind analytics
    MetaChecker,  # Checker for Meta analytics
    TunnellerChecker  # Checker for Tunneller analytics
)

# Importing utility functions used for processing analytics data
from alice.acceptance.modules.check_analytics_info.lib.utils import collect_dump_data, generate_file_name  

# Importing resource module from Python library, likely used to manage test data files
from library.python import resource  

# Defining a constant that specifies the directory containing test data
DATA_DIR = 'data'  

# Using the pytest.mark.parametrize decorator to run the test with different checker classes
@pytest.mark.parametrize('cls_checker', [MegamindAnalyticsInfoChecker, MetaChecker, TunnellerChecker])  
def test_checker(cls_checker):  # Function to test a given checker class
    # Iterating over each test directory found in the resource files under DATA_DIR
    for test_dir in (path.split(os.sep)[1] for path in resource.resfs_files(DATA_DIR)):  
        # Instantiating the checker class dynamically
        checker = cls_checker()  
        
        # Constructing the path to the current test directory
        cur_dir = os.path.join(DATA_DIR, test_dir)  
        
        # Loading the input data table from a JSON file located in the test directory
        input_table = json.loads(resource.resfs_read(os.path.join(cur_dir, 'input_table.json')))  
        
        # Collecting actual analytics dump data using the checker
        actual = collect_dump_data(checker, input_table)  
        
        # Loading the expected output data from a corresponding JSON file
        expected = json.loads(
            resource.resfs_read(os.path.join(cur_dir, '{}.json'.format(generate_file_name(checker)))))  
        
        # Asserting that the expected and actual results match, ensuring test correctness
        assert expected == json.loads(json.dumps(actual))  
```
