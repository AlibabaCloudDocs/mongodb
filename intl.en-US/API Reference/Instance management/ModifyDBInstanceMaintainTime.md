# ModifyDBInstanceMaintainTime

You can call this operation to modify the maintenance window of an ApsaraDB for MongoDB instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceMaintainTime&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceMaintainTime|The operation that you want to perform. Set the value to **ModifyDBInstanceMaintainTime**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of an instance. |
|MaintainEndTime|String|Yes|02:00Z|The end time of the maintenance window. Specify the time in the *HH:mmZ* format. The time must be in UTC.

 **Note:** The difference between the start time and end time must be one hour. For example, if **MaintainStartTime** is **01:00Z**, **MaintainEndTime** must be **02:00Z**. |
|MaintainStartTime|String|Yes|01:00Z|The start time of the maintenance window. Specify the time in the *HH:mm*Z format. The time must be in UTC. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|A9310426-C763-42A2-A3AD-70A8DA204531|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=ModifyDBInstanceMaintainTime
&MaintainStartTime=01:00Z
&MaintainEndTime=02:00Z
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDBInstanceMaintainTimeResponse>
	  <RequestId>A9310426-C763-42A2-A3AD-70A8DA204531</RequestId>
</ModifyDBInstanceMaintainTimeResponse>
```

`JSON` format

```
{
	"RequestId": "A9310426-C763-42A2-A3AD-70A8DA204531"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

