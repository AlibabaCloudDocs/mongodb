# DescribeShardingNetworkAddress {#doc_api_Dds_DescribeShardingNetworkAddress .reference}

You can call this operation to query the connection information of sharded cluster instances in ApsaraDB for MongoDB.

This operation supports sharded cluster instances only.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeShardingNetworkAddress) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeShardingNetworkAddress|The operation that you want to perform. Set the value to **DescribeShardingNetworkAddress**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the shard or mongos in the specified sharded cluster instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NetworkAddresses| | |The list of the instance connection addresses.

 |
|└ExpiredTime|String|2591963|The remaining duration of the classic network address. Unit: seconds.

 |
|└IPAddress|String|10.140.xxx.xx|The IP address.

 |
|└NetworkAddress|String|s-bpxxxxxxxx.mongodb.rds.aliyuncs.com|The connection address \(string\).

 |
|└NetworkType|String|VPC|The network type. Valid values:

 -   **VPC**
-   **Classic**
-   **Public**

 |
|└NodeId|String|s-bpxxxxxxxx|The ID of the mongos.

 |
|└Port|String|3717|The port number.

 |
|└VPCId|String|vpc-bpxxxxxxxx|The ID of the VPC.

 **Note:** This parameter is returned when the network type is **VPC**.

 |
|└VswitchId|String|vsw-bpxxxxxxxx|The VSwitch ID of the VPC.

 **Note:** This parameter is returned when the network type is **VPC**.

 |
|RequestId|String|18D8AAFD-6BEB-420F-8164-810CB0C0AA39|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeShardingNetworkAddress
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeShardingNetworkAddressResponse>
  <NetworkAddresses>
    <NetworkAddress>
      <NetworkType>VPC</NetworkType>
      <NodeId>s-bpxxxxxxxx</NodeId>
      <Port>3717</Port>
      <VPCId>vpc-bpxxxxxxxx</VPCId>
      <IPAddress>192.168.xxx.xx</IPAddress>
      <VswitchId>vsw-bpxxxxxxxx</VswitchId>
      <NetworkAddress>s-bp1xxxxxxxx.mongodb.rds.aliyuncs.com</NetworkAddress> 
    </NetworkAddress>
    <NetworkAddress>
      <NetworkType>VPC</NetworkType>
      <NodeId>s-bpxxxxxxxx</NodeId>
      <Port>3717</Port>
      <VPCId>vpc-bpxxxxxxxx</VPCId>
      <IPAddress>192.168.xxx.xx</IPAddress>
      <VswitchId>vsw-bpxxxxxxxx</VswitchId>
      <NetworkAddress>s-bpxxxxxxxx.mongodb.rds.aliyuncs.com</NetworkAddress>
    </NetworkAddress>
  </NetworkAddresses> 
  <RequestId>B4B78989-6D75-4930-BC26-635C3BB3A33B</RequestId> 
</DescribeShardingNetworkAddressResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"NetworkAddresses":{
		"NetworkAddress":[
			{
				"NetworkType":"VPC",
				"Port":"3717",
				"NodeId":"s-bpxxxxxxxx",
				"VPCId":"vpc-bpxxxxxxxx",
				"IPAddress":"192.168.xxx.xx",
				"NetworkAddress":"s-bp1xxxxxxxx.mongodb.rds.aliyuncs.com",
				"VswitchId":"vsw-bpxxxxxxxx"
			},
			{
				"NetworkType":"VPC",
				"Port":"3717",
				"NodeId":"s-bpxxxxxxxx",
				"VPCId":"vpc-bpxxxxxxxx",
				"IPAddress":"192.168.xxx.xx",
				"NetworkAddress":"s-bpxxxxxxxx.mongodb.rds.aliyuncs.com",
				"VswitchId":"vsw-bpxxxxxxxx"
			}
		]
	},
	"RequestId":"B4B78989-6D75-4930-BC26-635C3BB3A33B"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

