```python
# Importing the built-in JSON module for handling JSON data (reading, writing, parsing)
import json  
# Importing the built-in OS module for interacting with the file system and directories
import os  

# Importing the Click module for creating command-line interfaces (CLI)
import click  

# Importing specific checker classes used for analytics validation
from alice.acceptance.modules.check_analytics_info.lib.checkers import (  
    MegamindAnalyticsInfoChecker,  # Checker for Megamind analytics
    MetaChecker,  # Checker for Meta analytics
    TunnellerChecker  # Checker for Tunneller analytics
)

# Importing utility functions used for processing analytics data
from alice.acceptance.modules.check_analytics_info.lib.utils import collect_dump_data, generate_file_name  

# Defining a list of checker classes to be used for validation
CHECKERS = [MegamindAnalyticsInfoChecker, MetaChecker, TunnellerChecker]  

# Defining a command-line interface (CLI) command using Click
@click.command()  
# Adding an option to specify the data directory (must be an existing path)
@click.option('--data-dir', type=click.Path(exists=True))  
def main(data_dir):  # Main function that processes all test directories in the given data directory
    # Iterating over each test directory inside the specified data directory
    for test_dir in os.listdir(data_dir):  
        # Constructing the full path to the current test directory
        cur_dir = os.path.join(data_dir, test_dir)  
        
        # Opening and reading the input JSON file containing test data
        with open(os.path.join(cur_dir, 'input_table.json'), 'r') as table_file:  
            input_table = json.load(table_file)  # Parsing JSON data into a Python dictionary
        
        # Iterating over each checker class in the CHECKERS list
        for checker_cls in CHECKERS:  
            checker = checker_cls()  # Instantiating the checker
            
            # Processing the input data using the checker to generate canonized data
            canonized_data = collect_dump_data(checker, input_table)  
            
            # Generating the output file name dynamically based on the checker
            output_file_path = os.path.join(cur_dir, '{}.json'.format(generate_file_name(checker)))  
            
            # Writing the processed data to the output JSON file
            with open(output_file_path, 'w') as canonized_data_file:  
                json.dump(canonized_data, canonized_data_file, indent=4, sort_keys=True)  
                # Dumps JSON data with indentation and sorted keys for readability

# Standard Python entry point: ensures the script runs only when executed directly
if __name__ == '__main__':  
    main()  # Calls the main function to execute the script
```
