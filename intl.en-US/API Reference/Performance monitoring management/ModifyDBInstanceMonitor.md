# ModifyDBInstanceMonitor

You can call this operation to set the monitoring granularity for a ApsaraDB for MongoDB instance.

**Note:** For more information about the monitoring granularity values supported for various metrics, see [Set monitoring granularity](~~68188~~).

Before you call this operation, make sure that the following requirements are met:

-   A replica set or sharded cluster instance is used.
-   MongoDB 3.4 \(the latest minor version\) or 4.0 must be selected.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceMonitor&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceMonitor|The operation that you want to perform. Set the value to **ModifyDBInstanceTDE**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|Granularity|String|Yes|1|The collection frequency of monitoring data. Valid values: **1** or **300**. Unit: seconds. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|EFD65226-08CC-4C4D-B6A4-CB3C382F67B0|The ID of the request. |

## Examples

Sample request

```
http(s)://mongodb.aliyuncs.com/? Action=ModifyDBInstanceMonitor
&DBInstanceId=dds-bpxxxxxxxx
&Granularity=1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDBInstanceMonitorResponse>
	  <RequestId>EFD65226-08CC-4C4D-B6A4-CB3C382F67B0</RequestId>
</ModifyDBInstanceMonitorResponse>
```

`JSON` format

```
{
	"RequestId": "EFD65226-08CC-4C4D-B6A4-CB3C382F67B0"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

