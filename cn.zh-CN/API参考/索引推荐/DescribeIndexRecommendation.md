# DescribeIndexRecommendation {#doc_api_Dds_DescribeIndexRecommendation .reference}

调用DescribeIndexRecommendation接口查询MongoDB实例的索引推荐详情。

实例须满足以下条件，否则该接口调用失败：

-   实例的地域为华东1、华东2、华南1、华北1或华北2。
-   实例类型为副本集实例或分片集群实例。
-   实例已开通审计日志功能。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=DescribeIndexRecommendation)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeIndexRecommendation|要执行的操作，取值：**DescribeIndexRecommendation**。

 |
|InstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 **说明：** 当本参数传入的是分片集群实例ID时，还需要传入**NodeId**参数。

 |
|TaskId|String|否|3223069|任务ID，您可以通过调用[DescribeAvailableTimeRange](~~95534~~)接口查询。

 |
|NodeId|String|否|d-bpxxxxxxxx|分片集群实例中Mongos节点ID或Shard节点ID。

 **说明：** 当**DBInstanceId**参数传入的是分片集群实例ID时，本参数才可用。

 |
|Database|String|否|mongodbtest|数据库名。

 |
|Collection|String|否|customer|集合名。

 |
|StartTime|String|否|2019-01-01T12Z|查询开始时间，格式为*yyyy-MM-dd*T*HH*Z。

 **说明：** **StartTime**取值必须晚于审计日志的开启时间。

 |
|EndTime|String|否|2019-01-02T13Z|查询结束时间，必须晚于查询开始时间，格式为*yyyy-MM-dd*T*HH*Z。

 |
|OperationType|String|否|query|操作类型，例如**query**、**delete**、**update**等。

 |
|PageSize|Integer|否|30|每页记录数，取值： **30、50、100**，默认值为**30**。

 |
|PageNumber|Integer|否|1|页码，取值为大于0且不超过Integer数据类型的的最大值，默认值为**1**。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Analyzations| | |索引推荐详情列表。

 |
|└AverageDocsExaminedCount|Long|1000000|平均文档扫描次数。

 |
|└AverageExecutionTime|Long|526|平均执行时间（毫秒）。

 |
|└AverageKeysExaminedCount|Long|0|平均索引扫描次数。

 |
|└AverageReturnRowCount|Long|1|平均返回行数。

 |
|└Count|Long|364|执行次数。

 |
|└Database|String|mongodbtest|​数据库名。

 |
|└ExecutionPlan|String|\{\\"stage\\":\\"COLLSCAN\\"\}|查询的执行计划。

 |
|└InMemorySort|String|false|是否使用内存查询。

 |
|└IndexCombines| |\{"IndexCombine": \["db.customer.createIndex\(\{\\"name\\": 1\}, \{background: true\}\)"\]\}|合并后的索引列表。

 |
|└IndexRecommendations| | |索引建议列表。

 |
|└Content|String|db.customer.createIndex\(\{\\"name\\": 1\}, \{background: true\}\)|建议的内容。

 |
|└RecmdType|String|Index|建议的类型。

 -   **Index**：建议从索引方向进行优化。
-   **Refactor**：询命令没有使用索引，需要对查询命令进行改写。
-   **WhereUse**：查询使用了where语法，而where语法无法使用索引，不建议使用。
-   **NoRecommendation**：没有建议。

 |
|└LastExecutionTime|String|2019-03-22T05:52:31Z|最近一次执行时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z。

 |
|└Namespace|String|mongodbtest.customer|命名空间。

 **说明：** 命名空间一般是数据库名和集合名的组合。

 |
|└Operation|String|query|操作类型。

 |
|└Query|String|\{\\"name\\":\\"<val\>\\"\}|查询命令。

 |
|└Sort|String|\{\}|排序命令。

 |
|└TotalExecutionTime|Long|191569|总执行时间（毫秒）。

 |
|RequestId|String|553CCFB2-C013-4A9D-86A9-F440BA7E365F|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeIndexRecommendation
&InstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeIndexRecommendationResponse>
  <Analyzations>
    <Analyzation>
      <InMemorySort>false</InMemorySort>
      <Sort>{}</Sort>
      <Operation>query</Operation>
      <Count>364</Count>
      <AverageKeysExaminedCount>0</AverageKeysExaminedCount>
      <Database>mongodbtest</Database>
      <Query>{"name":"&lt;val&gt;"}</Query>
      <AverageExecutionTime>526</AverageExecutionTime>
      <AverageReturnRowCount>0</AverageReturnRowCount>
      <IndexRecommendations>
        <Recommendation>
          <RecmdType>Index</RecmdType>
          <Content>db.customer.createIndex({"name": 1}, {background: true})</Content>
        </Recommendation>
      </IndexRecommendations>
      <TotalExecutionTime>191569</TotalExecutionTime>
      <LastExecutionTime>2019-03-22T05:52:31Z</LastExecutionTime>
      <ExecutionPlan>{"stage":"COLLSCAN"}</ExecutionPlan>
      <Namespace>mongodbtest.customer</Namespace>
      <AverageDocsExaminedCount>1000000</AverageDocsExaminedCount>
      <IndexCombines>
        <IndexCombine>db.customer.createIndex({"name": 1}, {background: true})</IndexCombine>
      </IndexCombines>
    </Analyzation>
  </Analyzations>
  <PageNumber>1</PageNumber>
  <TotalRecordCount>1</TotalRecordCount>
  <RequestId>553CCFB2-C013-4A9D-86A9-F440BA7E365F</RequestId>
  <PageRecordCount>1</PageRecordCount>
</DescribeIndexRecommendationResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Analyzations":{
		"Analyzation":[
			{
				"InMemorySort":false,
				"Sort":"{}",
				"Operation":"query",
				"Count":364,
				"AverageKeysExaminedCount":0,
				"Database":"mongodbtest",
				"Query":"{\"name\":\"<val>\"}",
				"AverageExecutionTime":526,
				"AverageReturnRowCount":0,
				"IndexRecommendations":{
					"Recommendation":[
						{
							"RecmdType":"Index",
							"Content":"db.customer.createIndex({\"name\": 1}, {background: true})"
						}
					]
				},
				"TotalExecutionTime":191569,
				"LastExecutionTime":"2019-03-22T05:52:31Z",
				"ExecutionPlan":"{\"stage\":\"COLLSCAN\"}",
				"Namespace":"mongodbtest.customer",
				"AverageDocsExaminedCount":1000000,
				"IndexCombines":{
					"IndexCombine":[
						"db.customer.createIndex({\"name\": 1}, {background: true})"
					]
				}
			}
		]
	},
	"TotalRecordCount":1,
	"PageNumber":1,
	"RequestId":"553CCFB2-C013-4A9D-86A9-F440BA7E365F",
	"PageRecordCount":1
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidEndTime.Format|Specified end time is not valid.|输入的结束时间无效，请您检查输入的时间格式是否正确。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

