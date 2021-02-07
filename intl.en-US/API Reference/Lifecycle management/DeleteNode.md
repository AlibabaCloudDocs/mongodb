# DeleteNode

You can call this operation to delete a shard or mongos node in a sharded cluster instance.

Before you call this operation, make sure that the following requirements are met:

-   The instance is in the running state.
-   The instance is a sharded cluster instance.
-   The billing method of the instance is pay-as-you-go.
-   The number of the shard or mongos nodes in the instance is greater than two.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DeleteNode&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteNode|The operation that you want to perform. Set the value to **DeleteNode**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|NodeId|String|Yes|s-bpxxxxxxxx|The ID of the shard or mongos node to be deleted. You can call the [DescribeDBInstanceAttribute](~~61923~~) operation to query the node ID. |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The token can contain only ASCII characters and cannot exceed 64 characters in length. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OrderId|String|111111111111111|The order ID of the instance. |
|RequestId|String|9F9BDE64-BF30-41F3-BD29-C19CE4AB3404|The ID of the request. |
|TaskId|Integer|111111111|The ID of the task. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DeleteNode
&NodeId=s-bpxxxxxxxx
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<TaskId>111111111</TaskId>
<RequestId>04BDBD93-3B59-496C-8B5E-7FF158E10C5C</RequestId>
<OrderId>111111111111111</OrderId>
```

`JSON` format

```
{
	"TaskId": 111111111,
	"RequestId": "04BDBD93-3B59-496C-8B5E-7FF158E10C5C",
	"OrderId": "111111111111111"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

