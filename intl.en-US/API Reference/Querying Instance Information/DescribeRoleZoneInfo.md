# DescribeRoleZoneInfo

You can call this operation to query the roles and zones of nodes in an ApsaraDB for MongoDB instance.

**Note:** For more information, see [View the zone of a node](~~123825~~).

This operation is applicable only to replica set and sharded cluster instances, but not to standalone instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeRoleZoneInfo&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeRoleZoneInfo|The operation that you want to perform. Set the value to **DescribeRoleZoneInfo**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|728B9A96-E262-4AE5-915E-3A51CCE2FDA9|The ID of the request. |
|ZoneInfos|Array| |An array that consists of information of nodes in the zone. |
|ZoneInfo| | | |
|InsName|String|dds-bpxxxxxxxx|The ID of the node. |
|NodeType|String|normal|The type of the node. Valid values:

 -   **normal**
-   **configServer**
-   **shard**
-   **mongos**

 **Note:** Valid value for replica set instances: **normal**. Valid values for replica set instances: **configServer**, **shard**, and **mongos**. |
|RoleId|String|83xxxxx|The ID of the role. |
|RoleType|String|Primary|The role of the node. Valid values:

 -   **Primary**
-   **Secondary**
-   **Hidden** |
|ZoneId|String|cn-hangzhou-e|The zone ID. |

## Examples

Sample request

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeRoleZoneInfo
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeRoleZoneInfoResponse>
	  <ZoneInfos>
		    <ZoneInfo>
			      <RoleType>Primary</RoleType>
			      <NodeType>normal</NodeType>
			      <InsName>dds-bpxxxxxxxx</InsName>
			      <ZoneId>cn-hangzhou-e</ZoneId>
			      <RoleId>83xxxxx</RoleId>
		    </ZoneInfo>
		    <ZoneInfo>
			      <RoleType>Secondary</RoleType>
			      <NodeType>normal</NodeType>
			      <InsName>dds-bpxxxxxxxx</InsName>
			      <ZoneId>cn-hangzhou-f</ZoneId>
			      <RoleId>83xxxxx</RoleId>
		    </ZoneInfo>
		    <ZoneInfo>
			      <RoleType>Hidden</RoleType>
			      <NodeType>normal</NodeType>
			      <InsName>dds-bpxxxxxxxx</InsName>
			      <ZoneId>cn-hangzhou-b</ZoneId>
			      <RoleId>83xxxxx</RoleId>
		    </ZoneInfo>
	  </ZoneInfos>
	  <RequestId>728B9A96-E262-4AE5-915E-3A51CCE2FDA9</RequestId>
</DescribeRoleZoneInfoResponse>
```

`JSON` format

```
{
	"ZoneInfos": {
		"ZoneInfo": [
			{
				"RoleType": "Primary",
				"NodeType": "normal",
				"InsName": "dds-bpxxxxxxxx",
				"ZoneId": "cn-hangzhou-e",
				"RoleId": "83xxxxx"
			},
			{
				"RoleType": "Secondary",
				"NodeType": "normal",
				"InsName": "dds-bpxxxxxxxx",
				"ZoneId": "cn-hangzhou-f",
				"RoleId": "83xxxxx"
			},
			{
				"RoleType": "Hidden",
				"NodeType": "normal",
				"InsName": "dds-bpxxxxxxxx",
				"ZoneId": "cn-hangzhou-b",
				"RoleId": "83xxxxx"
			}
		]
	},
	"RequestId": "728B9A96-E262-4AE5-915E-3A51CCE2FDA9"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

