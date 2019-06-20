# RestoreDBInstance {#doc_api_Dds_RestoreDBInstance .reference}

You can call this operation to restore data to the current MongoDB instance.

This operation is only applicable to replica set instances. RestoreDBInstance cannot be performed on standalone instances or sharded cluster instances. You can use the following methods to clone a standalone instance: [Create an instance based on a backup](~~55013~~). Call [CreateShardingDBInstance](~~61884~~) to clone a sharded cluster instance.

**Note:** This operation overwrites the data of the current instance, and the data cannot be recovered. Exercise caution when performing this operation.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=RestoreDBInstance) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RestoreDBInstance|The operation that you want to perform. Set the value to **RestoreDBInstance**.

 |
|BackupId|Integer|Yes|11111111|The ID of the backup.

 **Note:** Call [DescribeBackups](~~62172~~) to query the backup ID.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|973DCB8F-56B3-4102-8777-3A90495927F7|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=RestoreDBInstance
&BackupId=11111111
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<RestoreDBInstanceResponse> 
  <RequestId>973DCB8F-56B3-4102-8777-3A90495927F7</RequestId> 
</RestoreDBInstanceResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"973DCB8F-56B3-4102-8777-3A90495927F7"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

