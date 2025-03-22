```python
# coding: utf-8
# Specifies the encoding of the file as UTF-8 to ensure proper handling of Unicode characters.

import vh
# Imports the `vh` module, which is likely a custom or third-party module for handling data or virtual files.

SINGLE_OPTION_TO_JSON = vh.op(
    # Defines a constant named `SINGLE_OPTION_TO_JSON` that represents a specific operation.
    # This operation is likely used to convert a single option into JSON format.

    id='2fdd4bb4-4303-11e7-89a6-0025909427cc',
    # Specifies the unique identifier (UUID) for this operation.
)

JSON_TO_MR_TABLE_OP = vh.op(
    # Defines a constant named `JSON_TO_MR_TABLE_OP` that represents a specific operation.
    # This operation is likely used to write JSON data into a MapReduce (MR) table.

    name='MR Write JSON to Directory (Create New)',
    # Specifies the human-readable name of the operation.
    id='5fe73009-86d1-4eaf-8c22-50c1f8b3097f',
    # Specifies the unique identifier (UUID) for this operation.
)

MR_TABLE_TO_JSON_OP = vh.op(
    # Defines a constant named `MR_TABLE_TO_JSON_OP` that represents a specific operation.
    # This operation is likely used to read JSON data from a MapReduce (MR) table.

    name='MR Read JSON',
    # Specifies the human-readable name of the operation.
    id='fcf99a2d-500b-407f-8075-f94d5e54a50e',
    # Specifies the unique identifier (UUID) for this operation.
)

YQL_1 = vh.op(
    # Defines a constant named `YQL_1` that represents a specific YQL (Yandex Query Language) operation.

    name='YQL 1',
    # Specifies the human-readable name of the operation.
    id='423ba830-b7e1-464e-9131-e9821a0f4c3c'
    # Specifies the unique identifier (UUID) for this operation.
).partial(yt_table_outputs=['output1'])
# Uses the `partial` method to specify that this operation has one output table named 'output1'.

YQL_2 = vh.op(
    # Defines a constant named `YQL_2` that represents another specific YQL operation.

    name='YQL 2',
    # Specifies the human-readable name of the operation.
    id='c424ef02-de07-4e0e-9c72-334f22ee492d'
    # Specifies the unique identifier (UUID) for this operation.
).partial(yt_table_outputs=['output1', 'output2'])
# Uses the `partial` method to specify that this operation has two output tables named 'output1' and 'output2'.

DEEP_DOWNLOADER_OP = vh.op(
    # Defines a constant named `DEEP_DOWNLOADER_OP` that represents a specific operation.
    # This operation is likely used to perform deep downloading of data.

    id='20956afe-14f4-4fd3-83e6-22bc81447c8f',
    # Specifies the unique identifier (UUID) for this operation.
)
```
