```python
import base64
# Imports the `base64` module, which provides functions for encoding and decoding data in Base64 format.

import json
# Imports the `json` module, which provides functions for working with JSON data (e.g., parsing and serializing).

from abc import ABC, abstractmethod
# Imports the `ABC` class and `abstractmethod` decorator from the `abc` module.
# These are used to define abstract base classes and abstract methods.

from search.tunneller.libs.protocol_decl.scraper_over_yt_info_pb2 import TScraperOverYtMessage
# Imports the `TScraperOverYtMessage` class from a Protocol Buffers (protobuf) generated module.
# This class is likely used to represent a message format for scraper-over-YT communication.

class Checker(ABC):
    # Defines an abstract base class named `Checker` using the `ABC` class.
    # This class serves as a blueprint for specific checker implementations.

    @abstractmethod
    def process_row(self, row):
        # Defines an abstract method named `process_row` that must be implemented by subclasses.
        # This method is intended to process a single row of data.
        pass

    @abstractmethod
    def dump_result(self):
        # Defines an abstract method named `dump_result` that must be implemented by subclasses.
        # This method is intended to output or save the results of the checking process.
        pass

class TunnellerChecker(Checker):
    # Defines a subclass named `TunnellerChecker` that inherits from the `Checker` abstract base class.
    # This class implements specific functionality for checking tunneller responses.

    NAME = 'tunneller_checker'
    # Defines a class-level constant `NAME` that stores the name of the checker.

    DESCRIPTION = 'checks emptiness, base64 correctness of tunneller raw responses'
    # Defines a class-level constant `DESCRIPTION` that describes the purpose of the checker.

    MAX_DIFF = 0.02
    # Defines a class-level constant `MAX_DIFF` that specifies the maximum allowed difference (e.g., for validation).

    class Counters:
        # Defines an inner class named `Counters` to track various statistics during the checking process.

        def __init__(self):
            # Defines the constructor for the `Counters` class.
            self.responses = 0
            # Initializes a counter for the total number of responses.
            self.tunneller_responses = 0
            # Initializes a counter for the number of tunneller responses.
            self.good_tunneller_responses = 0
            # Initializes a counter for the number of valid tunneller responses.
            self.empty_tunneller_responses = 0
            # Initializes a counter for the number of empty tunneller responses.
            self.undecodable_tunneller_responses = 0
            # Initializes a counter for the number of undecodable tunneller responses.

        def __add__(self, other):
            # Defines the `__add__` method to allow adding two `Counters` instances.
            counters = TunnellerChecker.Counters()
            # Creates a new `Counters` instance to store the result of the addition.
            counters.responses = self.responses + other.responses
            # Adds the `responses` counters from both instances.
            counters.tunneller_responses = self.tunneller_responses + other.tunneller_responses
            # Adds the `tunneller_responses` counters from both instances.
            counters.good_tunneller_responses = self.good_tunneller_responses + other.good_tunneller_responses
            # Adds the `good_tunneller_responses` counters from both instances.
            counters.empty_tunneller_responses = self.empty_tunneller_responses + other.empty_tunneller_responses
            # Adds the `empty_tunneller_responses` counters from both instances.
            counters.undecodable_tunneller_responses = self.undecodable_tunneller_responses + \
                                                       other.undecodable_tunneller_responses
            # Adds the `undecodable_tunneller_responses` counters from both instances.
            return counters
            # Returns the new `Counters` instance containing the summed values.

        def __eq__(self, other):
            # Defines the `__eq__` method to compare two `Counters` instances for equality.
            eq = True
            # Initializes a variable `eq` to `True`.
            eq = eq and self.responses == other.responses
            # Checks if the `responses` counters are equal.
            eq = eq and self.tunneller_responses == other.tunneller_responses
            # Checks if the `tunneller_responses` counters are equal.
            eq = eq and self.good_tunneller_responses == other.good_tunneller_responses
            # Checks if the `good_tunneller_responses` counters are equal.
            eq = eq and self.empty_tunneller_responses == other.empty_tunneller_responses
            # Checks if the `empty_tunneller_responses` counters are equal.
            eq = eq and self.undecodable_tunneller_responses == other.undecodable_tunneller_responses
            # Checks if the `undecodable_tunneller_responses` counters are equal.
            return eq
            # Returns the result of the equality comparison.

        def __ne__(self, other):
            # Defines the `__ne__` method to compare two `Counters` instances for inequality.
            return not self.__eq__(other)
            # Returns the negation of the `__eq__` method result.

    def __init__(self):
        # Defines the constructor for the `TunnellerChecker` class.
        self._test_counters = self.Counters()
        # Initializes a `Counters` instance for tracking test statistics.
        self._stable_counters = self.Counters()
        # Initializes a `Counters` instance for tracking stable statistics.
```

