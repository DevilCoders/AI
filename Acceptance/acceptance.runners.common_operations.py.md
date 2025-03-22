```python
# Import the 'vh' module, which is likely a framework for defining and executing data pipelines.
import vh

# Define an operation for building Arcadia projects using a unique ID.
# This operation is used to compile and build code from the Arcadia repository.
build_arcadia_project_op = vh.op(id='95ddb9b8-8777-4946-a015-1737e4219317')

# Define an operation for retrieving MR (MapReduce) tables using a unique ID.
# This operation is used to fetch data from YT (Yandex Table) clusters.
get_mr_table_op = vh.op(id='6ef6b6f1-30c4-4115-b98c-1ca323b50ac0')

# Define an operation for executing YQL (Yandex Query Language) queries using a unique ID.
# This operation is used to process and transform data using YQL.
yql_2_op = vh.op(id='cd0dca17-e564-4e98-984c-fa73da3bc496')

# Define an operation for downloading data for end-to-end testing using a unique ID.
# This operation is used to fetch data from external services for testing purposes.
ue2e_downloader_op = vh.op(id='54cae161-87d7-4d1b-b9aa-3ce69af61834')
```
