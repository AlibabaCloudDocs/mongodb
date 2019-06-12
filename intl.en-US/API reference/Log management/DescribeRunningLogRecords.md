# DescribeRunningLogRecords {#doc_api_Dds_DescribeRunningLogRecords .reference}

You can call this operation to query the running logs of the MongoDB instance.

This operation is applicable to replica set instances and sharded cluster instances. DescribeRunningLogRecords cannot be performed on standalone instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeRunningLogRecords) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeRunningLogRecords|The operation that you want to perform. Set the value to **DescribeRunningLogRecords**.

 |
|StartTime|String|Yes|2019-01-01T12:10Z|The beginning of the time range that you want to query. The time is in the *yyyy-MM-dd*T*HH:mm*Z format.

 |
|EndTime|String|Yes|2019-01-02T12:10Z|The end of the time range that you want to query. The time is in the *yyyy-MM-dd*T*HH:mm*Z format.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** If you specify this parameter to the ID of a sharded cluster instance, you must also specify the **NodeId** parameter.

 |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the mongos or shard in the specified sharded cluster instance.

 **Note:** This parameter is only valid when you specify the **DBInstanceId** parameter to the ID of a sharded cluster instance.

 |
|DBName|String|No|mongodbtest|The name of the database.

 |
|RoleType|String|No|primary|The role of the node in the instance. Valid values:

 -   **primary**
-   **secondary**

 **Note:** If you set **NodeId** to the ID of a mongos, the value of **RoleType** must be **primary**.

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
|Items| | |A list of running log details.

 |
|└Category|String|NETWORK|The category of the logs.

 |
|└ConnInfo|String|conn18xxxxxx|The log connection information.

 |
|└Content|String|end connection 11.xxx.xxx.xx:3xxxx \(0 connections now open\)\\n|The content of log information.

 |
|└CreateTime|String|2019-02-26T12:09:34Z|The time when the log is generated. The time is in the *yyyy-MM-dd*T*HH:mm:ss*Z format.

 |
|PageNumber|Integer|1|The number of the page.

 |
|PageRecordCount|Integer|30|The number of records per page.

 |
|RequestId|String|45D2B592-DEBA-4347-BBF3-47FF6C97DBBC|The ID of the request.

 |
|TotalRecordCount|Integer|2|The total number of records.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeRunningLogRecords
&StartTime=2019-01-01T12:10Z
&EndTime=2019-01-02T12:10Z
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

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

`JSON` format

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

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

