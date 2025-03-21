```python
import re  # Import the regular expressions module for string manipulation
import yt.wrapper as yt  # Import the YT wrapper module for working with Yandex Table (YT)
import argparse  # Import the argparse module for parsing command-line arguments
import random  # Import the random module for generating random numbers
from itertools import zip_longest  # Import zip_longest for iterating over multiple lists in parallel, filling missing values with a default

# Import custom modules for text preprocessing
from alice.boltalka.tools.dssm_preprocessing.preprocessing.lib.main import TwitterCleaner, TextNormalizer

SEED = 57  # Set a seed for random number generation to ensure reproducibility
MIN_CONTEXT_LEN = 6  # Define the minimum length of a context (sequence of words)
MAX_CONTEXT_LEN = 9  # Define the maximum length of a context (sequence of words)
NEG_NUM = 1  # Define the number of negative samples to generate for each context

def reverse(context):  # Define a function to reverse a context (sequence of words)
    return "reverse", list(reversed(context))  # Return a tuple with the operation name ("reverse") and the reversed context

def dropout(context):  # Define a function to randomly drop a word from a context
    dropout = random.randint(1, len(context) - 2)  # Randomly choose an index to drop (excluding the first and last words)
    return f"dropout{dropout}", context[:dropout] + context[dropout + 1:]  # Return a tuple with the operation name (e.g., "dropout3") and the context with the dropped word
```

```python
def replace(context, neg_type, negatives):  # Define a function to replace a word in the context with a negative sample
    idx = random.randint(0, len(context) - 1)  # Randomly choose an index in the context to replace
    utterance = random.choice(negatives)  # Randomly select a negative sample from the provided list
    context = context[:]  # Create a copy of the context to avoid modifying the original
    context[idx] = utterance  # Replace the word at the chosen index with the negative sample
    return f"replace{idx}{neg_type}", context  # Return a tuple with the operation name (e.g., "replace2neg_type") and the modified context

def swap(context):  # Define a function to swap two words in the context
    choices = list(range(len(context)))  # Create a list of indices for the context
    a = random.choice(choices)  # Randomly choose the first index to swap
    b = random.choice([i for i in choices if i != a])  # Randomly choose a second index to swap (must be different from the first)
    context = context[:]  # Create a copy of the context to avoid modifying the original
    context[a], context[b] = context[b], context[a]  # Swap the words at the chosen indices
    return f"swap{a}w{b}", context  # Return a tuple with the operation name (e.g., "swap1w3") and the modified context
```

```python
def sample_negative(context, tree_negatives, easy_negatives):  # Define a function to sample a negative example from the context
    if random.random() < 0.25:  # With a 25% probability, reverse the context
        return reverse(context)  # Return the reversed context and the operation name
    if len(context) > MIN_CONTEXT_LEN and random.random() < 0.33:  # If the context is longer than the minimum length and with a 33% probability, perform dropout
        return dropout(context)  # Return the context with a dropped word and the operation name
    if random.random() < 0.5:  # With a 50% probability, swap two words in the context
        return swap(context)  # Return the context with swapped words and the operation name
    if tree_negatives and random.random() < 0.7:  # If tree negatives are available and with a 70% probability, replace a word with a tree negative
        return replace(context, 'tree', tree_negatives)  # Return the context with a replaced word and the operation name
    return replace(context, 'easy', easy_negatives)  # If none of the above conditions are met, replace a word with an easy negative and return the result
```

