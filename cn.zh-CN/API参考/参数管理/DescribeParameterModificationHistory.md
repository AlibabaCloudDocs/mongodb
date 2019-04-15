# DescribeParameterModificationHistory {#doc_api_Dds_DescribeParameterModificationHistory .reference}

调用DescribeParameterModificationHistory接口查询MongoDB实例参数的修改记录。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=DescribeParameterModificationHistory)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeParameterModificationHistory|要执行的操作，取值：**DescribeParameterModificationHistroy**。

 |
|StartTime|String|是|2019-01-01T12:10Z|查询开始时间，格式为*yyyy-MM-dd*T*HH:mm*Z。

 |
|EndTime|String|是|2019-01-02T12:10Z|查询结束时间，必须晚于查询开始时间，格式为*yyyy-MM-dd*T*HH:mm*Z。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 **说明：** 当本参数传入的是分片集群实例ID时，还需要传入**NodeId**参数。

 |
|NodeId|String|否|d-bpxxxxxxxx|分片集群实例中Mongos节点ID或Shard节点ID。

 **说明：** 当**DBInstanceId**参数传入的是分片集群实例ID时，本参数才可用。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|HistoricalParameters| | |参数的修改记录列表。

 |
|└ModifyTime|String|2019-03-12T07:58:24Z|参数修改的时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z。

 |
|└NewParameterValue|String|200|修改后的参数值。

 |
|└OldParameterValue|String|100|修改前的参数值。

 |
|└ParameterName|String|operationProfiling.slowOpThresholdMs|被修改参数的名称。

 |
|RequestId|String|B1BB6E0E-B4EF-4145-81FA-A07719860248|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DescribeParameterModificationHistory
&StartTime=2019-01-01T12:10Z
&EndTime=2019-01-02T12:10Z
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
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

``` {#json_return_success_demo}
{
	"HistoricalParameters":{
		"HistoricalParameter":[
			{
				"OldParameterValue":"100",
				"ModifyTime":"2019-03-12T07:58:24Z",
				"NewParameterValue":"200",
				"ParameterName":"operationProfiling.slowOpThresholdMs"
			}
		]
	},
	"RequestId":"B1BB6E0E-B4EF-4145-81FA-A07719860248"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

