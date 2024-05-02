### Basic Usage

1. Paginators are created via the `get_paginator()` method of a boto3 client. The `get_paginator()` method accepts an operation name and returns a reusable `Paginator` object. 
2. You then call the `paginate` method of the Paginator, passing in any relevant operation parameters to apply to the underlying API operation. 
3. The `paginate` method then returns an iterable `PageIterator`
4. You must call the `paginate` method of a Paginator in order to iterate over the pages of API operation results. 

```python
def get_all_object_keys_from_s3(s3_client, bucket_name: str) -> list[str]:
    s3_paginator = s3_client.get_paginator('list_objects_v2')
    s3_page_iterator = s3_paginator.paginate(Bucket=bucket_name)
    
    return [object_summary['Key']
           for page in s3_page_iterator
           for object_summary in page['Contents']]
```

### Customizing the Pagination

The `paginate` method accepts a `PaginationConfig` named argument that can be used to customize the pagination.

```python
paginator = client.get_paginator('list_objects_v2')
page_iterator = paginator.paginate(Bucket='my-bucket',
                                   PaginationConfig={'MaxItems': 10})
```

### Parameter Forwarding
Many Paginators can be filtered server-side with options that are passed through to each underlying API call.

```python
def get_all_execution_names(sfn_client, state_machine_arn: str) -> list[str]:
    sfn_paginator = sfn_client.get_paginator('list_executions')
    response_iterator = sfn_paginator.paginate(
        stateMachineArn=state_machine_arn,
        statusFilter='SUCCEEDED',
        maxResults=1000
    )

    return [execution_data['name']
		   for page in response_iterator
           for execution_data in page['executions']]
```