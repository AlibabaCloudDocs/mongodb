# MigrateAvailableZone {#doc_api_Dds_MigrateAvailableZone .reference}

You can call this operation to change the zone of a MongoDB instance.

This operation is applicable to replica set instances. MigrateAvailableZone cannot be performed on standalone instances and sharded cluster instances.

**Note:** If you have applied a public network address to the instance, you must first call [ReleasePublicNetworkAddress](~~67604~~) to release the public network address.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=MigrateAvailableZone) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|MigrateAvailableZone|The operation that you want to perform. Set the value to **MigrateAvailableZone**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** You must specify the **Vswitch** parameter if the network type of the instance is VPC.

 |
|ZoneId|String|Yes|cn-hangzhou-b|The ID of the destination zone to which you want to migrate the MongoDB instance.

 **Note:** 

-   The destination zone must be in the same region as the current zone of the instance.
-   You can call [DescribeRegions](~~61933~~) to query the IDs of zones in Alibaba Cloud.

 |
|EffectiveTime|String|Yes|Immediately|The time when the instance is migrated to the destination zone. Valid values:

 -   **Immediately**
-   **MaintainTime**: The instance will be migrated during the maintenance period of the instance.

 Default value: **Immediately**.

 |
|Vswitch|String|No|1|The ID of the VSwitch in the destination zone.

 **Note:** This parameter can be used only when the network type of the instance is VPC.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|0FDDC511-7252-4A4A-ADDA-5CB1BF63873D|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=MigrateAvailableZone
&DBInstanceId=dds-bpxxxxxxxx
&ZoneId=cn-hangzhou-b
&EffectiveTime=Immediately
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<MigrateAvailableZoneResponse>
  <RequestId>0FDDC511-7252-4A4A-ADDA-5CB1BF63873D</RequestId>
</MigrateAvailableZoneResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"0FDDC511-7252-4A4A-ADDA-5CB1BF63873D"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

