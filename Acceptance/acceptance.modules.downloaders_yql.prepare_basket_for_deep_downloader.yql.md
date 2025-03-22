```sql
# PRAGMA directive to set the schema inference limit to 100 rows
PRAGMA yt.InferSchema = '100';

# Define a multi-line string containing the Python code
$code = @@
# Import the base64 module for encoding and decoding data
import base64
# Import the cyson module for working with YSON (Yandex Object Notation) data
import cyson
# Import the json module for working with JSON data
import json
# Import cryptographic modules for encryption and decryption
from cryptography.hazmat.backends import default_backend
from cryptography.hazmat.primitives import serialization
from cryptography.hazmat.primitives.asymmetric import padding
from cryptography.hazmat.primitives import hashes

# Define the size of each partition for encryption
PARTITION_SIZE = 256

# Define the public key as a base64-encoded string
PUBLIC_KEY_STR = (
    b'MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzokOkMWkvbyDU7ZWEH0p'
    b'Hv+K5Hx6efvVgvd42hupk7CZmFGQOLxSOt4PDnS3+cL5FNJzwRPMcKOB+fMdG5BJ'
    b'zfIVtWR8L6SENg/j+QB4vY3d7TeonchfIOP4z2r8FM+K6ekLzXqN/MbVBVdU0W+b'
    b'xC4SV8K3g+Wrrqx0E6y2EzjDjdKaOWZygrnwi5vaM9juZtVEqNwde7UDrHoYgITI'
    b'EOb3VE1UJJZgdW/ypT2F55H/FN7EjCuwIeoyrWKcDyuBhltWdHBE4eUK59K7uYtS'
    b'jli/3GHx2v5uS69PLDQ4ttBWvMHL6jKQ9ihlY/kKDf5toR+imaK+PNuX+x3lyrZx'
    b'/wIDAQAB')

# Define a function to encrypt a message using the public key
def encrypt(message):
    # Ensure the message is not empty
    assert message, 'Empty message for encrypt'
    # Load the public key from the base64-encoded string
    public_key = serialization.load_der_public_key(base64.b64decode(PUBLIC_KEY_STR), backend=default_backend())
    # Initialize an empty byte string to store the result
    result = b''
    # Process the message in chunks of size PARTITION_SIZE
    while(len(message) > 0):
        # Encrypt the current chunk of the message
        ciphertext = public_key.encrypt(
            message[:PARTITION_SIZE],
            padding.OAEP(
                mgf=padding.MGF1(algorithm=hashes.SHA1()),
                algorithm=hashes.SHA1(),
                label=None
            )
        )
        # Remove the processed chunk from the message
        message = message[PARTITION_SIZE:]
        # Encode the ciphertext in base64 and wrap it in markers
        r = b'<--' + base64.b64encode(ciphertext) + b'-->'
        # Append the result to the final output
        result += r
    # Return the encrypted message
    return result

# Define a reducer function to process key-value pairs
def reducer(key, values):
    # Convert each value from YSON to a Python dictionary
    rows = [cyson.loads(v) for v in values]
    # Initialize a flag to determine if the session sequence should be reversed
    use_reversed_session_sequence = False
    # Process each row in the list
    for row in rows:
        # Extract the 'flags' field from the row, defaulting to an empty list
        flags = row.pop(b'flags', [])
        # Check if the 'soy_decrypt_secrets' flag is present
        if b'soy_decrypt_secrets' in flags:
            # Encrypt the 'oauth' field if it exists
            if row.get(b'oauth'):
                row[b'oauth'] = encrypt(row[b'oauth'])
        # Check if the 'use_reversed_session_sequence' flag is present
        if b'use_reversed_session_sequence' in flags:
            use_reversed_session_sequence = True

    # Sort the rows based on the session sequence
    if use_reversed_session_sequence:
        try:
            # Sort in reverse order using the 'reversed_session_sequence' field
            rows.sort(key=lambda t: -t[b'reversed_session_sequence'])
        except KeyError:
            # Fallback to sorting by 'session_sequence' if 'reversed_session_sequence' is missing
            rows.sort(key=lambda t: -t[b'session_sequence'])
    else:
        # Sort in reverse order using the 'session_sequence' field
        rows.sort(key=lambda t: -t[b'session_sequence'])
    # Return the sorted rows and the session ID
    return {'session_requests': cyson.dumps(rows), 'session_id': key}

# Define a function to enrich a row with additional flags
def enrich_row(row, flags):
    # Parse the flags from a JSON string to a Python object
    flags = json.loads(flags)
    # Parse the row from YSON to a Python dictionary
    row = cyson.loads(row)
    # Add the flags to the row
    row['flags'] = flags
    # Convert the row back to YSON format
    return cyson.dumps(row)
@@;

# Define a reducer function using the Python code
$reducer = Python3::reducer(
    # Specify the function signature for the reducer
    Callable<(
        String?,
        Stream<Yson?>
    ) -> Struct<session_requests:Yson?,session_id:String>>,
    # Pass the Python code to the reducer
    $code
);

# Define a function to enrich rows using the Python code
$enrich_row = Python3::enrich_row(
    # Specify the function signature for the enrich_row function
    Callable<(
        Yson?,
        String
    ) -> Yson>,
    # Pass the Python code to the enrich_row function
    $code
);

# Insert the processed data into the output table
INSERT INTO {{output1}} WITH TRUNCATE
# Reduce the input data using the reducer function
REDUCE {{input1}}
# Group the data by the session_id field
ON session_id USING $reducer($enrich_row(Yson::Serialize(Yson::From(TableRow())), {{param.downloader_flags}}));
```
