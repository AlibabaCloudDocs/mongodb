# DescribeAuditRecords {#doc_api_Dds_DescribeAuditRecords .reference}

You can call this operation to query the records of audit logs of MongoDB instances.

When you call this operation, ensure that the audit log function of the instance is enabled. Otherwise, the operation will return an empty audit log.

**Note:** This operation is applicable to replica set instances and sharded cluster instances. DescribeAuditRecords cannot be performed on standalone instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeAuditRecords) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAuditRecords|The operation that you want to perform. Set the value to **DescribeAuditRecords**.

 |
|StartTime|String|Yes|2019-03-13T12:11:14Z|The beginning of the time range that you want to query. The time is in the *yyyy-MM-dd*T*HH:mm:ss*Z format.

 |
|EndTime|String|Yes|2019-03-13T13:11:14Z|The end of the time range that you want to query. The time is in the *yyyy-MM-dd*T*HH:mm:ss*Z format.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** If you specify this parameter to the ID of a sharded cluster instance, you must also specify the **NodeId** parameter.

 |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the mongos or shard in the specified sharded cluster instance.

 **Note:** This parameter is only valid when you specify the **DBInstanceId** parameter to the ID of a sharded cluster instance.

 |
|Database|String|No|testdatabase|The name of the database. If you do not specify this parameter, this operation returns records of all databases.

 |
|User|String|No|root|The user of the database. If you do not specify this parameter, this operation returns records of all users.

 |
|Form|String|No|Stream|The form of the audit log that the operation returns. Valid values:

 -   **File**: triggers the generation of audit logs. If this parameter is set to File, only common parameters are returned. In this case, you need to call the [DescribeAuditFiles](~~62162~~) operation to obtain the download address of the audit logs.
-   **Stream**: returns data streams.

 Default value: **Stream**.

 |
|QueryKeywords|String|No|slow|The keywords used for queries. Separate multiple keywords with spaces. The maximum number of keywords is 10.

 |
|PageSize|Integer|No|30|The number of records on each page. Valid values: **30**, **50**, and **100**. Default value: **30**.

 |
|PageNumber|Integer|No|1|The number of the page. Valid values: any non-zero positive integer. Default value: **1**.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Items| | |The detailed list of audit logs.

 |
|└AccountName|String|root|The user of the database.

 |
|└DBName|String|test123|The name of the database.

 |
|└ExecuteTime|String|2019-03-11T03:30:27Z|The time when the statement was executed. The time is in the *yyyy-MM-dd*T*HH:mm:ss*Z format.

 |
|└HostAddress|String|11.xxx.xxx.xxx|The IP address of the client.

 |
|└ReturnRowCounts|Long|2|The number of returned records.

 |
|└Syntax|String|\{ \\"atype\\" : \\"createCollection\\", \\"param\\" : \{ \\"ns\\" : \\"123.test1\\" \}, \\"result\\": \\"OK\\" \}|The statement that was executed.

 |
|└ThreadID|String|140682188297984|The ID of the thread.

 |
|└TotalExecutionTimes|Long|700|The duration of the statement execution. Unit: microseconds.

 |
|PageNumber|Integer|1|The number of the page.

 |
|PageRecordCount|Integer|30|The maximum number of records on the current page.

 |
|RequestId|String|3278BEB8-503B-4E46-8F7E-D26E040C9769|The ID of the request.

 |
