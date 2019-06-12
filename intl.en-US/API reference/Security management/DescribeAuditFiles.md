# DescribeAuditFiles {#doc_api_Dds_DescribeAuditFiles .reference}

You can call this operation to query the audit log files of MongoDB instances.

This operation is applicable to replica set instances and sharded cluster instances. DescribeAuditFiles cannot be performed on standalone instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeAuditFiles) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAuditFiles|The operation that you want to perform. Set the value to **DescribeAuditFiles**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the mongos or shard in the specified sharded cluster instance.

 **Note:** If you do not specify this parameter, the audit logs of all mongos and shards will be returned.

 |
|PageSize|Integer|No|30|The number of records on each page. Valid values: **30, 50, and 100**. Default value: **30**.

 |
|PageNumber|Integer|No|1|The number of the page. Valid values: any non-zero positive integer. Default value: **1**.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Items| | |The information about all audit files.

 |
|└FileID|Integer|406505|The ID of the file.

 |
|└LogDownloadURL|String|http://xxxxxxxx.oss-cn-hangzhou.aliyuncs.com/custinsxxxxxx/custinsxxxxxx\_xxxxxx.csv|The download link for audit log files.

 **Note:** If the download link is unavailable, this parameter is empty.

 |
|└LogEndTime|String|2019-03-12T09:23:15Z|The end time of the audit log.

 |
|└LogSize|Long|98|The size of the audit log file. Unit: Bytes.

 |
|└LogStartTime|String|2019-03-11T08:19:29Z|The start time of the audit log.

 |
|└LogStatus|String|Success|The status of the audit log file.

 -   **Success**: The audit log files are archived.
-   **Failed**: The audit log files failed to be archived.
-   **Generating**: The audit log files are in the process of being archived.
-   **Initializing**: Archiving is not started.

 |
|PageNumber|Integer|1|The number of the page.

 |
|PageRecordCount|Integer|1|The number of records on the current page.

 |
|RequestId|String|F8CA8312-530A-413A-9129-F2BB32A8D404|The ID of the request.

 |
|TotalRecordCount|Integer|1|The total number of records.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeAuditFiles
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeAuditFilesResponse>
  <Items>
    <LogFile>
      <LogStartTime>2019-03-11T08:19:29Z</LogStartTime>
      <LogEndTime>2019-03-12T09:23:15Z</LogEndTime>
      <LogStatus>Success</LogStatus>
      <FileID>406505</FileID>
      <LogDownloadURL>http://xxxxxxxx.oss-cn-hangzhou.aliyuncs.com/custinsxxxxxx/custinsxxxxxx_xxxxxx.csv</LogDownloadURL>
      <LogSize>98</LogSize>
    </LogFile>
  </Items>
  <PageNumber>1</PageNumber>
  <TotalRecordCount>1</TotalRecordCount>
  <RequestId>F8CA8312-530A-413A-9129-F2BB32A8D404</RequestId>
  <PageRecordCount>1</PageRecordCount>
</DescribeAuditFilesResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"Items":{
		"LogFile":[
			{
				"LogStartTime":"2019-03-11T08:19:29Z",
				"LogEndTime":"2019-03-12T09:23:15Z",
				"LogStatus":"Success",
				"FileID":406505,
				"LogDownloadURL":"http://xxxxxxxx.oss-cn-hangzhou.aliyuncs.com/custinsxxxxxx/custinsxxxxxx_xxxxxx.csv",
				"LogSize":98
			}
		]
	},
	"TotalRecordCount":1,
	"PageNumber":1,
	"RequestId":"F8CA8312-530A-413A-9129-F2BB32A8D404",
	"PageRecordCount":1
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidDBInstanceClass.NotFound|Specified DB instance class is not found.|The error message returned when the specified instance type does not exists. Verify the specified instance type.|
|403|IncorrectDBInstanceType|Current DB instance type does not support this operation.|The error message returned when the current operation is not supported by the instance type of the specified instance.|

[View error codes](https://error-center.aliyun.com/status/product/Dds)

