# DescribeBackups {#doc_api_Dds_DescribeBackups .reference}

You can call this operation to query the backups of a MongoDB instance.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeBackups) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|StartTime|String|Yes|2019-03-12T12:00Z|The start time of the query. It must be in the *yyyy-MM-dd*T*HH:mm:*Z format.

 |
|EndTime|String|Yes|2019-03-13T12:00Z|The end time of the query. It must be later than the start time. The format is *yyyy-MM-dd*T*HH: mm*Z.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** If you set this parameter to the ID of a sharded cluster instance, you must also specify **the NodeId** parameter at the same time.

 |
|Action|String|No|DescribeBackups|The operation that you want to perform. Set the value to **DescribeBackups**.

 |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the shard in the sharded cluster instance.

 **Note:** This parameter can be used only when **DBInstanceId**is the ID of the sharded cluster instance.

 |
|BackupId|String|No|5664xxxx|The ID of the backup.

 |
|PageNumber|Integer|No|1|The number of the page. This value must be a non-zero positive integer. Default value: **1**.

 |
|PageSize|Integer|No|30|The number of records on each page. Valid values: **30, 50, and 100.**Default value: **30**.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The number of the page.

 |
|PageSize|Integer|30|The number of records on each page.

 |
|RequestId|String|8925E66F-1971-4C8C-90A7-F93BF1867E25|The ID of the request.

 |
|TotalCount|Integer|1|The total number of backups.

 |
|Backups| | |The detailed list of all returned backups.

 |
|└BackupDBNames|String|mongodbtest, new, test|The name of the backup database.

 |
|└BackupDownloadURL|String|http://xxxxx.oss-cn-hangzhou.aliyuncs.com/xxxxx/hinsxxxxx\_data\_xxxxx.tar.gz|The download URL of the backup file. If the download URL is unavailable, this parameter is an empty string.

 |
|└BackupEndTime|String|2019-03-13T04:34:57Z|The end time of the backup. The format is *yyyy-MM-dd*T*HH: mm:ss*Z.

 |
|└BackupId|Integer|11111111|The ID of the backup.

 |
|└BackupMethod|String|Physical|The backup method.

 -   **Snapshot**
-   **Physical**
-   **Logical**

 |
|└BackupMode|String|Automated|The backup mode.

 -   **Automated**
-   **Manual**

 |
|└BackupSize|Long|335520510|The size of the backup file. Unit: Bytes.

 |
|└BackupStartTime|String|2019-03-13T04:32:42Z|The start time of the backup. The format is *yyyy-MM-dd*T*HH:mm:ss*Z.

 |
|└BackupStatus|String|Success|The state of the backup.

 -   **Success**: The backup is successful.
-   **Failed**: The backup has failed.

 |
|└BackupType|String|FullBackup|The backup type.

 -   **FullBackup**
-   **IncrementalBackup**

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? &Action= DescribeBackups
&StartTime=2019-03-12T12:00Z 
&EndTime=2019-03-13T12:00Z 
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeBackupsResponse>
  <PageNumber>1</PageNumber>
  <TotalCount>1</TotalCount>
  <PageSize>30</PageSize>
  <RequestId>8925E66F-1971-4C8C-90A7-F93BF1867E25</RequestId> 
  <Backups>
    <Backup>
      <BackupDownloadURL>http://xxxxx.oss-cn-hangzhou.aliyuncs.com/xxxxx/xxxxxx.tar.gz</BackupDownloadURL>
      <BackupType>FullBackup</BackupType>
      <BackupDBNames>mongodbtest,new,test</BackupDBNames>
      <BackupEndTime>2019-03-13T04:34:57Z</BackupEndTime>
      <BackupMethod>Physical</BackupMethod> 
      <BackupMode>Automated</BackupMode>
      <BackupSize>204595200</BackupSize> 
      <BackupStatus>Success</BackupStatus> 
      <BackupStartTime>2019-03-13T04:32:42Z</BackupStartTime> 
      <BackupId>11111111</BackupId>
    </Backup> 
  </Backups> 
</DescribeBackupsResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":30,
	"RequestId":"8925E66F-1971-4C8C-90A7-F93BF1867E25",
	"Backups":{
		"Backup":[
			{
				"BackupDownloadURL":"http://xxxxx.oss-cn-hangzhou.aliyuncs.com/xxxxx/xxxxxx.tar.gz",
				"BackupType":"FullBackup",
				"BackupDBNames":"mongodbtest,new,test",
				"BackupEndTime":"2019-03-13T04:34:57Z",
				"BackupMode":"Automated",
				"BackupMethod":"Physical",
				"BackupStatus":"Success",
				"BackupSize":204595200,
				"BackupId":11111111,
				"BackupStartTime":"2019-03-13T04:32:42Z"
			}
		]
	}
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

