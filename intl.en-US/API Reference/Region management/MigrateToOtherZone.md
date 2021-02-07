# MigrateToOtherZone

You can call this operation to migrate an ApsaraDB for MongoDB instance to another zone.

This operation is applicable only to replica set instances, but not to standalone instances or sharded cluster instances.

**Note:** If you have applied for a public endpoint of the instance, you must first call the [ReleasePublicNetworkAddress](~~67604~~) operation to release the public endpoint.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=MigrateToOtherZone&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|MigrateToOtherZone|The operation that you want to perform. Set the value to **MigrateToOtherZone**. |
|InstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** If the network type of the instance is VPC, you must specify the **Vswitch** parameter . |
|ZoneId|String|Yes|cn-hangzhou-b|The ID of the destination zone to which you want to migrate the ApsaraDB for MongoDB instance.

 **Note:**

-   The destination and source zones must be in one region.
-   You can call [DescribeRegions](~~61933~~) to query the zone IDs. |
|EffectiveTime|String|No|Immediately|The time when the instance is migrated to the destination zone. Valid values:

 -   **Immediately**: The instance is immediately migrated to the destination zone.
-   **MaintainTime**: The instance is migrated during the maintenance period of the instance.

 Default value: **Immediately**. |
|VSwitchId|String|No|vsw-bpxxxxxxxx|The ID of the vSwitch in the destination zone.

 **Note:** This parameter is valid and required only when the network type of the instance is VPC. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|0FDDC511-7252-4A4A-ADDA-5CB1BF63873D|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=MigrateToOtherZone
&DBInstanceId=dds-bpxxxxxxxx
&ZoneId=cn-hangzhou-b
&EffectiveTime=Immediately
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RequestId>0FDDC511-7252-4A4A-ADDA-5CB1BF63873D</RequestId>
```

`JSON` format

```
{
	"RequestId": "0FDDC511-7252-4A4A-ADDA-5CB1BF63873D"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

