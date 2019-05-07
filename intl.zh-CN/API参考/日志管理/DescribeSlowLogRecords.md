# DescribeSlowLogRecords {#doc_api_Dds_DescribeSlowLogRecords .reference}

调用DescribeSlowLogRecords接口查询MongoDB实例运行出现的慢操作日志明细。

本接口适用于副本集实例和分片集群实例，暂不支持单节点实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=DescribeSlowLogRecords)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeSlowLogRecords|要执行的操作，取值：**DescribeSlowLogRecords**。

 |
|StartTime|String|是|2019-02-24T12:10Z|查询开始时间，格式为*yyyy-MM-dd*T*HH:mm*Z。

 |
|EndTime|String|是|2019-02-26T12:10Z|查询结束时间，必须晚于查询开始时间，格式为*yyyy-MM-dd*T*HH:mm*Z。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 **说明：** 当本参数传入的是分片集群实例ID时，还需要传入**NodeId**参数。

 |
|NodeId|String|否|d-bpxxxxxxxx|Shard节点ID。

 **说明：** 当**DBInstanceId**参数传入的是分片集群实例ID时，本参数才可用。

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
|Engine|String|MongoDB|数据库引擎。

 |
|Items| | |慢操作日志明细列表。

 |
|└AccountName|String|root|执行该操作的数据库用户名。

 |
|└DBName|String|mongodbtest|数据库名。

 |
|└DocsExamined|Long|1000000|该操作执行时扫描的文档数。

 |
|└ExecutionStartTime|String|2019-02-25T01:41:28Z|操作执行的开始时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z。

 |
|└HostAddress|String|47.xxx.xxx.xx|连接数据库的主机地址。

 |
|└KeysExamined|Long|0|索引扫描行数。

 |
|└QueryTimes|String|600|该语句的执行时长，单位为毫秒。

 |
|└ReturnRowCounts|Long|0|返回行数。

 |
|└SQLText|String|\{\\"op\\":\\"query\\",\\"ns\\":\\"mongodbtest.customer\\",\\"query\\":\{\\"find\\":\\"customer\\",\\"filter\\":\{\\"name\\":\\"jack\\"\}\}\}|慢操作执行的语句。

 |
|PageNumber|Integer|1|页码。

 |
|PageRecordCount|Integer|1|本页慢操作日志明细的个数。

 |
|RequestId|String|414A4E5-4C36-4461-95FC-23757A20B5F8|请求ID。

 |
|TotalRecordCount|Integer|1|总记录数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeSlowLogRecords
&StartTime=2019-02-24T12:10Z
&EndTime=2019-02-26T12:10Z
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeSlowLogRecordsResponse>
  <Items>
    <LogRecords>
      <ReturnRowCounts>0</ReturnRowCounts>
      <KeysExamined>0</KeysExamined>
      <HostAddress>47.xxx.xxx.xx</HostAddress>
      <SQLText>{"op":"query","ns":"mongodbtest.customer","query":{"find":"customer","filter":{"name":"jack"}}}</SQLText>
      <ExecutionStartTime>2019-02-25T01:41:28Z</ExecutionStartTime>
      <AccountName>root</AccountName>
      <QueryTimes>600</QueryTimes>
      <DocsExamined>1000000</DocsExamined>
      <DBName>mongodbtest</DBName>
    </LogRecords>
  </Items>
  <PageNumber>1</PageNumber>
  <TotalRecordCount>1</TotalRecordCount>
  <RequestId>5414A4E5-4C36-4461-95FC-23757A20B5F8</RequestId>
  <Engine>MongoDB</Engine>
  <PageRecordCount>1</PageRecordCount>
</DescribeSlowLogRecordsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Items":{
		"LogRecords":[
			{
				"KeysExamined":"0",
				"ReturnRowCounts":0,
				"HostAddress":"47.110.74.177",
				"SQLText":"{\"op\":\"query\",\"ns\":\"mongodbtest.customer\",\"query\":{\"find\":\"customer\",\"filter\":{\"name\":\"ajackeyifeo1w\"}}}",
				"ExecutionStartTime":"2019-02-25T01:41:28Z",
				"AccountName":"root",
				"QueryTimes":600,
				"DBName":"mongodbtest",
				"DocsExamined":"1000000"
			}
		]
	},
	"TotalRecordCount":1,
	"PageNumber":1,
	"RequestId":"5414A4E5-4C36-4461-95FC-23757A20B5F8",
	"Engine":"MongoDB",
	"PageRecordCount":1
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