```python
@staticmethod
# Decorates the method as a static method, meaning it belongs to the class rather than an instance of the class.

def _get_all_tunneller_responses(tunneller_raw_responses_dict):
    # Defines a static method named `_get_all_tunneller_responses` that extracts tunneller responses from a dictionary.
    # The method takes one argument:
    # - `tunneller_raw_responses_dict`: A dictionary containing tunneller raw responses.

    tunneller_raw_responses = []
    # Initializes an empty list named `tunneller_raw_responses` to store the extracted responses.

    if not isinstance(tunneller_raw_responses_dict, dict):
        # Checks if `tunneller_raw_responses_dict` is not a dictionary.
        return tunneller_raw_responses
        # Returns the empty list if the input is not a dictionary.

    for _, responses in tunneller_raw_responses_dict.items():
        # Iterates over the key-value pairs in `tunneller_raw_responses_dict`.
        # The key is ignored (using `_`), and the value is stored in `responses`.

        responses = responses.get('responses', [])
        # Retrieves the list of responses under the key 'responses'. If the key does not exist, defaults to an empty list.

        if responses:
            # Checks if the `responses` list is not empty.
            tunneller_raw_responses.extend(responses)
            # Extends the `tunneller_raw_responses` list with the responses from the current key.

    return tunneller_raw_responses
    # Returns the list of all tunneller raw responses.

@staticmethod
# Decorates the method as a static method, meaning it belongs to the class rather than an instance of the class.

def _check_base64(s):
    # Defines a static method named `_check_base64` that checks if a string is valid Base64 and can be decoded into a protobuf message.
    # The method takes one argument:
    # - `s`: A string to be checked.

    try:
        # Begins a `try` block to handle potential exceptions during Base64 decoding and protobuf parsing.

        message = TScraperOverYtMessage()
        # Creates an instance of the `TScraperOverYtMessage` protobuf class.

        message.ParseFromString(base64.b64decode(s))
        # Decodes the Base64 string `s` into bytes and parses it into the `message` object.

        return True
        # Returns `True` if the Base64 string is valid and can be parsed into a protobuf message.

    except Exception:
        # Catches any exception that occurs during the `try` block (e.g., invalid Base64 or protobuf parsing error).
        return False
        # Returns `False` if an exception occurs.

def _calc_counters(self, vins_response):
    # Defines a method named `_calc_counters` that calculates counters for tunneller responses in a Vins response.
    # The method takes one argument:
    # - `vins_response`: A dictionary containing the Vins response data.

    counters = self.Counters()
    # Creates a new instance of the `Counters` class to track statistics.

    counters.responses += 1
    # Increments the `responses` counter by 1 to track the total number of responses.

    tunneller_raw_responses_dict = vins_response.get('directive', {}).get('payload', {}).get(
        'megamind_analytics_info', {}).get('tunneller_raw_responses', {})
    # Retrieves the `tunneller_raw_responses` dictionary from the nested structure in `vins_response`.
    # Uses `dict.get` with default values to avoid KeyError if any key is missing.

    tunneller_raw_responses = TunnellerChecker._get_all_tunneller_responses(tunneller_raw_responses_dict)
    # Calls the `_get_all_tunneller_responses` static method to extract all tunneller raw responses from the dictionary.

    for tunneller_raw_response in tunneller_raw_responses:
        # Iterates over each tunneller raw response in the list.

        counters.tunneller_responses += 1
        # Increments the `tunneller_responses` counter by 1 to track the total number of tunneller responses.

        if tunneller_raw_response == '':
            # Checks if the tunneller raw response is an empty string.
            counters.empty_tunneller_responses += 1
            # Increments the `empty_tunneller_responses` counter by 1.

        elif not TunnellerChecker._check_base64(tunneller_raw_response):
            # Checks if the tunneller raw response is not valid Base64 using the `_check_base64` static method.
            counters.undecodable_tunneller_responses += 1
            # Increments the `undecodable_tunneller_responses` counter by 1.

        else:
            # If the tunneller raw response is valid Base64, this block executes.
            counters.good_tunneller_responses += 1
            # Increments the `good_tunneller_responses` counter by 1.

    return counters
    # Returns the `counters` object containing the calculated statistics.
```

