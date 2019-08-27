# DeleteNode {#doc_api_Dds_DeleteNode .reference}

You can call this operation to delete a shard or mongos in a sharded cluster instance of ApsaraDB for MongoDB.

Ensure that the instance meets the following conditions when you call this operation:

-   The instance is in the running state.
-   The instance type is sharded cluster.
-   The billing method of the instance is Pay-As-You-Go.
-   The number of shards or mongos in the instance must be greater than two.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DeleteNode) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteNode|The operation that you want to perform. Set the value to **DeleteNode**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|NodeId|String|Yes|s-bpxxxxxxxx|The ID of the shard or mongos to be deleted. You can call the [DescribeDBInstanceAttribute](~~61923~~) operation to query the ID.

 |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure idempotence of the request. You can use the client to generate this value, but you must ensure that it is unique among different requests. The token can contain only ASCII characters, and cannot exceed 64 characters in length.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|9F9BDE64-BF30-41F3-BD29-C19CE4AB3404|The ID of the request.

 |
|TaskId|Integer|111111111|The ID of the task.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DeleteNode
&NodeId=s-bpxxxxxxxx
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DeleteNodeResponse>
  <RequestId>9F9BDE64-BF30-41F3-BD29-C19CE4AB3404</RequestId>
  <TaskId>111111111</TaskId>
</DeleteNodeResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"9F9BDE64-BF30-41F3-BD29-C19CE4AB3404",
	"TaskId":111111111
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

