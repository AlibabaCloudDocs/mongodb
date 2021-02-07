# DeleteDBInstance

You can call this operation to release a MongoDB instance.

Ensure that the instance meets the following conditions when you call this operation:

-   The instance is in the running state.
-   The billing method of the instance is pay-as-you-go.

**Note:** After an instance is released, all the data in the instance is lost and cannot be retrieved. Exercise caution when you release instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DeleteDBInstance&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteDBInstance|The operation that you want to perform. Set the value to **DeleteDBInstance**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The token can contain only ASCII characters and cannot exceed 64 characters in length. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|72651AF9-7897-41A7-8B67-6C15C7F26A0A|The ID of the request. |

## Examples

Sample request

```
http(s)://mongodb.aliyuncs.com/? Action=DeleteDBInstance
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteDBInstanceResponse>
	  <RequestId>72651AF9-7897-41A7-8B67-6C15C7F26A0A</RequestId>
</DeleteDBInstanceResponse>
```

`JSON` format

```
{
	"RequestId": "72651AF9-7897-41A7-8B67-6C15C7F26A0A"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

