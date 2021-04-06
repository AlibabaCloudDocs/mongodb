# DescribeDBInstanceMonitor

You can call this operation to query the collection frequency of monitoring data for an ApsaraDB for MongoDB instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeDBInstanceMonitor&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDBInstanceMonitor|The operation that you want to perform. Set the value to **DescribeDBInstanceMonitor**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Granularity|String|1|The collection frequency of monitoring data. The value is **1** or **300**. Unit: seconds. |
|RequestId|String|EFD65226-08CC-4C4D-B6A4-CB3C382F67B0|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeDBInstanceMonitor
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeDBInstanceMonitorResponse>
	  <Granularity>1</Granularity>
	  <RequestId>EFD65226-08CC-4C4D-B6A4-CB3C382F67B0</RequestId>
</DescribeDBInstanceMonitorResponse>
```

`JSON` format

```
{
	"Granularity": 1,
	"RequestId": "EFD65226-08CC-4C4D-B6A4-CB3C382F67B0"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

