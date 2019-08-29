# DescribeRoleZoneInfo {#doc_api_Dds_DescribeRoleZoneInfo .reference}

调用DescribeRoleZoneInfo接口查询MongoDB实例的各节点的角色和所属的可用区

**说明：** 更多详情请参见[查看节点所属的可用区](~~123825~~)。

本接口适用于副本集实例和分片集群实例，暂不支持单节点实例。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeRoleZoneInfo&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|Action|String|否|DescribeRoleZoneInfo|要执行的操作，取值：**DescribeRoleZoneInfo**。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|728B9A96-E262-4AE5-915E-3A51CCE2FDA9|请求ID。

 |
|ZoneInfos| | |节点在可用区中的分布信息列表。

 |
|InsName|String|dds-bpxxxxxxxx|节点ID。

 |
|NodeType|String|normal|节点类型，返回值为：

 -   **normal**：普通节点。
-   **configServer**：配置服务器节点。
-   **shard**：Shard节点。
-   **mongos**：Mongos节点。

 **说明：** 当实例类型为副本集实例时，返回值为**normal**；当实例类型为分片集群实例时，返回值中包含**configServer**、**shard**和**mongos**。

 |
|RoleId|String|83xxxxx|角色ID。

 |
|RoleType|String|Primary|节点的角色，返回值为：

 -   **Primary**：主节点。
-   **Secondary**：从节点。
-   **Hidden**：隐藏节点。

 |
|ZoneId|String|cn-hangzhou-e|可用区ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeRoleZoneInfo
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
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

`JSON` 格式

``` {#json_return_success_demo}
{
	"ZoneInfos":{
		"ZoneInfo":[
			{
				"NodeType":"normal",
				"RoleType":"Primary",
				"InsName":"dds-bpxxxxxxxx",
				"ZoneId":"cn-hangzhou-e",
				"RoleId":"83xxxxx"
			},
			{
				"NodeType":"normal",
				"RoleType":"Secondary",
				"InsName":"dds-bpxxxxxxxx",
				"ZoneId":"cn-hangzhou-f",
				"RoleId":"83xxxxx"
			},
			{
				"NodeType":"normal",
				"RoleType":"Hidden",
				"InsName":"dds-bpxxxxxxxx",
				"ZoneId":"cn-hangzhou-b",
				"RoleId":"83xxxxx"
			}
		]
	},
	"RequestId":"728B9A96-E262-4AE5-915E-3A51CCE2FDA9"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

