# UpgradeDBInstanceKernelVersion

You can call this operation to upgrade the minor database version of a MongoDB instance.

The instance must be in the running state when you call this operation.

**Note:**

-   This operation is applicable to replica set instances and sharded cluster instances. UpgradeDBInstanceKernelVersion cannot be performed on standalone instances.
-   The instance will be restarted once during the upgrade. Perform this operation during off-peak hours.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=UpgradeDBInstanceKernelVersion&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpgradeDBInstanceKernelVersion|The operation that you want to perform. Set the value to **UpgradeDBInstanceKernelVersion**. |
|DBInstanceId|String|No|dds-bpxxxxxxxx|The ID of the instance. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|27B9A130-7C4B-40D9-84E8-2FC081097AAC|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=UpgradeDBInstanceKernelVersion
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UpgradeDBInstanceKernelVersionResponse>
	  <RequestId>27B9A130-7C4B-40D9-84E8-2FC081097AAC</RequestId>
</UpgradeDBInstanceKernelVersionResponse>
```

`JSON` format

```
{
	"RequestId": "27B9A130-7C4B-40D9-84E8-2FC081097AAC"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