```python
def process_row(self, row):
    # Defines the `process_row` method, which processes a single row of data.
    # The method takes one argument:
    # - `row`: A dictionary representing a row of data.

    verdict = True
    # Initializes `verdict` to `True`, indicating the row is valid by default.

    message = None
    # Initializes `message` to `None`, which will store a descriptive message if the row is invalid.

    if row.get('test.VinsResponse') and row.get('stable.VinsResponse'):
        # Checks if the row contains both 'test.VinsResponse' and 'stable.VinsResponse' keys.

        row_test_counters = self._calc_counters(json.loads(row['test.VinsResponse']))
        # Parses the 'test.VinsResponse' JSON string and calculates counters using `_calc_counters`.

        self._test_counters += row_test_counters
        # Adds the counters from the test response to the overall test counters.

        row_stable_counters = self._calc_counters(json.loads(row['stable.VinsResponse']))
        # Parses the 'stable.VinsResponse' JSON string and calculates counters using `_calc_counters`.

        self._stable_counters += row_stable_counters
        # Adds the counters from the stable response to the overall stable counters.

        if row_test_counters != row_stable_counters:
            # Checks if the counters for the test and stable responses are not equal.
            verdict = False
            # Sets `verdict` to `False` if the counters differ.

            if row_test_counters.tunneller_responses != row_stable_counters.tunneller_responses:
                # Checks if the number of tunneller responses differs between test and stable.
                message = ('amount of tunneller responses ({}) in test response not equals to'
                           ' amount ({}) in stable response'.format(row_test_counters.tunneller_responses,
                                                                    row_stable_counters.tunneller_responses))
                # Sets a descriptive message about the mismatch in tunneller response counts.

            elif row_test_counters.good_tunneller_responses != row_stable_counters.good_tunneller_responses:
                # Checks if the number of good tunneller responses differs between test and stable.
                message = ('amount of good tunneller responses ({}) in test response not equals to amount'
                           ' ({}) in stable response'.format(row_test_counters.good_tunneller_responses,
                                                             row_stable_counters.good_tunneller_responses))
                # Sets a descriptive message about the mismatch in good tunneller response counts.

    elif row.get('test.VinsResponse'):
        # Checks if the row contains only 'test.VinsResponse'.
        self._test_counters += self._calc_counters(json.loads(row['test.VinsResponse']))
        # Parses the 'test.VinsResponse' JSON string and updates the test counters.

        message = 'vins response from stable downloading is empty'
        # Sets a message indicating that the stable response is missing.

    elif row.get('stable.VinsResponse'):
        # Checks if the row contains only 'stable.VinsResponse'.
        self._stable_counters += self._calc_counters(json.loads(row['stable.VinsResponse']))
        # Parses the 'stable.VinsResponse' JSON string and updates the stable counters.

        message = 'vins response from test downloading is empty'
        # Sets a message indicating that the test response is missing.

    return verdict, message
    # Returns a tuple containing:
    # - `verdict`: A boolean indicating whether the row is valid.
    # - `message`: A descriptive message if the row is invalid.

@staticmethod
# Decorates the method as a static method, meaning it belongs to the class rather than an instance of the class.

def _calc_diff(test_val, stable_val):
    # Defines a static method named `_calc_diff` that calculates the relative difference between two values.
    # The method takes two arguments:
    # - `test_val`: The value from the test response.
    # - `stable_val`: The value from the stable response.

    return (test_val - stable_val) / stable_val
    # Returns the relative difference between `test_val` and `stable_val`.

@staticmethod
# Decorates the method as a static method, meaning it belongs to the class rather than an instance of the class.

def _calc_mean_tunneller_responses(counters):
    # Defines a static method named `_calc_mean_tunneller_responses` that calculates the mean number of tunneller responses.
    # The method takes one argument:
    # - `counters`: A `Counters` object containing response statistics.

    return counters.tunneller_responses / counters.responses
    # Returns the mean number of tunneller responses per Vins response.

@staticmethod
# Decorates the method as a static method, meaning it belongs to the class rather than an instance of the class.

def _check_count_tunneller(test_counters, stable_counters):
    # Defines a static method named `_check_count_tunneller` that checks if the mean number of tunneller responses is within the allowed difference.
    # The method takes two arguments:
    # - `test_counters`: A `Counters` object for the test response.
    # - `stable_counters`: A `Counters` object for the stable response.

    mean_test_tunneller_responses = TunnellerChecker._calc_mean_tunneller_responses(test_counters)
    # Calculates the mean number of tunneller responses for the test response.

    mean_stable_tunneller_responses = TunnellerChecker._calc_mean_tunneller_responses(stable_counters)
    # Calculates the mean number of tunneller responses for the stable response.

    return abs(TunnellerChecker._calc_diff(mean_test_tunneller_responses,
                                           mean_stable_tunneller_responses)) < TunnellerChecker.MAX_DIFF
    # Returns `True` if the absolute difference between the means is less than `MAX_DIFF`, otherwise `False`.

def dump_result(self):
    # Defines the `dump_result` method, which generates a summary of the checking process.
    # The method takes no arguments.

    verdict = True
    # Initializes `verdict` to `True`, indicating the overall result is valid by default.

    message = ''
    # Initializes `message` to an empty string, which will store the summary message.

    for counters, name in ((self._test_counters, 'test'), (self._stable_counters, 'stable')):
        # Iterates over the test and stable counters.

        message += 'stats of {} downloading:\n'.format(name)
        # Adds a header to the message indicating whether the stats are for test or stable downloading.

        message += 'vins responses: {}\n'.format(counters.responses)
        # Adds the total number of Vins responses to the message.

        if counters.responses > 0:
            # Checks if there are any Vins responses.
            message += 'tunneller responses: {}\n'.format(counters.tunneller_responses)
            # Adds the total number of tunneller responses to the message.

            message += 'empty tunneller responses: {}\n'.format(counters.empty_tunneller_responses)
            # Adds the number of empty tunneller responses to the message.

            message += 'undecodable tunneller responses: {}\n'.format(counters.undecodable_tunneller_responses)
            # Adds the number of undecodable tunneller responses to the message.

            message += 'good tunneller responses: {}\n'.format(counters.good_tunneller_responses)
            # Adds the number of good tunneller responses to the message.

            message += 'mean tunneller responses {:.2f}\n'.format(self._calc_mean_tunneller_responses(counters))
            # Adds the mean number of tunneller responses per Vins response to the message.

        message += '\n'
        # Adds a newline to separate the test and stable stats.

    if (self._test_counters.tunneller_responses == self._test_counters.good_tunneller_responses) and (
            self._test_counters.responses > 0) and (self._stable_counters.responses > 0):
        # Checks if all tunneller responses in the test response are good and both test and stable responses exist.

        if self._check_count_tunneller(self._test_counters, self._stable_counters):
            # Checks if the mean number of tunneller responses is within the allowed difference.
            message += 'test downloading is ok'
            # Adds a message indicating that the test downloading is valid.

            if self._test_counters.tunneller_responses != self._test_counters.good_tunneller_responses:
                # Checks if there are any bad tunneller responses in the stable response.
                message += ' but stable downloading has bad tunneller responses'
                # Adds a message indicating that the stable downloading has issues.

        else:
            # If the mean number of tunneller responses exceeds the allowed difference, this block executes.
            verdict = False
            # Sets `verdict` to `False`.

            message += ('mean of tunneller responses of test downloading ({:.2f})'
                        ' differs more than {:.2f} comparing to stable downloading ({:.2f}) by abs value').format(
                self._calc_mean_tunneller_responses(self._test_counters), self.MAX_DIFF,
                self._calc_mean_tunneller_responses(self._stable_counters))
            # Adds a message describing the difference in mean tunneller responses.

        message += '\n'
        # Adds a newline to separate this section from the next.

    if self._test_counters.empty_tunneller_responses > 0:
        # Checks if there are any empty tunneller responses in the test response.
        verdict = False
        # Sets `verdict` to `False`.

        message += 'amount empty tunneller responses of test downloading is not 0'
        # Adds a message indicating that there are empty tunneller responses.

        if self._stable_counters.empty_tunneller_responses > 0:
            # Checks if there are any empty tunneller responses in the stable response.
            message += ' but stable downloading has empty responses too'
            # Adds a message indicating that the stable downloading also has empty responses.

        message += '\n'
        # Adds a newline to separate this section from the next.

    if self._test_counters.undecodable_tunneller_responses > 0:
        # Checks if there are any undecodable tunneller responses in the test response.
        verdict = False
        # Sets `verdict` to `False`.

        message += 'amount undecodable tunneller responses of test downloading is not 0'
        # Adds a message indicating that there are undecodable tunneller responses.

        if self._stable_counters.undecodable_tunneller_responses > 0:
            # Checks if there are any undecodable tunneller responses in the stable response.
            message += ' but stable downloading has undecodable responses too'
            # Adds a message indicating that the stable downloading also has undecodable responses.

        message += '\n'
        # Adds a newline to separate this section from the next.

    return {
        'name': self.NAME,
        # Returns the name of the checker.
        'description': self.DESCRIPTION,
        # Returns the description of the checker.
        'verdict': verdict,
        # Returns the overall verdict (True if valid, False if invalid).
        'message': message
        # Returns the summary message.
    }
```