|TotalRecordCount|Integer|40|The total number of records.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeAuditRecords
&StartTime=2019-03-13T12:11:14Z
&EndTime=2019-03-13T13:11:14Z
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeAuditRecordsResponse>
  <Items>
    <SQLRecord>
      <TotalExecutionTimes>703</TotalExecutionTimes>
      <Syntax>{ "atype" : "command", "param" : { "command" : "find", "ns" : "123.test1", "args" : { "find" : "test1", "filter" : { "x" : 1, "y" : 2 }, "shardVersion" : [ { "$timestamp" : { "t" : 0, "i" : 0 } }, { "$oid" : "000000000000000000000000" } ], "$clusterTime" : { "clusterTime" : { "$timestamp" : { "t" : 1552275017, "i" : 2 } }, "signature" : { "hash" : { "$binary" : "9qfygDs61fKCvdXJqjq+f0zML0E=", "$type" : "00" }, "keyId" : { "$numberLong" : "6666955498811555841" } } }, "$client" : { "application" : { "name" : "MongoDB Shell" }, "driver" : { "name" : "MongoDB Internal Client", "version" : "3.4.10" }, "os" : { "type" : "Linux", "name" : "Ubuntu", "architecture" : "x86_64", "version" : "16.04" }, "mongos" : { "host" : "rxxxxxx.cloud.cm10:3074", "client" : "47.xxx.xxx.xx:53854", "version" : "4.0.0" } }, "$configServerState" : { "opTime" : { "ts" : { "$timestamp" : { "t" : 1552275017, "i" : 2 } }, "t" : { "$numberLong" : "3" } } }, "$db" : "123" } }, "result": "OK" }</Syntax>
      <HostAddress>11.xxx.xxx.xx</HostAddress>
      <ExecuteTime>2019-03-11T03:30:27Z</ExecuteTime>
      <ThreadID>139xxxxxxxx</ThreadID>
      <AccountName>__system;</AccountName>
      <DBName>local;</DBName>
    </SQLRecord>
    <SQLRecord>
      <TotalExecutionTimes>0</TotalExecutionTimes>
      <Syntax>{ "atype" : "createIndex", "param" : { "ns" : "123.test1", "indexName" : "y_1", "indexSpec" : { "v" : 2, "key" : { "y" : 1 }, "name" : "y_1", "ns" : "123.test1" } }, "result": "OK" }</Syntax>
      <HostAddress/>
      <ExecuteTime>2019-03-11T03:30:06Z</ExecuteTime>
      <ThreadID>140xxxxxxxx</ThreadID>
      <AccountName>__system;</AccountName>
      <DBName>local;</DBName>
    </SQLRecord>
  </Items>
  <PageNumber>1</PageNumber>
  <TotalRecordCount>2</TotalRecordCount>
  <RequestId>3278BEB8-503B-4E46-8F7E-D26E040C9769</RequestId>
  <PageRecordCount>30</PageRecordCount>
</DescribeAuditRecordsResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"Items":{
		"SQLRecord":[
			{
				"TotalExecutionTimes":703,
				"Syntax":"{ \"atype\" : \"command\", \"param\" : { \"command\" : \"find\", \"ns\" : \"123.test1\", \"args\" : { \"find\" : \"test1\", \"filter\" : { \"x\" : 1, \"y\" : 2 }, \"shardVersion\" : [ { \"$timestamp\" : { \"t\" : 0, \"i\" : 0 } }, { \"$oid\" : \"000000000000000000000000\" } ], \"$clusterTime\" : { \"clusterTime\" : { \"$timestamp\" : { \"t\" : 1552275017, \"i\" : 2 } }, \"signature\" : { \"hash\" : { \"$binary\" : \"9qfygDs61fKCvdXJqjq+f0zML0E=\", \"$type\" : \"00\" }, \"keyId\" : { \"$numberLong\" : \"6666955498811555841\" } } }, \"$client\" : { \"application\" : { \"name\" : \"MongoDB Shell\" }, \"driver\" : { \"name\" : \"MongoDB Internal Client\", \"version\" : \"3.4.10\" }, \"os\" : { \"type\" : \"Linux\", \"name\" : \"Ubuntu\", \"architecture\" : \"x86_64\", \"version\" : \"16.04\" }, \"mongos\" : { \"host\" : \"rxxxxxx.cloud.cm10:3074\", \"client\" : \"47.xxx.xxx.xx:53854\", \"version\" : \"4.0.0\" } }, \"$configServerState\" : { \"opTime\" : { \"ts\" : { \"$timestamp\" : { \"t\" : 1552275017, \"i\" : 2 } }, \"t\" : { \"$numberLong\" : \"3\" } } }, \"$db\" : \"123\" } }, \"result\": \"OK\" }",
				"HostAddress":"11.xxx.xxx.xxx",
				"ExecuteTime":"2019-03-11T03:30:27Z",
				"ThreadID":"139xxxxxxxx",
				"AccountName":"__system;",
				"DBName":"local;"
			},
			{
				"TotalExecutionTimes":0,
				"Syntax":"{ \"atype\" : \"createIndex\", \"param\" : { \"ns\" : \"123.test1\", \"indexName\" : \"y_1\", \"indexSpec\" : { \"v\" : 2, \"key\" : { \"y\" : 1 }, \"name\" : \"y_1\", \"ns\" : \"123.test1\" } }, \"result\": \"OK\" }",
				"HostAddress":"",
				"ExecuteTime":"2019-03-11T03:30:06Z",
				"ThreadID":"140xxxxxxxx",
				"AccountName":"__system;",
				"DBName":"local;"
			}
		]
	},
	"TotalRecordCount":2,
	"PageNumber":1,
	"RequestId":"3278BEB8-503B-4E46-8F7E-D26E040C9769",
	"PageRecordCount":30
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidEndTime.Format|Specified end time is not valid.|The error message returned when you specified an invalid end time. Check whether the format of the time is correct.|

[View error codes](https://error-center.aliyun.com/status/product/Dds)

