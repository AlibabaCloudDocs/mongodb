# MigrateAvailableZone

You can call this operation to change the zone of an ApsaraDB for MongoDB instance.

This operation is applicable only to replica set instances, but not to standalone and sharded cluster instances.

**Note:** If you have applied for a public endpoint of the instance, you must first call the [ReleasePublicNetworkAddress](~~67604~~) operation to release the public endpoint.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=MigrateAvailableZone&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|MigrateAvailableZone|The operation that you want to perform. Set the value to **MigrateAvailableZone**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** You must specify the **Vswitch** parameter if the network type of the instance is VPC. |
|ZoneId|String|Yes|cn-hangzhou-b|The ID of the new zone.

 **Note:**

-   The new zone must be in the same region as the current zone of the instance.
-   You can call the [DescribeRegions](~~61933~~) operation to query the zone IDs. |
|Vswitch|String|No|vsw-bpxxxxxxxx|The ID of the vSwitch in the new zone.

 **Note:** This parameter can be used only when the network type of the instance is VPC. |
|EffectiveTime|String|No|Immediately|The time when the instance is migrated to the new zone. Valid values:

 -   **Immediately**: The instance will be migrated to the new zone immediately.
-   **MaintainTime**: The instance will be migrated to the new zone during the maintenance period of the instance.

 Default value: **Immediately**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|0FDDC511-7252-4A4A-ADDA-5CB1BF63873D|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=MigrateAvailableZone
&DBInstanceId=dds-bpxxxxxxxx
&ZoneId=cn-hangzhou-b
&EffectiveTime=Immediately
&<Common request parameters>
```

Sample success responses

`XML` format

```
<MigrateAvailableZoneResponse>
	  <RequestId>0FDDC511-7252-4A4A-ADDA-5CB1BF63873D</RequestId>
</MigrateAvailableZoneResponse>
```

`JSON` format

```
{
	"RequestId": "0FDDC511-7252-4A4A-ADDA-5CB1BF63873D"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

