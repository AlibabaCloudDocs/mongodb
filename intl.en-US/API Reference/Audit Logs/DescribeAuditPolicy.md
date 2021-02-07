# DescribeAuditPolicy

You can call this operation to query whether the log audit feature is enabled for a MongoDB instance.

-   The instance must be in the running state when you call this operation.
-   This operation is applicable to replica set instances and sharded cluster instances, but cannot be performed on standalone instances.
-   You can call this operation up to 30 times per minute. To call this operation at a higher frequency, use a Logstore. For more information, see [Manage a Logstore](~~48990~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeAuditPolicy&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAuditPolicy|The operation that you want to perform. Set the value to **DescribeAuditPolicy**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|LogAuditStatus|String|Enable|The status of the log audit feature. Valid values:

 -   Enable
-   Disabled

 Default value: Disabled. |
|RequestId|String|111E7B16-0A87-4CBA-B271-F34AD61E099F|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeAuditPolicy
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` fomat

```
<DescribeAuditPolicyResponse>
	  <LogAuditStatus>Enable</LogAuditStatus>
	  <RequestId>111E7B16-0A87-4CBA-B271-F34AD61E099F</RequestId>
</DescribeAuditPolicyResponse>
```

`JSON` format

```
{
	"LogAuditStatus": "Enable",
	"RequestId": "111E7B16-0A87-4CBA-B271-F34AD61E099F"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

