# DescribeIndexRecommendation {#doc_api_Dds_DescribeIndexRecommendation .reference}

You can call this operation to query the index recommendation details of an AsparaDB for MongoDB instance.

Ensure that the instance meets the following conditions when you call this operation:

-   The region of the instance is China \(Hangzhou\), China \(Shanghai\), China \(Shenzhen\), China \(Qingdao\), or China \(Beijing\).
-   The instance type is replica set or sharded cluster.
-   The log audit function is enabled for the instance.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeIndexRecommendation) simplifies API usage. You can use OpenAPI explorer to perform operations such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeIndexRecommendation|The operation that you want to perform. Set the value to **DescribeIndexRecommendation**.

 |
|InstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** If you specify this parameter to the ID of a sharded cluster instance, you must also specify the **NodeId** parameter.

 |
|TaskId|String|No|3223069|The ID of the task. You can call the [DescribeAvailableTimeRange](~~95534~~) operation to query task IDs.

 |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the mongos or shard in the specified cluster instance.

 **Note:** This parameter is only valid when you specify the **DBInstanceId** parameter to the ID of a sharded cluster instance.

 |
|Database|String|No|mongodbtest|The name of the database.

 |
|Collection|String|No|customer|The name of the set.

 |
|StartTime|String|No|2019-01-01T12Z|The beginning of the time range that you want to query. The time is in the *yyyy-MM-dd*T*HH*Z format.

 **Note:** The value of **StartTime** parameter must be later than the time when the log audit function was enabled.

 |
|EndTime|String|No|2019-01-02T13Z|The end of the time range that you want to query. The value of EndTime must be later than the value of StartTime. The time is in the *yyyy-MM-dd*T*HH*Z format.

 |
|OperationType|String|No|query|The type of operation to perform, such as **query**, **delete**, and **update**.

 |
|PageSize|Integer|No|30|The number of records to display on each page. Valid values: **30, 50, and 100**. Default value: **30**.

 |
|PageNumber|Integer|No|1|The page number to display. Valid values: any non-zero positive integer. Default value: **1**.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Analyzations| | |The details about the index recommendation.

 |
|└AverageDocsExaminedCount|Long|1000000|The average number of times targets documents were scanned in the current index recommendation task.

 |
|└AverageExecutionTime|Long|526|The average execution time. Unit: milliseconds.

 |
|└AverageKeysExaminedCount|Long|0|The average number of times targets indexes were scanned in the current index recommendation task.

 |
|└AverageReturnRowCount|Long|1|The average number of rows returned.

 |
|└Count|Long|364|The number of times the request was executed.

 |
|└Database|String|mongodbtest|The name of the database to query.

 |
|└ExecutionPlan|String|\{\\"stage\\":\\"COLLSCAN\\"\}|The execution plan of the query.

 |
|└InMemorySort|String|false|Indicates whether in-memory sorting was performed.

 |
|└IndexCombines| |\{"IndexCombine": \["db.customer.createIndex\(\{\\"name\\": 1\}, \{background: true\}\)"\]\}|The merged indexes.

 |
|└IndexRecommendations| | |The index recommendations.

 |
|└Content|String|db.customer.createIndex\(\{\\"name\\": 1\}, \{background: true\}\)|The content of the recommendation.

 |
|└RecmdType|String|Index|The returned recommendation.

 -   **Index**: Optimize the index direction.
-   **Refactor**: Rewrite the query statement because no indexes are being applied to the query.
-   **WhereUse**: The query includes the WHERE clause, which cannot be used with indexes. Do not include the WHERE clause in index queries.
-   **NoRecommendation** : No recommendations.

 |
|└LastExecutionTime|String|2019-03-22T05:52:31Z|The most recent execution time. The time is in the *yyyy-MM-dd*T*HH:mm:ss*Z format.

 |
|└Namespace|String|mongodbtest.customer|The namespace.

 **Note:** The namespace is typically a combination of the database name and set name.

 |
|└Operation|String|query|The operation type.

 |
|└Query|String|\{\\"name\\":\\"<val\>\\"\}|The query command.

 |
|└Sort|String|\{\}|The sorting command.

 |
|└TotalExecutionTime|Long|191569|Total execution time. Unit: milliseconds.

 |
|RequestId|String|553CCFB2-C013-4A9D-86A9-F440BA7E365F|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeIndexRecommendation
&InstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

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

`JSON` format

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

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidEndTime.Format|Specified end time is not valid.|The error message returned when the end time is invalid. Check the format of the specified time.|

[View error codes](https://error-center.aliyun.com/status/product/Dds)

