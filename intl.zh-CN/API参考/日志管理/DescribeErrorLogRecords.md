# DescribeErrorLogRecords {#doc_api_Dds_DescribeErrorLogRecords .reference}

调用DescribeErrorLogRecords接口查询MongoDB实例的错误日志。

本接口适用于副本集实例和分片集群实例，暂不支持单节点实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=DescribeErrorLogRecords)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeErrorLogRecords|要执行的操作，取值：**DescribeErrorLogRecords**。

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
|RoleType|String|否|primary|实例中节点的角色。取值：

 -   **primary**：主节点。
-   **secondary**：从节点。

 **说明：** 当**NodeId**参数传入的是Mongos节点ID时，本参数取值只能为**primary**。

 |
|DBName|String|否|mongodbtest|数据库名。

 |
|PageSize|Integer|否|30|每页记录数，取值范围：**30**~**100**。

 |
|PageNumber|Integer|否|1|页码，取值为大于0且不超过Integer数据类型的的最大值，默认值为**1**。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Items| | |错误日志明细列表。

 |
|└Category|String|NETWORK|日志类别。

 |
|└ConnInfo|String|conn18xxxxxx|日志连接信息。

 |
|└Content|String|xxxxxxxx|日志信息。

 |
|└CreateTime|String|2019-02-26T12:09:34Z|日志生成时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z。

 |
|PageNumber|Integer|1|页码。

 |
|PageRecordCount|Integer|1|每页的记录数。

 |
|RequestId|String|68BCBEC2-1E66-471F-A1A8-E3C60C0A80B0|请求ID。

 |
|TotalRecordCount|Integer|1|总记录数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeErrorLogRecords
&StartTime=2019-01-01T12:10Z
&EndTime=2019-01-02T12:10Z
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeErrorLogRecordsResponse>
  <Items>
    <LogRecords>
      <Category>NETWORK</Category>
      <CreateTime>2019-02-26T12:09:34Z</CreateTime>
      <ConnInfo>conn18xxxxxx</ConnInfo>
      <Content>xxxxxxxx</Content>
    </LogRecords>
  </Items>
  <PageNumber>1</PageNumber>
  <TotalRecordCount>2</TotalRecordCount>
  <RequestId>68BCBEC2-1E66-471F-A1A8-E3C60C0A80B0</RequestId>
</DescribeErrorLogRecordsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Items":{
		"LogRecords":[
			{
				"Category":"NETWORK",
				"CreateTime":"2019-02-26T12:09:34Z",
				"ConnInfo":"conn18xxxxxx",
				"Content":"xxxxxxxx"
			}
		]
	},
	"TotalRecordCount":2,
	"PageNumber":1,
	"RequestId":"68BCBEC2-1E66-471F-A1A8-E3C60C0A80B0"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

