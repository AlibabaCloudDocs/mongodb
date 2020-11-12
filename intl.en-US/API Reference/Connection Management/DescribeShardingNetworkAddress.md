# DescribeShardingNetworkAddress

You can call this operation to query the connection information of sharded cluster instances of ApsaraDB for MongoDB.

This operation supports sharded cluster instances only.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeShardingNetworkAddress&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeShardingNetworkAddress|The operation that you want to perform. Set the value to **DescribeShardingNetworkAddress**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of an instance. |
|NodeId|String|No|d-bpxxxxxxxx|A sharded cluster instance consists of three components: mongos, shard, and Configserver.

 **Note:** You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the ID of the mongos, shard, or Configserverr node. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CompatibleConnections|Array| |An array that consists of the endpoints of DynamoDB instances. |
|CompatibleConnection| | | |
|ExpiredTime|String|2591963|The remaining duration of the classic network address. Unit: seconds. |
|IPAddress|String|10.140.xxx.xx|The IP address of the instance. |
|NetworkAddress|String|dds-bpxxxxxxxxxxxxxx.mongodb.rds.aliyuncs.com|The endpoint of the instance. |
|NetworkType|String|VPC|The network type. Valid values:

 -   **VPC**
-   **Classic**
-   **Public**: pubic endpoint |
|Port|String|3717|The port number. |
|VPCId|String|vpc-bpxxxxxxxx|The ID of the VPC.

 **Note:** This parameter is returned when the network type is **VPC**. |
|VswitchId|String|vsw-bpxxxxxxxx|The VSwitch ID of the VPC.

 **Note:** This parameter is returned when the network type is **VPC**. |
|NetworkAddresses|Array| |An array that consists of the endpoints of ApsaraDB for MongoDB instances. |
|NetworkAddress| | | |
|ExpiredTime|String|2591963|The remaining duration of the classic network address. Unit: seconds. |
|IPAddress|String|10.140.xxx.xx|The IP address of the instance. |
|NetworkAddress|String|s-bpxxxxxxxx.mongodb.rds.aliyuncs.com|The endpoint of the instance. |
|NetworkType|String|VPC|The network type. Valid values:

 -   **VPC**
-   **Classic**
-   **Public**: pubic endpoint |
|NodeId|String|s-bpxxxxxxxx|The ID of the mongos. |
|NodeType|String|mongos|The type of the node. Valid values:

 -   **mongos**
-   **shard**
-   **configserver** |
|Port|String|3717|The port number. |
|Role|String|Primary|The role of the node. Valid values:

 -   Primary
-   Secondary |
|VPCId|String|vpc-bpxxxxxxxx|The ID of the VPC.

 **Note:** This parameter is returned when the network type is **VPC**. |
|VswitchId|String|vsw-bpxxxxxxxx|The VSwitch ID of the VPC.

 **Note:** This parameter is returned when the network type is **VPC**. |
|RequestId|String|18D8AAFD-6BEB-420F-8164-810CB0C0AA39|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeShardingNetworkAddress
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<NetworkAddresses>
    <NetworkAddress>
        <NetworkType>Public</NetworkType>
        <NodeId>s-bpxxxxxxxx</NodeId>
        <Port>3717</Port>
        <VPCId/>
        <IPAddress>47.xx.xx.xxx</IPAddress>
        <NodeType>mongos</NodeType>
        <Role>Primary</Role>
        <NetworkAddress>s-bpxxxxxxxx-pub.mongodb.rds.aliyuncs.com</NetworkAddress>
    </NetworkAddress>
    <NetworkAddress>
        <NetworkType>VPC</NetworkType>
        <NodeId>s-bpxxxxxxxx</NodeId>
        <Port>3717</Port>
        <VPCId>vpc-bpxxxxxxxx</VPCId>
        <IPAddress>192.168.xx.xxx</IPAddress>
        <NodeType>mongos</NodeType>
        <Role>Primary</Role>
        <VswitchId>vsw-bpxxxxxxxx</VswitchId>
        <NetworkAddress>s-bpxxxxxxxx.mongodb.rds.aliyuncs.com</NetworkAddress>
    </NetworkAddress>
</NetworkAddresses>
<RequestId>3F5DD5CD-0B93-46FF-96DD-F938B13CDE8B</RequestId>
```

`JSON` format

```
{
	"NetworkAddresses": {
		"NetworkAddress": [
			{
				"NetworkType": "Public",
				"NodeId": "s-bpxxxxxxxx",
				"Port": "3717",
				"VPCId": "",
				"IPAddress": "47.xx.xx.xxx",
				"NodeType": "mongos",
				"Role": "Primary",
				"NetworkAddress": "s-bpxxxxxxxx-pub.mongodb.rds.aliyuncs.com"
			},
			{
				"NetworkType": "VPC",
				"NodeId": "s-bpxxxxxxxx",
				"Port": "3717",
				"VPCId": "vpc-bpxxxxxxxx",
				"IPAddress": "192.168.xx.xxx",
				"NodeType": "mongos",
				"Role": "Primary",
				"VswitchId": "vsw-bpxxxxxxxx",
				"NetworkAddress": "s-bpxxxxxxxx.mongodb.rds.aliyuncs.com"
			}
		]
	},
	"RequestId": "3F5DD5CD-0B93-46FF-96DD-F938B13CDE8B"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

