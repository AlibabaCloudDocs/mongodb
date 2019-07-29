# DescribeRunningLogRecords {#doc_api_Dds_DescribeRunningLogRecords .reference}

调用DescribeRunningLogRecords接口查询MongoDB实例的运行日志。

本接口适用于副本集实例和分片集群实例，暂不支持单节点实例。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeRunningLogRecords&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeRunningLogRecords|要执行的操作，取值：**DescribeRunningLogRecords**。

 |
|StartTime|String|是|2019-01-01T12:10Z|查询开始时间，格式为*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。

 |
|EndTime|String|是|2019-01-02T12:10Z|查询结束时间，必须晚于查询开始时间，格式为*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 **说明：** 当本参数传入的是分片集群实例ID时，还需要传入**NodeId**参数。

 |
|NodeId|String|否|d-bpxxxxxxxx|分片集群实例中Mongos节点ID或Shard节点ID。

 **说明：** 当**DBInstanceId**参数传入的是分片集群实例ID时，本参数才可用。

 |
|DBName|String|否|mongodbtest|数据库名。

 |
|RoleType|String|否|primary|实例中节点的角色。取值：

 -   **primary**：主节点。
-   **secondary**：从节点。

 **说明：** 当**NodeId**参数传入的是Mongos节点ID时，**RoleType**取值只能为**primary**。

 |
|PageSize|Integer|否|30|每页记录数，取值范围为**30**~**100**。

 |
|PageNumber|Integer|否|1|页码，取值为大于0且不超过Integer数据类型的的最大值，默认值为**1**。

 |
|RegionId|String|否|cn-hangzhou|实例所属的地域ID，您可以通过调用[DescribeDBInstanceAttribute](~~62010~~)进行查询。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Items| | |运行日志明细列表。

 |
|Category|String|NETWORK|日志类别。

 |
|ConnInfo|String|conn18xxxxxx|日志连接信息。

 |
|Content|String|end connection 11.xxx.xxx.xx:3xxxx \(0 connections now open\)\\n|日志信息。

 |
|CreateTime|String|2019-02-26T12:09:34Z|日志生成时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|PageNumber|Integer|1|页码。

 |
|PageRecordCount|Integer|30|每页的记录数。

 |
|RequestId|String|45D2B592-DEBA-4347-BBF3-47FF6C97DBBC|请求ID。

 |
|TotalRecordCount|Integer|2|总记录数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeRunningLogRecords
&StartTime=2019-01-01T12:10Z
&EndTime=2019-01-02T12:10Z
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeRunningLogRecordsResponse>
	  <Items>
		    <LogRecords>
			      <Category>-</Category>
			      <CreateTime>2019-02-26T12:09:34Z</CreateTime>
			      <ConnInfo>conn18xxxxxx</ConnInfo>
			      <Content>
				end connection 11.xxx.xxx.xx:3xxxx (0 connections now open)
			</Content>
		    </LogRecords>
		    <LogRecords>
			      <Category>NETWORK</Category>
			      <CreateTime>2019-02-26T12:09:34Z</CreateTime>
			      <ConnInfo>thread1</ConnInfo>
			      <Content>connection accepted from 11.xxx.xxx.xx:3xxxx #1862051 (11 connections now open)</Content>
		    </LogRecords>
	  </Items>
	  <PageNumber>1</PageNumber>
	  <TotalRecordCount>2</TotalRecordCount>
	  <RequestId>45D2B592-DEBA-4347-BBF3-47FF6C97DBBC</RequestId>
</DescribeRunningLogRecordsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Items":{
		"LogRecords":[
			{
				"Category":"-",
				"CreateTime":"2019-02-26T12:09:34Z",
				"ConnInfo":"conn18xxxxxx",
				"Content":"end connection 11.xxx.xxx.xx:3xxxx (0 connections now open)\n"
			},
			{
				"Category":"NETWORK",
				"CreateTime":"2019-02-26T12:09:34Z",
				"ConnInfo":"thread1",
				"Content":"connection accepted from 11.xxx.xxx.xx:3xxxx #1862051 (11 connections now open)"
			}
		]
	},
	"TotalRecordCount":2,
	"PageNumber":1,
	"RequestId":"45D2B592-DEBA-4347-BBF3-47FF6C97DBBC"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

