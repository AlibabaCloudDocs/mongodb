# DescribeRunningLogRecords

You can call this operation to query the operational logs of an ApsaraDB for MongoDB instance.

-   This operation is applicable to replica set instances and sharded cluster instances, but not to standalone instances.
-   You can call this operation up to 30 times per minute. To call this operation at a higher frequency, use a Logstore. For more information, see [Manage a Logstore](~~48990~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeRunningLogRecords&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeRunningLogRecords|The operation that you want to perform. Set the value to **DescribeRunningLogRecords**. |
|StartTime|String|Yes|2019-01-01T12:10Z|The beginning of the time range to query. Specify the time in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC. |
|EndTime|String|Yes|2019-01-01T13:10Z|The end of the time range to query. The end time must be later than the start time. Specify the time in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC.

 **Note:** The end time must be within 24 hours from the start time. Otherwise, the query fails. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** If you set this parameter to the ID of a sharded cluster instance, you must also specify the **NodeId** parameter. |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the mongos or shard node in the specified sharded cluster instance.

 **Note:** This parameter takes effect only if you set the **DBInstanceId** parameter to the ID of a sharded cluster instance. |
|DBName|String|No|mongodbtest|The name of the database. |
|RoleType|String|No|primary|The role of the node in the instance. Valid values:

 -   **primary**
-   **secondary**

 **Note:** If you set the **NodeId** parameter to the ID of a mongos node, you must set the **RoleType** parameter to **primary**. |
|PageSize|Integer|No|30|The number of entries to return on each page. Valid values: **30** to **100**. |
|PageNumber|Integer|No|1|The number of the page to return. The value must be an integer that is larger than 0. Default value: **1**. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the region ID of the instance. |
|OrderType|String|No|asc|The order of time in which the operational log entries to return are sorted. Valid values:

 -   asc: The log entries are sorted by time in ascending order.
-   desc: The log entries are sorted by time in descending order. |
|ResourceGroupId|String|No|sg-bpxxxxxxxxxxxxxxxxxx|The ID of the resource group. |
|RoleId|String|No|651xxxxx|The role ID of the node. You can call the [DescribeReplicaSetRole](~~62134~~) operation to query the role ID. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Engine|String|MongoDB|The database engine. |
|Items|Array of LogRecords| |Details about the operational log entries. |
|LogRecords| | | |
|Category|String|NETWORK|The category of the log entry. |
|ConnInfo|String|conn18xxxxxx|The connection information of the log entry. |
|Content|String|end connection 11.xxx.xxx.xx:3xxxx \(0 connections now open\)\\n|The content of the log entry. |
|CreateTime|String|2019-02-26T12:09:34Z|The time when the log entry was generated. The time is in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|Id|Integer|1111111111|The ID of the log entry. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageRecordCount|Integer|30|The number of entries returned per page. |
|RequestId|String|45D2B592-DEBA-4347-BBF3-47FF6C97DBBC|The ID of the request. |
|TotalRecordCount|Integer|2|The total number of returned entries. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeRunningLogRecords
&StartTime=2019-01-01T12:10Z
&EndTime=2019-01-01T13:10Z
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
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

```
{
    "Items": {
        "LogRecords": [
            {
                "Category": "-",
                "CreateTime": "2019-02-26T12:09:34Z",
                "ConnInfo": "conn18xxxxxx",
                "Content": "end connection 11.xxx.xxx.xx:3xxxx (0 connections now open)\n"
            },
            {
                "Category": "NETWORK",
                "CreateTime": "2019-02-26T12:09:34Z",
                "ConnInfo": "thread1",
                "Content": "connection accepted from 11.xxx.xxx.xx:3xxxx #1862051 (11 connections now open)"
            }
        ]
    },
    "PageNumber": 1,
    "TotalRecordCount": 2,
    "RequestId": "45D2B592-DEBA-4347-BBF3-47FF6C97DBBC"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

