# DescribeShardingNetworkAddress {#doc_api_Dds_DescribeShardingNetworkAddress .reference}

调用DescribeShardingNetworkAddress接口查询MongoDB分片集群实例的连接信息。

该接口仅支持分片集群实例。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeShardingNetworkAddress&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|Action|String|否|DescribeShardingNetworkAddress|要执行的操作，取值：**DescribeShardingNetworkAddress**。

 |
|NodeId|String|否|d-bpxxxxxxxx|分片集群实例中Mongos节点ID、Shard节点ID或ConfigServer节点ID。

 **说明：** 您可以调用[DescribeDBInstanceAttribute](~~62010~~)接口查询Mongos/Shard/ConfigServer节点ID。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|NetworkAddresses| | |实例连接地址信息列表。

 |
|NetworkAddress| | |实例连接地址信息列表。

 |
|ExpiredTime|String|2591963|保留的经典网络地址剩余时长，单位为秒。

 |
|IPAddress|String|10.140.xxx.xx|IP地址。

 |
|NetworkAddress|String|s-bpxxxxxxxx.mongodb.rds.aliyuncs.com|连接地址（字符串）。

 |
|NetworkType|String|VPC|网络类型。

 -   **VPC**：专有网络。
-   **Classic**：经典网络。
-   **Public**：公网。

 |
|NodeId|String|s-bpxxxxxxxx|Mongos节点ID。

 |
|NodeType|String|mongos|节点类型，返回值为

 -   **mongos**：mongos节点。
-   **shard**：shard节点。
-   **configserver**：configserver节点。

 |
|Port|String|3717|连接端口。

 |
|VPCId|String|vpc-bpxxxxxxxx|专有网络ID。

 **说明：** 当网络类型为**VPC**时返回该参数。

 |
|VswitchId|String|vsw-bpxxxxxxxx|专有网络中交换机ID。

 **说明：** 当网络类型为**VPC**时返回该参数。

 |
|RequestId|String|18D8AAFD-6BEB-420F-8164-810CB0C0AA39|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeShardingNetworkAddress
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