```python
class SessionFilter:  # Define a class to filter and process sessions of text data
    def __init__(self):  # Define the constructor for the SessionFilter class
        # Initialize the TwitterCleaner with specific cleaning options
        self.twitter_cleaner = TwitterCleaner(argparse.Namespace(
            skip_rt=True,  # Skip retweets
            skip_url=True,  # Skip URLs
            skip_hashtag=True,  # Skip hashtags
            skip_new_post=True,  # Skip new posts
            strip_mention=True,  # Strip mentions (e.g., @username)
            skip_at=False,  # Do not skip @ symbols
            replace_html_entities=True  # Replace HTML entities (e.g., &amp;)
        ))
        # Initialize the TextNormalizer with specific normalization options
        self.normalizer = TextNormalizer(argparse.Namespace(
            lang='ru',  # Set the language to Russian
            strip_bad_chars=True,  # Strip bad characters
            separate_punctuation=True,  # Separate punctuation from words
            remove_punctuation=False,  # Do not remove punctuation
            lowercase=True,  # Convert text to lowercase
            uppercase_first=False,  # Do not uppercase the first letter
            replace_yo=True,  # Replace 'ё' with 'е'
            strip_ext=False,  # Do not strip extended characters
            skip_140=False,  # Do not skip text longer than 140 characters
            skip_numeric_many=False  # Do not skip text with many numeric characters
        ))

    def __call__(self, row):  # Define the callable method to process a row of data
        session = row['value']  # Extract the session text from the row
        langs = row['langs']  # Extract the language information from the row
        key = row['key']  # Extract the key from the row
        if langs:  # If language information is available
            langs = langs.split('\t')  # Split the language information into a list
        cur_session = []  # Initialize a list to store the current session's turns
        prev_user = None  # Initialize a variable to track the previous user

    def get_row(session):  # Define a helper function to create a row from a session
        return dict(key=hash(key), session='\n'.join(session), head=session[0])  # Return a dictionary with the session data

        for i, turn in enumerate(session.split('\t')):  # Iterate over each turn in the session
            user, turn = turn.split(' ', 1)  # Split the turn into user and text
            turn = self.twitter_cleaner(turn) or ''  # Clean the turn using TwitterCleaner
            turn = self.normalizer(turn)  # Normalize the turn using TextNormalizer
            bad_turn = not turn or (langs and langs[i] != 'ru')  # Check if the turn is invalid or not in Russian
            if user == prev_user or bad_turn:  # If the user is the same as the previous user or the turn is bad
                if len(cur_session) >= MIN_CONTEXT_LEN:  # If the current session meets the minimum length requirement
                    yield get_row(cur_session)  # Yield the current session as a row
                cur_session = []  # Reset the current session
            if not bad_turn:  # If the turn is valid
                cur_session.append(turn)  # Add the turn to the current session
            prev_user = user  # Update the previous user
        if len(cur_session) >= MIN_CONTEXT_LEN:  # If the final session meets the minimum length requirement
            yield get_row(cur_session)  # Yield the final session as a row
```

```python
class PrefixSuppressor:  # Define a class to suppress rows with duplicate prefixes in sessions
    def __call__(self, key, rows):  # Define the callable method to process rows
        # Expects rows to be reduced by the first turn and sorted by session
        prev_session = None  # Initialize a variable to store the previous session
        prev_row = None  # Initialize a variable to store the previous row
        for row in rows:  # Iterate over each row
            cur_session = row['session'].split('\n')  # Split the current session into turns
            if prev_session is not None:  # If there is a previous session
                for i in range(len(prev_session)):  # Compare each turn in the previous session
                    if i >= len(cur_session) or cur_session[i] != prev_session[i]:  # If the turns differ
                        yield prev_row  # Yield the previous row
                        break  # Stop comparing further turns
            prev_session = cur_session  # Update the previous session
            prev_row = row  # Update the previous row
        if prev_session:  # If there is a final session
            yield prev_row  # Yield the final row


@yt.with_context  # Decorate the class to enable YT context support
class PairIdAssigner(object):  # Define a class to assign batch indices to rows
    def __call__(self, row, context):  # Define the callable method to process a row with context
        row['batch_idx'] = int(context.row_index) // 2  # Assign a batch index based on the row index
        yield row  # Yield the modified row


SENTENCE_REGEXP = re.compile(r'((?:[?!.]+\s*)+)')  # Define a regex to split text into sentences based on punctuation


def default_splitter(row):  # Define a default splitter function to split a session into turns
    return row['session'].split('\n')  # Split the session by newline characters


def megabart_splitter(row):  # Define a custom splitter function for MegaBART
    session = row['text']  # Extract the text from the row
    if '[SEP]' in session:  # If the session contains the '[SEP]' delimiter
        return [el.strip() for el in session.split('[SEP]')]  # Split the session by '[SEP]' and strip whitespace
    else:  # If the session does not contain '[SEP]'
        session = session.lower()  # Convert the session to lowercase
        sentences = SENTENCE_REGEXP.split(session)  # Split the session into sentences using the regex
        # Combine sentences into pairs and strip whitespace
        return [a.strip() + b.strip() for a, b in zip_longest(sentences[::2], sentences[1::2], fillvalue='') if a]


SPLITTERS = dict(  # Define a dictionary of available splitters
    default=default_splitter,  # Map 'default' to the default splitter
    megabart=megabart_splitter  # Map 'megabart' to the MegaBART splitter
)
```

