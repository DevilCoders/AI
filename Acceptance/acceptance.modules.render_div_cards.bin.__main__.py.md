```python
# Specify the encoding for the script (UTF-8)
# coding: utf-8

# Import the argparse module for parsing command-line arguments
import argparse
# Import the hashlib module for generating hash values
import hashlib
# Import the logging module for logging messages
import logging
# Import the shutil module for file operations (e.g., copying, moving)
import shutil
# Import the tarfile module for working with tar archives
import tarfile
# Import the urllib.parse module for URL parsing and manipulation
import urllib.parse
# Import the uuid module for generating unique identifiers
import uuid
# Import the simplejson module as json for working with JSON data
import simplejson as json

# Import the Queue class for thread-safe queues
from queue import Queue
# Import the b64encode function for base64 encoding
from base64 import b64encode
# Import the Thread class for creating and managing threads
from threading import Thread
# Import the time function for getting the current time
from time import time
# Import the attr module for defining classes with attributes
import attr
# Import the boto3 module for interacting with AWS services
import boto3
# Import the botocore.config module for configuring AWS clients
import botocore.config
# Import the ijson module for iterative JSON parsing
import ijson
# Import the os module for interacting with the operating system
import os
# Import the requests module for making HTTP requests
import requests

# Import the jsonschema module for validating JSON data against schemas
import jsonschema

# Create a logger object for the current module
logger = logging.getLogger(__name__)
# Configure the logging format and level
logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s', level=logging.INFO)
# Set the logging level for the urllib3.connectionpool logger to ERROR to reduce noise
logging.getLogger('urllib3.connectionpool').setLevel(logging.ERROR)
# Set the logging level for the botocore.vendored.requests.packages.urllib3.connectionpool logger to ERROR
logging.getLogger('botocore.vendored.requests.packages.urllib3.connectionpool').setLevel(logging.ERROR)

# Define a JSON schema for validating dialog data
DIALOG_SCHEMA = {
    # Specify the JSON schema version
    '$schema': 'http://json-schema.org/draft-04/schema#',
    # Define the type of the root element as an array
    'type': 'array',
    # Define the schema for each item in the array
    'items': {
        # Use the "anyOf" keyword to allow items to match one of the following schemas
        "anyOf": [
            {
                # Define the first possible schema for an item
                'type': 'object',
                'properties': {
                    # The item must have a 'type' property of type string
                    'type': {'type': 'string'},
                    # The item must have a 'message' property of type object
                    'message': {'type': 'object'}
                }
            },
            {
                # Define the second possible schema for an item
                'type': 'object',
                'properties': {
                    # The item must have a 'type' property of type string
                    'type': {'type': 'string'},
                    # The item must have a 'message' property of type object
                    'message': {
                        'type': 'object',
                        # The 'message' object can have a 'cards' property, which is an array of objects
                        'properties': {'cards': {'type': 'array', 'items': {'type': 'object'}}},
                        # Allow additional properties in the 'message' object
                        'additionalProperties': True
                    }
                }
            }
        ]
    }
}


# Define a frozen (immutable) class for representing a screenshot
@attr.s(frozen=True)
class Screenshot(object):
    # Define an attribute for the file path (type: str)
    file_path = attr.ib(type=str)
    # Define an attribute for the MD5 hash (type: str, default: None)
    md5 = attr.ib(type=str, default=None)


# Define a frozen (immutable) class for representing a rendered item
@attr.s(frozen=True)
class RenderedItem(object):
    # Define an attribute for the dialog (not included in the string representation)
    dialog = attr.ib(repr=False)
    # Define an attribute for the caption (type: str)
    caption = attr.ib()
    # Define an attribute for the S3 key (type: str)
    s3_key = attr.ib()
    # Define an attribute for the file path (type: str)
    file_path = attr.ib()
    # Define an attribute for the index (type: int)
    idx = attr.ib()

    # Define a method to convert the object to a dictionary
    def to_dict(self):
        # Convert the object to a dictionary using attr.asdict
        d = attr.asdict(self)
        # Remove the 'dialog' field from the dictionary
        del d['dialog']
        # Return the resulting dictionary
        return d

    # Define a method to save the file content from an iterator
    def save_file(self, content_iterator):
        # Create an MD5 hasher object
        hasher = hashlib.md5()
        # Initialize a variable to track the content length
        content_length = 0
        # Open the file in write-binary mode
        with open(self.file_path, 'wb') as f:
            # Iterate over the content chunks
            for chunk in content_iterator:
                if chunk:
                    # Update the content length
                    content_length += len(chunk)
                    # Write the chunk to the file
                    f.write(chunk)
                    # Update the MD5 hash with the chunk
                    hasher.update(chunk)
        # Raise an error if the content length is zero
        if content_length == 0:
            raise ValueError('empty screenshot content (length: 0)')
        # Return the hexadecimal digest of the MD5 hash
        return hasher.hexdigest()

    # Define a static method to generate an S3 key based on the caption and dialog
    @staticmethod
    def generate_key_for_s3(caption, dialog):
        # Combine the caption and dialog JSON string (sorted keys) into a single string
        data = caption
        data += json.dumps(dialog, sort_keys=True)
        # Create an MD5 hasher object
        md5 = hashlib.md5()
        # Update the hash with the encoded data
        md5.update(data.encode('utf-8'))
        # Generate a UUID based on the MD5 hash
        key = str(uuid.uuid3(uuid.NAMESPACE_DNS, md5.hexdigest()))
        # Return the S3 key with a prefix
        return 'nirvana/' + key + '.json'

    # Define a static method to create a RenderedItem instance
    @staticmethod
    def create(dialog, caption, file_path, idx):
        # Validate the dialog against the schema
        jsonschema.validate(dialog, DIALOG_SCHEMA)
        # Generate the S3 key
        s3_key = RenderedItem.generate_key_for_s3(caption, dialog)
        # Return a new RenderedItem instance
        return RenderedItem(dialog, caption, s3_key, file_path, idx)


# Define a mutable class for representing an item in the queue
@attr.s
class QueueItem(object):
    # Define an attribute for the screenshot (type: Screenshot, default: None)
    screenshot = attr.ib(type=Screenshot, default=None)
    # Define an attribute to track if the item is done (type: bool, default: False)
    done = attr.ib(type=bool, default=False)
    # Define an attribute for the rendered item (type: RenderedItem, default: None)
    rendered_item = attr.ib(type=RenderedItem, default=None)
    # Define an attribute to track the number of attempts (default: 0)
    attempt = attr.ib(default=0)
    # Define an attribute to store errors (default: an empty list)
    errors = attr.ib(default=attr.Factory(list))


# Define a frozen (immutable) class for representing command-line arguments
@attr.s(frozen=True)
class Args(object):
    # Define an attribute for the renderer
    renderer = attr.ib()
    # Define an attribute for the source file path
    source = attr.ib()
    # Define an attribute for the destination file path
    destination = attr.ib()
    # Define an attribute for the number of threads (converted to int)
    n_threads = attr.ib(converter=int)
    # Define an attribute for the ID key
    id_key = attr.ib()
    # Define an attribute for the dialog key
    dialog_key = attr.ib()
    # Define an attribute for the MD5 destination file path
    md5_destination = attr.ib()
    # Define an attribute for the errors destination file path
    errors_destination = attr.ib()
    # Define an attribute for the maximum number of attempts (converted to int)
    max_attempts = attr.ib(converter=int)


# Define a class for interacting with an S3 bucket
class S3Bucket(object):
    # Define the constructor
    def __init__(self, key_id, access_key, endpoint_url, bucket_name, max_pool=200):
        # Configure the boto3 client with a maximum connection pool size
        boto_config = botocore.config.Config(max_pool_connections=max_pool)
        # Store the endpoint URL
        self.endpoint_url = endpoint_url
        # Create a boto3 session with the provided credentials
        self.session = boto3.session.Session(aws_access_key_id=key_id, aws_secret_access_key=access_key)
        # Create an S3 client with the specified configuration
        self.s3 = self.session.client(service_name='s3', endpoint_url=self.endpoint_url, verify=False, config=boto_config)
        # Store the bucket name
        self.bucket_name = bucket_name

    # Define a method to upload an object to S3
    def put(self, key, value, **kwargs):
        # Upload the object to the specified bucket and key
        self.s3.put_object(Bucket=self.bucket_name, Key=key, Body=value, **kwargs)

    # Define a method to delete an object from S3
    def delete(self, key):
        # Delete the object from the specified bucket and key
        self.s3.delete_object(Bucket=self.bucket_name, Key=key)

    # Define a method to generate a public URL for an object
    def get_public_url(self, key):
        # Construct the host URL by modifying the endpoint URL
        host = self.endpoint_url.replace('mds.', '').replace('http://', '').replace('https://', '')
        # Construct the base URL for the bucket
        url = 'http://{bucket}.{host}'.format(bucket=self.bucket_name, host=host)
        # Join the base URL with the object key to form the full URL
        return urllib.parse.urljoin(url, key)


# Define a class for interacting with the Rotor API
class RotorApi(object):
    # Define the connection timeout
    CONN_TIMEOUT = 0.5
    # Define the snapshot timeout
    SNAPSHOT_TIMEOUT = 1
    # Create a requests session with custom headers
    SESSION = requests.Session()
    SESSION.headers.update({
        'Content-Type': 'application/json',
        # Close the connection after each request to avoid 502 errors
        'Connection': 'close',
    })

    # Define the constructor
    def __init__(self, server, source, rotor_timeout, tvm_secret=None):
        # Construct the handler URL by joining the server URL with the API endpoint
        self.handler = urllib.parse.urljoin(server, 'v1/rotor/execute/png')
        # Store the source (quota) for the API
        self.source = source
        # Store the rotor processing timeout
        self.process_timeout = rotor_timeout
        # Calculate the total timeout (connection + snapshot)
        self.timeout = (self.CONN_TIMEOUT, rotor_timeout + self.SNAPSHOT_TIMEOUT)
        # Store the TVM secret (if provided)
        self.tvm_secret = tvm_secret

    # Define a method to get a response from the Rotor API
    def get_response(self, url):
        # Define the payload for the API request
        payload = {
            'Url': url,
            'Source': self.source,
            'Timeout': self.process_timeout,
            'Options': {
                'OutputFormat': {
                    'Html': False,
                    'Png': True
                },
                'ViewPortSize': {
                    'Width': 350,
                    'Height': 250
                },  # See ScreenshotMode
                'EnableImages': True,
                'ScreenshotMode': 1,  # 0 - Viewport only, 1 - Full visible
                'SnapshotTimeoutSeconds': self.SNAPSHOT_TIMEOUT
            }
        }
        # Add the TVM service ticket to the payload if provided
        if self.tvm_secret:
            payload['TvmServiceTicket'] = self.tvm_secret

        # Send the POST request to the Rotor API
        response = self.SESSION.post(self.handler, json=payload, timeout=self.timeout)
        # Close the connection to avoid 502 errors
        response.connection.close()
        # Raise an error if the response status code is not 200
        if response.status_code != 200:
            error_message = 'Response code {0} / rotor status: {1} / rotor httpcode: {2}'.format(
                response.status_code,
                response.headers.get('X-Rotor-Status', 'No X-Rotor-Status'),
                response.headers.get('X-Rotor-HttpCode', 'No X-Rotor-HttpCode')
            )
            # Append the response text to the error message if available
            if response.text:
                error_message = '{0} - {1}'.format(error_message, response.text)
            raise ValueError(error_message)
        # Return the response
        return response


# Define a class for rendering screenshots
class Renderer(object):
    # Define the constructor
    def __init__(self, rotor_client, s3_bucket, div2html_url):
        # Store the Rotor client
        self.rotor = rotor_client
        # Store the S3 bucket
        self.s3_bucket = s3_bucket
        # Store the div2html URL
        self.div2html_url = div2html_url

    # Define a method to render a screenshot
    def render(self, data):
        # Extract the rendered item from the data
        item = data.rendered_item
        # Construct the URL for the div2html service
        url = self.div2html_url + f'?url={self.s3_bucket.get_public_url(item.s3_key)}'
        try:
            # Record the start time
            past = time()
            # Upload the dialog to S3
            self.s3_bucket.put(item.s3_key, json.dumps(item.dialog))
            # Log the upload completion
            logger.info('Uploaded: {0} / {1} / {2}'.format(item.idx, item.caption, time() - past))

            # Record the start time
            past = time()
            # Log the request to the Rotor API
            logger.info('Asking rotor api %s %s / %s', url, item.idx, item.caption)
            # Get the response from the Rotor API and create an iterator for the content
            iterator = self.rotor.get_response(url).iter_content(chunk_size=4 * 1024)
            # Log the rendering completion
            logger.info('Rendered: {0} / {1} / {2} / {3}'.format(item.idx, url, item.caption, time() - past))

            # Record the start time
            past = time()
            # Save the file and get the MD5 hash
            md5 = item.save_file(iterator)
            # Log the file save completion
            logger.info('Saved: {0} / {1} / {2}'.format(item.idx, item.caption, time() - past))
            # Return a Screenshot object
            return Screenshot(item.file_path, md5)
        except Exception as e:
            # Log any exceptions that occur during rendering
            logger.error(
                'Rendering screenshot {idx} / {caption} attempt {attempt} {url} exception\n{error_type}: {error}'.format(
                    idx=item.idx,
                    caption=item.caption,
                    url=url,
                    error_type=type(e),
                    error=str(e),
                    attempt=data.attempt,
                )
            )
            # Re-raise the exception
            raise


# Define a function to prepare a folder by clearing it if it exists
def prepare_folder(folder):
    if os.path.exists(folder):
        shutil.rmtree(folder)
    os.mkdir(folder)


# Define a function to clear a folder
def clear_folder(folder):
    shutil.rmtree(folder)


# Define a function to get an environment variable with a prefix
def env(env_key):
    return os.getenv('DIV2HTML_' + env_key)


# Define a custom argparse action to validate required arguments
class ValidateAction(argparse.Action):
    def __call__(self, parser, namespace, values, option_string=None):
        if not values:
            raise ValueError('Argument {} is required'.format(option_string))
        setattr(namespace, self.dest, values)


# Define a function to parse command-line arguments
def parse_args():
    # Create an argument parser
    parser = argparse.ArgumentParser()
    # Add arguments for S3 credentials, endpoint, bucket, TVM, Rotor, and file paths
    parser.add_argument('--key_id', help='S3 Access Key Id', default=env('S3_KEY_ID'), action=ValidateAction)
    parser.add_argument('--access_key', help='S3 Access Secret Key', default=env('S3_SECRET_KEY'), action=ValidateAction)
    parser.add_argument('--endpoint_url', help='S3 endpoint url', default=env('S3_ENDPOINT'), action=ValidateAction)
    parser.add_argument('--client_id', help='TVM Client Id', default=env('TVM_CLIENT_ID'), action=ValidateAction)
    parser.add_argument('--client_secret', help='TVM Client Secret', default=env('TVM_CLIENT_SECRET'), action=ValidateAction)
    parser.add_argument('--bucket_name', help='S3 bucket name', default=env('S3_BUCKET'), action=ValidateAction)
    parser.add_argument('--rotor_server', help='Rotor server', default=env('ROTOR_SERVER'), action=ValidateAction)
    parser.add_argument('--zora_source', help='Zora source (aka quota)', default=env('ZORA_SOURCE'), action=ValidateAction)
    parser.add_argument('--rotor_timeout', default=12, help='Rotor processing timeout')
    parser.add_argument('--id_key', default='key', help='Unique identifier of object')
    parser.add_argument('--dialog_key', default='dialog', help='Dialog of object')
    parser.add_argument('--div2html_url', default='http://div2html.s3.yandex.net/test/dialog.html',
                        help='Url of div2html service')
    parser.add_argument('--source', help='Path to source file')
    parser.add_argument('--destination', help='Path to result file', default=env('DESTINATION'), action=ValidateAction)
    parser.add_argument('--md5_destination', help='Path to md5 file', default=env('MD5_DESTINATION'), action=ValidateAction)
    parser.add_argument('--errors_destination', help='Path to file with errors',
                        default=env('ERRORS_DESTINATION'), action=ValidateAction)
    parser.add_argument('--n_threads', default=10, help='Number of threads')
    parser.add_argument('--max-attempts', default=10, help='Number of attempts to render per screenshot')
    # Parse the arguments
    args = parser.parse_args()

    # Extract the key ID and access key
    key_id = args.key_id
    access_key = args.access_key
    # Encode the TVM client ID and secret
    client_id = args.client_id.encode('utf-8')
    client_secret = args.client_secret.encode('utf-8')

    # Generate the TVM secret if the client secret is provided
    tvm_secret = b64encode(client_id + client_secret) if client_secret and client_secret else None

    # Set the number of threads (hardcoded to 250 for this example)
    n_threads = 250
    # Extract the Zora source
    zora_source = args.zora_source
    # Log the number of threads
    logger.info('Threads number: {0}'.format(n_threads))

    # Create an S3 bucket instance
    bucket = S3Bucket(key_id, access_key, args.endpoint_url, args.bucket_name, max_pool=n_threads * 3)
    # Log the bucket parameters
    logger.info('Bucket with parameters endpoint url: "{0}", bucket name: "{1}" is used'.format(args.endpoint_url,
                                                                                                args.bucket_name))
    # Create a Rotor API instance
    rotor = RotorApi(args.rotor_server, zora_source, int(args.rotor_timeout), tvm_secret)
    # Log the Rotor API parameters
    logger.info('Rotor api with parameters server: "{0}", source: "{1}", timeout: "{2}" is used'.format(
        args.rotor_server, zora_source, args.rotor_timeout,
    ))
    # Create a Renderer instance
    renderer = Renderer(rotor, bucket, args.div2html_url)

    # Return an Args instance with the parsed arguments
    return Args(
        renderer=renderer,
        source=args.source,
        destination=args.destination,
        n_threads=n_threads,
        id_key=args.id_key,
        dialog_key=args.dialog_key,
        md5_destination=args.md5_destination,
        errors_destination=args.errors_destination,
        max_attempts=int(args.max_attempts)
    )


# Define a generator function to read items from the source file
def read_generator(source, folder, id_key, dialog_key):
    # Open the source file in read-binary mode
    with open(source, 'rb') as input_file:
        # Iterate over the items in the file using ijson
        for i, item in enumerate(ijson.items(input_file, "item")):
            # Extract the dialog and caption
            dialog = item[dialog_key]
            caption = urllib.parse.quote_plus(str(item[id_key]))
            # Construct the file path for the screenshot
            file_path = folder + '/' + caption + '.png'
            # Log the generated dialog
            logger.info('Generated dialog: {0} / {1}'.format(i, caption))
            # Yield a RenderedItem instance
            yield RenderedItem.create(dialog, caption, file_path, i)


# Define the main function
def main():
    # Parse the command-line arguments
    args = parse_args()
    # Extract the folder name from the destination path
    folder = os.path.basename(args.destination).split('.')[0]
    # Prepare the folder
    prepare_folder(folder)
    # Log the start of the process
    logger.info('Starting')

    # Create input and output queues
    input_queue = Queue(2 * args.n_threads)
    output_queue = Queue()

    # Define a worker function for the threads
    def worker():
        while True:
            # Get an item from the input queue
            item = input_queue.get()
            if item is None:
                break
            try:
                # Render the screenshot
                item.screenshot = args.renderer.render(item)

            except Exception as e:
                # Log any exceptions that occur during rendering
                logger.exception('Error: {0} / {1}'.format(item.rendered_item.idx, e))
                # Mark the item as not done
                item.done = False
                # Increment the attempt count
                item.attempt += 1
                # Add the error message to the errors list
                item.errors.append(str(e))

                # Put the item in the output queue
                output_queue.put(item)
            else:
                # Mark the item as done
                item.done = True
                # Put the item in the output queue
                output_queue.put(item)
            # Mark the task as done in the input queue
            input_queue.task_done()

    # Create and start the worker threads
    threads = []
    for i in range(args.n_threads):
        thread = Thread(target=worker)
        thread.daemon = True
        thread.start()
        threads.append(thread)

    # Initialize counters and lists for tracking progress
    total_items = 0
    total_done = 0
    file_paths = []
    hashes = {}
    errors = []

    # Define a function to process file hashes
    def process_file_hash(fh):
        file_path, md5 = fh.screenshot.file_path, fh.screenshot.md5
        file_paths.append(file_path)
        key = file_path.split('/')[-1]
        hashes[key] = md5

    # Define a function to process failed screenshots
    def process_failed_screenshot(item):
        errors.append({
            'idx': item.rendered_item.idx,
            'data': item.rendered_item.to_dict(),
            'errors': item.errors,
        })

    # Define a function to process the output queue
    def process_output_queue():
        number = 0
        while not output_queue.empty():
            # Get an item from the output queue
            item = output_queue.get()

            if item.done:
                number += 1
                process_file_hash(item)
            else:
                if item.attempt < args.max_attempts:
                    input_queue.put(item, block=True)
                else:
                    logger.error('Max attempts %s exceeded for item %s', args.max_attempts, item)
                    process_failed_screenshot(item)
                    number += 1
            output_queue.task_done()
        return number

    # Read items from the source file and add them to the input queue
    for el in read_generator(args.source, folder, args.id_key, args.dialog_key):
        total_items += 1
        input_queue.put(QueueItem(rendered_item=el), block=True)
        total_done += process_output_queue()

    # Log that all input items are in the queue
    logger.info('All input items in queue, waiting for the end of processing.')
    # Process the output queue until all items are done
    while total_done < total_items:
        total_done += process_output_queue()

    # Wait for the input and output queues to finish
    input_queue.join()
    output_queue.join()
    # Signal the worker threads to exit
    for i in range(args.n_threads):
        input_queue.put(None)
    # Wait for all threads to finish
    for thread in threads:
        thread.join()

    # Create a tar archive of the rendered screenshots
    with tarfile.TarFile.gzopen(args.destination, mode='w', compresslevel=0) as tar:
        for file_path in file_paths:
            tar.add(file_path)

    # Save the MD5 hashes to a file
    with open(args.md5_destination, mode='w') as f:
        json.dump(hashes, f)

    # Save the errors to a file
    with open(args.errors_destination, mode='w') as f:
        json.dump(errors, f)

    # Clear the folder
    clear_folder(folder)
    # Log the completion of the process
    logger.info('Finished: {0}'.format(total_items))


# Run the main function if the script is executed directly
if __name__ == "__main__":
    main()
```
