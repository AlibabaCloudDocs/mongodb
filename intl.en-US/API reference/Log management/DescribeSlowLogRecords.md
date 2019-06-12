# DescribeSlowLogRecords {#doc_api_Dds_DescribeSlowLogRecords .reference}

You can call this operation to query the slow operation log details of the MongoDB instance.

This operation is applicable to replica set instances and sharded cluster instances. DescribeSlowLogRecords cannot be performed on standalone instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeSlowLogRecords) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeSlowLogRecords|The operation that you want to perform. Set the value to **DescribeSlowLogRecords**.

 |
|StartTime|String|Yes|2019-02-24T12:10Z|The beginning of the time range that you want to query. The time is in the *yyyy-MM-dd*T*HH:mm*Z format.

 |
|EndTime|String|Yes|2019-02-26T12:10Z|The end of the time range that you want to query. The time is in the *yyyy-MM-dd*T*HH:mm*Z format.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** If you specify this parameter to the ID of a sharded cluster instance, you must also specify the **NodeId** parameter.

 |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the shard.

 **Note:** This parameter is only valid when you specify the **DBInstanceId** parameter to the ID of a sharded cluster instance.

 |
|DBName|String|No|mongodbtest|The name of the database.

 |
|PageSize|Integer|No|30|The number of records to display on each page. Valid values: **30** to **100**.

 |
|PageNumber|Integer|No|1|The number of the page. Valid values: any non-zero positive integer. Default value: **1**.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Engine|String|MongoDB|The database engine.

 |
|Items| | |A list of slow operation log details.

 |
|└AccountName|String|root|The name of the user who performed the operation.

 |
|└DBName|String|mongodbtest|The name of the database.

 |
|└DocsExamined|Long|1000000|The number of documents scanned during the operation.

 |
|└ExecutionStartTime|String|2019-02-25T01:41:28Z|The start time of the operation. The time is in the *yyyy-MM-dd*T*HH:mm:ss*Z format.

 |
|└HostAddress|String|47.xxx.xxx.xx|The host IP address that you use to connect to a database.

 |
|└KeysExamined|Long|0|The data records that are scanned during indexing.

 |
|└QueryTimes|String|600|The execution duration of the statement. Unit: milliseconds.

 |
|└ReturnRowCounts|Long|0|The number of returned rows.

 |
|└SQLText|String|\{\\"op\\":\\"query\\",\\"ns\\":\\"mongodbtest.customer\\",\\"query\\":\{\\"find\\":\\"customer\\",\\"filter\\":\{\\"name\\":\\"jack\\"\}\}\}|The SQL statement that is executed during the slow operation.

 |
|PageNumber|Integer|1|The number of the page.

 |
|PageRecordCount|Integer|1|The number of slow operation logs on the page.

 |
|RequestId|String|414A4E5-4C36-4461-95FC-23757A20B5F8|The ID of the request.

 |
|TotalRecordCount|Integer|1|The total number of records.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeSlowLogRecords
&StartTime=2019-02-24T12:10Z
&EndTime=2019-02-26T12:10Z
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

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

`JSON` format

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

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

