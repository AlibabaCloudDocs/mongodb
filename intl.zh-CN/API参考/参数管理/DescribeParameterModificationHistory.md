# DescribeParameterModificationHistory

调用DescribeParameterModificationHistory接口查询MongoDB实例参数的修改记录。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeParameterModificationHistory&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeParameterModificationHistory|要执行的操作，取值：**DescribeParameterModificationHistory**。 |
|StartTime|String|是|2019-01-01T12:10Z|查询开始时间，格式为*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。 |
|EndTime|String|是|2019-01-02T12:10Z|查询结束时间，必须晚于查询开始时间，格式为*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 **说明：** 当本参数传入的是分片集群实例ID时，还需要传入**NodeId**参数。 |
|CharacterType|String|是|mongos|实例的角色类型，取值：

 -   db: shard角色
-   cs：config server角色
-   mongos：mongos角色
-   logic：分片集群实例 |
|NodeId|String|否|d-bpxxxxxxxx|分片集群实例中Mongos节点ID或Shard节点ID。

 **说明：** 当**DBInstanceId**参数传入的是分片集群实例ID时，本参数才可用。 |
|RegionId|String|否|cn-hangzhou|实例所属的地域ID，您可以调用[DescribeDBInstanceAttribute](~~62010~~)接口查询。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|HistoricalParameters|Array of HistoricalParameter| |参数的修改记录列表。 |
|HistoricalParameter| | | |
|ModifyTime|String|2019-03-12T07:58:24Z|参数修改的时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。 |
|NewParameterValue|String|200|修改后的参数值。 |
|OldParameterValue|String|100|修改前的参数值。 |
|ParameterName|String|operationProfiling.slowOpThresholdMs|被修改参数的名称。 |
|RequestId|String|B1BB6E0E-B4EF-4145-81FA-A07719860248|请求ID。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=DescribeParameterModificationHistory
&StartTime=2019-01-01T12:10Z
&EndTime=2019-01-02T12:10Z
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeParameterModificationHistoryResponse>
	  <HistoricalParameters>
		    <HistoricalParameter>
			      <OldParameterValue>100</OldParameterValue>
			      <ModifyTime>2019-03-12T07:58:24Z</ModifyTime>
			      <NewParameterValue>200</NewParameterValue>
			      <ParameterName>operationProfiling.slowOpThresholdMs</ParameterName>
		    </HistoricalParameter>
	  </HistoricalParameters>
	  <RequestId>B1BB6E0E-B4EF-4145-81FA-A07719860248</RequestId>
</DescribeParameterModificationHistoryResponse>
```

`JSON` 格式

```
{
	"HistoricalParameters": {
		"HistoricalParameter": [
			{
				"OldParameterValue": "100",
				"ModifyTime": "2019-03-12T07:58:24Z",
				"NewParameterValue": "200",
				"ParameterName": "operationProfiling.slowOpThresholdMs"
			}
		]
	},
	"RequestId": "B1BB6E0E-B4EF-4145-81FA-A07719860248"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