```python
class MegamindAnalyticsInfoChecker(Checker):
    # Defines a subclass named `MegamindAnalyticsInfoChecker` that inherits from the `Checker` abstract base class.
    # This class implements specific functionality for checking the presence of `megamind_analytics_info` and `original_utterance`.

    NAME = 'megamind_analytics_info_checker'
    # Defines a class-level constant `NAME` that stores the name of the checker.

    DESCRIPTION = 'checks presence of megamind_analytics_info and original_utterance'
    # Defines a class-level constant `DESCRIPTION` that describes the purpose of the checker.

    class Counters:
        # Defines an inner class named `Counters` to track various statistics during the checking process.

        def __init__(self):
            # Defines the constructor for the `Counters` class.
            self.responses = 0
            # Initializes a counter for the total number of responses.
            self.megamind_analytics_info = 0
            # Initializes a counter for the number of responses containing `megamind_analytics_info`.
            self.original_utterance = 0
            # Initializes a counter for the number of responses containing `original_utterance`.

        def __add__(self, other):
            # Defines the `__add__` method to allow adding two `Counters` instances.
            counters = MegamindAnalyticsInfoChecker.Counters()
            # Creates a new `Counters` instance to store the result of the addition.
            counters.responses = self.responses + other.responses
            # Adds the `responses` counters from both instances.
            counters.megamind_analytics_info = self.megamind_analytics_info + other.megamind_analytics_info
            # Adds the `megamind_analytics_info` counters from both instances.
            counters.original_utterance = self.original_utterance + other.original_utterance
            # Adds the `original_utterance` counters from both instances.
            return counters
            # Returns the new `Counters` instance containing the summed values.

        def __eq__(self, other):
            # Defines the `__eq__` method to compare two `Counters` instances for equality.
            eq = True
            # Initializes a variable `eq` to `True`.
            eq = eq and self.responses == other.responses
            # Checks if the `responses` counters are equal.
            eq = eq and self.megamind_analytics_info == other.megamind_analytics_info
            # Checks if the `megamind_analytics_info` counters are equal.
            eq = eq and self.original_utterance == other.original_utterance
            # Checks if the `original_utterance` counters are equal.
            return eq
            # Returns the result of the equality comparison.

        def __ne__(self, other):
            # Defines the `__ne__` method to compare two `Counters` instances for inequality.
            return not self.__eq__(other)
            # Returns the negation of the `__eq__` method result.

    def __init__(self):
        # Defines the constructor for the `MegamindAnalyticsInfoChecker` class.
        self._test_counters = self.Counters()
        # Initializes a `Counters` instance for tracking test statistics.
        self._stable_counters = self.Counters()
        # Initializes a `Counters` instance for tracking stable statistics.

    def _calc_counters(self, vins_response):
        # Defines a method named `_calc_counters` that calculates counters for a Vins response.
        # The method takes one argument:
        # - `vins_response`: A dictionary containing the Vins response data.

        counters = self.Counters()
        # Creates a new instance of the `Counters` class to track statistics.

        counters.responses += 1
        # Increments the `responses` counter by 1 to track the total number of responses.

        megamind_analytics_info_dict = vins_response.get('directive', {}).get('payload', {}).get(
            'megamind_analytics_info')
        # Retrieves the `megamind_analytics_info` dictionary from the nested structure in `vins_response`.
        # Uses `dict.get` with default values to avoid KeyError if any key is missing.

        if megamind_analytics_info_dict is not None:
            # Checks if `megamind_analytics_info_dict` is not `None`.
            counters.megamind_analytics_info += 1
            # Increments the `megamind_analytics_info` counter by 1.

            if 'original_utterance' in megamind_analytics_info_dict:
                # Checks if the `original_utterance` key exists in `megamind_analytics_info_dict`.
                counters.original_utterance += 1
                # Increments the `original_utterance` counter by 1.

        return counters
        # Returns the `counters` object containing the calculated statistics.

    def process_row(self, row):
        # Defines the `process_row` method, which processes a single row of data.
        # The method takes one argument:
        # - `row`: A dictionary representing a row of data.

        verdict = True
        # Initializes `verdict` to `True`, indicating the row is valid by default.

        message = None
        # Initializes `message` to `None`, which will store a descriptive message if the row is invalid.

        if row.get('test.VinsResponse') and row.get('stable.VinsResponse'):
            # Checks if the row contains both 'test.VinsResponse' and 'stable.VinsResponse' keys.

            row_test_counters = self._calc_counters(json.loads(row['test.VinsResponse']))
            # Parses the 'test.VinsResponse' JSON string and calculates counters using `_calc_counters`.

            self._test_counters += row_test_counters
            # Adds the counters from the test response to the overall test counters.

            row_stable_counters = self._calc_counters(json.loads(row['stable.VinsResponse']))
            # Parses the 'stable.VinsResponse' JSON string and calculates counters using `_calc_counters`.

            self._stable_counters += row_stable_counters
            # Adds the counters from the stable response to the overall stable counters.

            if row_test_counters != row_stable_counters:
                # Checks if the counters for the test and stable responses are not equal.
                verdict = False
                # Sets `verdict` to `False` if the counters differ.

                if row_test_counters.megamind_analytics_info != row_stable_counters.megamind_analytics_info:
                    # Checks if the number of `megamind_analytics_info` entries differs between test and stable.
                    present, absent = 'test', 'stable'
                    # Initializes variables to track which response has the missing data.
                    if row_test_counters.megamind_analytics_info == 0:
                        # Checks if the test response is missing `megamind_analytics_info`.
                        present, absent = absent, present
                        # Swaps `present` and `absent` if the test response is missing the data.
                    message = ('megamind analytics info is present in {} response but absent in {}'.format(present,
                                                                                                           absent))
                    # Sets a descriptive message about the mismatch in `megamind_analytics_info`.

                elif row_test_counters.original_utterance != row_stable_counters.original_utterance:
                    # Checks if the number of `original_utterance` entries differs between test and stable.
                    present, absent = 'test', 'stable'
                    # Initializes variables to track which response has the missing data.
                    if row_test_counters.original_utterance == 0:
                        # Checks if the test response is missing `original_utterance`.
                        present, absent = absent, present
                        # Swaps `present` and `absent` if the test response is missing the data.
                    message = ('original utterance is present in {} response but absent in {}'.format(present,
                                                                                                      absent))
                    # Sets a descriptive message about the mismatch in `original_utterance`.

        elif row.get('test.VinsResponse'):
            # Checks if the row contains only 'test.VinsResponse'.
            self._test_counters += self._calc_counters(json.loads(row['test.VinsResponse']))
            # Parses the 'test.VinsResponse' JSON string and updates the test counters.

            message = 'vins response from stable downloading is empty'
            # Sets a message indicating that the stable response is missing.

        elif row.get('stable.VinsResponse'):
            # Checks if the row contains only 'stable.VinsResponse'.
            self._stable_counters += self._calc_counters(json.loads(row['stable.VinsResponse']))
            # Parses the 'stable.VinsResponse' JSON string and updates the stable counters.

            message = 'vins response from test downloading is empty'
            # Sets a message indicating that the test response is missing.

        return verdict, message
        # Returns a tuple containing:
        # - `verdict`: A boolean indicating whether the row is valid.
        # - `message`: A descriptive message if the row is invalid.

    def dump_result(self):
        # Defines the `dump_result` method, which generates a summary of the checking process.
        # The method takes no arguments.

        verdict = True
        # Initializes `verdict` to `True`, indicating the overall result is valid by default.

        message = ''
        # Initializes `message` to an empty string, which will store the summary message.

        for counters, name in ((self._test_counters, 'test'), (self._stable_counters, 'stable')):
            # Iterates over the test and stable counters.

            message += 'stats of {} downloading:\n'.format(name)
            # Adds a header to the message indicating whether the stats are for test or stable downloading.

            message += 'vins responses: {}\n'.format(counters.responses)
            # Adds the total number of Vins responses to the message.

            message += 'megamind analytics info: {}\n'.format(counters.megamind_analytics_info)
            # Adds the number of responses containing `megamind_analytics_info` to the message.

            message += 'original utterance: {}\n'.format(counters.original_utterance)
            # Adds the number of responses containing `original_utterance` to the message.

            message += '\n'
            # Adds a newline to separate the test and stable stats.

        if (self._test_counters.responses == self._test_counters.megamind_analytics_info) and (
                self._test_counters.responses == self._test_counters.original_utterance):
            # Checks if all responses in the test response contain both `megamind_analytics_info` and `original_utterance`.
            message += 'test downloading is ok'
            # Adds a message indicating that the test downloading is valid.

            if (self._stable_counters.responses != self._stable_counters.megamind_analytics_info) or (
                    self._stable_counters.responses != self._stable_counters.original_utterance):
                # Checks if the stable response is missing `megamind_analytics_info` or `original_utterance`.
                message += (' but some stable downloading vins responses has no megamind analytics info'
                            ' or original utterance')
                # Adds a message indicating that the stable downloading has issues.

            message += '\n'
            # Adds a newline to separate this section from the next.

        if self._test_counters.responses != self._test_counters.megamind_analytics_info:
            # Checks if not all responses in the test response contain `megamind_analytics_info`.
            verdict = False
            # Sets `verdict` to `False`.

            message += 'megamind analytics info is not present in every response of test downloading'
            # Adds a message indicating that `megamind_analytics_info` is missing in some responses.

            message += '\n'
            # Adds a newline to separate this section from the next.

        if self._test_counters.responses != self._test_counters.original_utterance:
            # Checks if not all responses in the test response contain `original_utterance`.
            verdict = False
            # Sets `verdict` to `False`.

            message += 'original utterance is not present in megamind analytics info of test downloading'
            # Adds a message indicating that `original_utterance` is missing in some responses.

            message += '\n'
            # Adds a newline to separate this section from the next.

        return {
            'name': self.NAME,
            # Returns the name of the checker.
            'description': self.DESCRIPTION,
            # Returns the description of the checker.
            'verdict': verdict,
            # Returns the overall verdict (True if valid, False if invalid).
            'message': message
            # Returns the summary message.
        }
```