```python
class NegativesSampler(object):  # Define a class to sample negative examples for a given session
    def __init__(self, splitter, full_sessions):  # Define the constructor
        self.splitter = splitter  # Store the splitter function to use for splitting sessions
        self.full_sessions = full_sessions  # Store whether to process full sessions or sliding windows

    def process(self, session, easy_negatives, begin, end):  # Define a method to process a session
        context = session[begin:end]  # Extract the context (subset of the session)
        yield dict(Text=context, sample_type='pos', target=1)  # Yield the positive example (context itself)
        tree_negatives = session[:begin] + session[end:]  # Create tree negatives from the remaining parts of the session
        for neg_idx in range(NEG_NUM):  # Generate the specified number of negative examples
            sample_type, neg_context = sample_negative(context, tree_negatives, easy_negatives)  # Sample a negative example
            yield dict(Text=neg_context, sample_type=sample_type, target=0)  # Yield the negative example

    def __call__(self, key, rows):  # Define the callable method to process rows
        pair_idx = key['batch_idx']  # Extract the batch index from the key
        rows = list(rows)  # Convert rows to a list
        if len(rows) != 2:  # If there are not exactly two rows, skip processing
            return
        rows = [SPLITTERS[self.splitter](el) for el in rows]  # Split each row into turns using the specified splitter
        random.seed(SEED + pair_idx)  # Set the random seed for reproducibility
        for session, easy_negatives in [rows, reversed(rows)]:  # Process each session and its reversed counterpart
            if self.full_sessions:  # If processing full sessions
                yield from self.process(session, easy_negatives, 0, len(session))  # Process the entire session
            else:  # If processing sliding windows
                if len(session) < MIN_CONTEXT_LEN:  # Skip sessions shorter than the minimum context length
                    continue
                for end in range(MIN_CONTEXT_LEN, len(session)):  # Iterate over possible end positions
                    begin = max(0, end - MAX_CONTEXT_LEN)  # Calculate the start position for the context
                    yield from self.process(session, easy_negatives, begin, end)  # Process the context window


def run(args):  # Define a function to run the preprocessing or generation pipeline
    if args.mode == 'preprocess':  # If the mode is preprocessing
        # Run a map-reduce job to filter and suppress duplicate prefixes
        yt.run_map_reduce(SessionFilter(), PrefixSuppressor(), args.src, args.dst, reduce_by='head', sort_by=('head', 'session'))
    elif args.mode == 'generate':  # If the mode is generating negative examples
        # Run a map-reduce job to assign batch indices and sample negatives
        yt.run_map_reduce(PairIdAssigner(), NegativesSampler(args.splitter, args.full_sessions), args.src, args.dst, reduce_by='batch_idx',
                          spec={'map_job_io': {'control_attributes': {'enable_row_index': True}}})


def main():  # Define the main function to parse arguments and run the pipeline
    parser = argparse.ArgumentParser(add_help=True)  # Create an argument parser
    parser.add_argument('mode')  # Add an argument for the mode (preprocess or generate)
    parser.add_argument('--src', required=True)  # Add an argument for the source path (input data)
    parser.add_argument('--dst', required=True)  # Add an argument for the destination path (output data)
    parser.add_argument('--splitter', default='default', choices=['default', 'megabart'])  # Add an argument for the splitter
    parser.add_argument('--full-sessions', action='store_true')  # Add an argument to process full sessions
    args = parser.parse_args()  # Parse the command-line arguments
    run(args)  # Run the pipeline with the parsed arguments
```