```python
class MetaChecker(Checker):
    # Defines a subclass named `MetaChecker` that inherits from the `Checker` abstract base class.
    # This class implements specific functionality for checking the non-emptiness of `meta` in Vins responses.

    NAME = 'meta_checker'
    # Defines a class-level constant `NAME` that stores the name of the checker.

    DESCRIPTION = 'checks non emptiness of meta'
    # Defines a class-level constant `DESCRIPTION` that describes the purpose of the checker.

    class Counters:
        # Defines an inner class named `Counters` to track various statistics during the checking process.

        def __init__(self):
            # Defines the constructor for the `Counters` class.
            self.responses = 0
            # Initializes a counter for the total number of responses.
            self.not_empty_metas = 0
            # Initializes a counter for the number of responses with non-empty `meta`.

        def __add__(self, other):
            # Defines the `__add__` method to allow adding two `Counters` instances.
            counters = MetaChecker.Counters()
            # Creates a new `Counters` instance to store the result of the addition.
            counters.responses = self.responses + other.responses
            # Adds the `responses` counters from both instances.
            counters.not_empty_metas = self.not_empty_metas + other.not_empty_metas
            # Adds the `not_empty_metas` counters from both instances.
            return counters
            # Returns the new `Counters` instance containing the summed values.

        def __eq__(self, other):
            # Defines the `__eq__` method to compare two `Counters` instances for equality.
            eq = True
            # Initializes a variable `eq` to `True`.
            eq = eq and self.responses == other.responses
            # Checks if the `responses` counters are equal.
            eq = eq and self.not_empty_metas == other.not_empty_metas
            # Checks if the `not_empty_metas` counters are equal.
            return eq
            # Returns the result of the equality comparison.

        def __ne__(self, other):
            # Defines the `__ne__` method to compare two `Counters` instances for inequality.
            return not self.__eq__(other)
            # Returns the negation of the `__eq__` method result.

    def __init__(self):
        # Defines the constructor for the `MetaChecker` class.
        self._test_counters = self.Counters()
        # Initializes a `Counters` instance for tracking test statistics.
        self._stable_counters = self.Counters()
        # Initializes a `Counters` instance for tracking stable statistics.

    def _calc_counters(self, vins_response):
        # Defines a method named `_calc_counters` that calculates counters for a Vins response.
        # The method takes one argument:
        # - `vins_response`: A dictionary containing the Vins response data.

        counters = self.Counters()
        # Creates a new instance of the `Counters` class to track statistics.

        counters.responses += 1
        # Increments the `responses` counter by 1 to track the total number of responses.

        meta = vins_response.get('directive', {}).get('payload', {}).get('response', {}).get('meta', [])
        # Retrieves the `meta` list from the nested structure in `vins_response`.
        # Uses `dict.get` with default values to avoid KeyError if any key is missing.

        counters.not_empty_metas += int(len(meta) > 0)
        # Increments the `not_empty_metas` counter by 1 if `meta` is not empty.

        return counters
        # Returns the `counters` object containing the calculated statistics.

    def process_row(self, row):
        # Defines the `process_row` method, which processes a single row of data.
        # The method takes one argument:
        # - `row`: A dictionary representing a row of data.

        verdict = True
        # Initializes `verdict` to `True`, indicating the row is valid by default.

        message = None
        # Initializes `message` to `None`, which will store a descriptive message if the row is invalid.

        if row.get('test.VinsResponse') and row.get('stable.VinsResponse'):
            # Checks if the row contains both 'test.VinsResponse' and 'stable.VinsResponse' keys.

            row_test_counters = self._calc_counters(json.loads(row['test.VinsResponse']))
            # Parses the 'test.VinsResponse' JSON string and calculates counters using `_calc_counters`.

            self._test_counters += row_test_counters
            # Adds the counters from the test response to the overall test counters.

            row_stable_counters = self._calc_counters(json.loads(row['stable.VinsResponse']))
            # Parses the 'stable.VinsResponse' JSON string and calculates counters using `_calc_counters`.

            self._stable_counters += row_stable_counters
            # Adds the counters from the stable response to the overall stable counters.

            if row_test_counters != row_stable_counters:
                # Checks if the counters for the test and stable responses are not equal.
                verdict = False
                # Sets `verdict` to `False` if the counters differ.

                if row_test_counters.not_empty_metas != row_stable_counters.not_empty_metas:
                    # Checks if the number of non-empty `meta` entries differs between test and stable.
                    present, absent = 'test', 'stable'
                    # Initializes variables to track which response has the missing data.
                    if row_test_counters.not_empty_metas == 0:
                        # Checks if the test response is missing non-empty `meta`.
                        present, absent = absent, present
                        # Swaps `present` and `absent` if the test response is missing the data.
                    message = ('meta is present in {} response but absent in {}'.format(present,
                                                                                        absent))
                    # Sets a descriptive message about the mismatch in non-empty `meta`.

        elif row.get('test.VinsResponse'):
            # Checks if the row contains only 'test.VinsResponse'.
            self._test_counters += self._calc_counters(json.loads(row['test.VinsResponse']))
            # Parses the 'test.VinsResponse' JSON string and updates the test counters.

            message = 'vins response from stable downloading is empty'
            # Sets a message indicating that the stable response is missing.

        elif row.get('stable.VinsResponse'):
            # Checks if the row contains only 'stable.VinsResponse'.
            self._stable_counters += self._calc_counters(json.loads(row['stable.VinsResponse']))
            # Parses the 'stable.VinsResponse' JSON string and updates the stable counters.

            message = 'vins response from test downloading is empty'
            # Sets a message indicating that the test response is missing.

        return verdict, message
        # Returns a tuple containing:
        # - `verdict`: A boolean indicating whether the row is valid.
        # - `message`: A descriptive message if the row is invalid.

    def dump_result(self):
        # Defines the `dump_result` method, which generates a summary of the checking process.
        # The method takes no arguments.

        verdict = True
        # Initializes `verdict` to `True`, indicating the overall result is valid by default.

        message = ''
        # Initializes `message` to an empty string, which will store the summary message.

        for counters, name in ((self._test_counters, 'test'), (self._stable_counters, 'stable')):
            # Iterates over the test and stable counters.

            message += 'stats of {} downloading\n'.format(name)
            # Adds a header to the message indicating whether the stats are for test or stable downloading.

            message += 'vins responses: {}\n'.format(counters.responses)
            # Adds the total number of Vins responses to the message.

            message += 'not empty metas: {}\n'.format(counters.not_empty_metas)
            # Adds the number of responses with non-empty `meta` to the message.

            message += '\n'
            # Adds a newline to separate the test and stable stats.

        if self._test_counters.responses == self._test_counters.not_empty_metas:
            # Checks if all responses in the test response contain non-empty `meta`.
            message += 'test downloading is ok'
            # Adds a message indicating that the test downloading is valid.

            if self._stable_counters.responses != self._stable_counters.not_empty_metas:
                # Checks if the stable response is missing non-empty `meta`.
                message += ' but some stable downloading vins responses has empty meta'
                # Adds a message indicating that the stable downloading has issues.

            message += '\n'
            # Adds a newline to separate this section from the next.

        else:
            # If not all responses in the test response contain non-empty `meta`, this block executes.
            verdict = False
            # Sets `verdict` to `False`.

            message += 'meta is not present in every response of test downloading'
            # Adds a message indicating that non-empty `meta` is missing in some responses.

            message += '\n'
            # Adds a newline to separate this section from the next.

        return {
            'name': self.NAME,
            # Returns the name of the checker.
            'description': self.DESCRIPTION,
            # Returns the description of the checker.
            'verdict': verdict,
            # Returns the overall verdict (True if valid, False if invalid).
            'message': message
            # Returns the summary message.
        }
```
