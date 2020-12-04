# DescribeAuditRecords

You can call this operation to query the audit log of an ApsaraDB for MongoDB instance.

-   When you call this operation, ensure that the audit log feature of the instance is enabled. Otherwise, the operation returns an empty audit log.
-   This operation is applicable to replica set instances and sharded cluster instances, but cannot be performed on standalone instances.
-   You can call this operation up to 30 times per minute. To call this operation at a higher frequency, use a Logstore. For more information, see [Manage a Logstore](~~48990~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeAuditRecords&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAuditRecords|The operation that you want to perform. Set the value to **DescribeAuditRecords**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

**Note:** If you set this parameter to the ID of a sharded cluster instance, you must also specify the **NodeId** parameter. |
|EndTime|String|Yes|2019-03-13T13:11:14Z|The end of the time range to query. The end time must be later than the start time. Specify the time in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC.

**Note:** The end time must be within 24 hours from the start time. Otherwise, the query fails. |
|StartTime|String|Yes|2019-03-13T12:11:14Z|The beginning of the time range to query. Specify the time in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|RegionId|String|No|cn-hangzhou|The ID of the region where the instance is deployed. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the region ID. |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the mongos or shard in the specified sharded cluster instance.

**Note:** This parameter is valid only if you set the **DBInstanceId** parameter to the ID of a sharded cluster instance. |
|Database|String|No|testdatabase|The name of the database. If you do not specify this parameter, this operation returns records of all databases. |
|User|String|No|root|The user of the database. If you do not specify this parameter, this operation returns records of all users. |
|Form|String|No|Stream|The form of the audit log that the operation returns. Valid values:

-   **File**: triggers the generation of audit logs. If this parameter is set to File, only common parameters are returned. In this case, you need to call the [DescribeAuditFiles](~~62162~~) operation to query the download address of the audit log.
-   **Stream**: returns data streams.

Default value: **Stream**. |
|QueryKeywords|String|No|slow|The keywords used for queries. Separate multiple keywords with spaces. The maximum number of keywords is 10. |
|PageSize|Integer|No|30|The number of entries to return on each page. Valid values: **30**, **50**, and **100**. Default value: **30**. |
|PageNumber|Integer|No|1|The number of the page to return. The value must be a positive integer. Default value: **1**. |
|OrderType|String|No|asc|The order of time in which the log entries to return are sorted. Valid values:

-   asc: The log entries are sorted by time in ascending order.
-   desc: The log entries are sorted by time in descending order. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Items|Array| |The list of entries in the audit log. |
|SQLRecord| | | |
|AccountName|String|root|The user of the database. |
|DBName|String|test123|The name of the database. |
|ExecuteTime|String|2019-03-11T03:30:27Z|The time when the statement was executed. Specify the time in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|HostAddress|String|11.xxx.xxx.xxx|The IP address of the client. |
|ReturnRowCounts|Long|2|The number of entries returned. |
|Syntax|String|\{ \\"atype\\" : \\"createCollection\\", \\"param\\" : \{ \\"ns\\" : \\"123.test1\\" \}, \\"result\\": \\"OK\\" \}|The statement that was executed. |
|TableName|String|C1|The name of the ApsaraDB for MongoDB collection. |
|ThreadID|String|140682188297984|The ID of the thread. |
|TotalExecutionTimes|Long|700|The duration of the statement execution. Unit: microseconds. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageRecordCount|Integer|30|The maximum number of entries on the current page. |
|RequestId|String|3278BEB8-503B-4E46-8F7E-D26E040C9769|The ID of the request. |
|TotalRecordCount|Integer|40|The total number of entries. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeAuditRecords
&StartTime=2019-03-13T12:11:14Z
&EndTime=2019-03-13T13:11:14Z
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
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
                  <HostAddress></HostAddress>
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

```
{
    "Items": {
        "SQLRecord": [
            {
                "TotalExecutionTimes": 703,
                "Syntax": "{ \"atype\" : \"command\", \"param\" : { \"command\" : \"find\", \"ns\" : \"123.test1\", \"args\" : { \"find\" : \"test1\", \"filter\" : { \"x\" : 1, \"y\" : 2 }, \"shardVersion\" : [ { \"$timestamp\" : { \"t\" : 0, \"i\" : 0 } }, { \"$oid\" : \"000000000000000000000000\" } ], \"$clusterTime\" : { \"clusterTime\" : { \"$timestamp\" : { \"t\" : 1552275017, \"i\" : 2 } }, \"signature\" : { \"hash\" : { \"$binary\" : \"9qfygDs61fKCvdXJqjq+f0zML0E=\", \"$type\" : \"00\" }, \"keyId\" : { \"$numberLong\" : \"6666955498811555841\" } } }, \"$client\" : { \"application\" : { \"name\" : \"MongoDB Shell\" }, \"driver\" : { \"name\" : \"MongoDB Internal Client\", \"version\" : \"3.4.10\" }, \"os\" : { \"type\" : \"Linux\", \"name\" : \"Ubuntu\", \"architecture\" : \"x86_64\", \"version\" : \"16.04\" }, \"mongos\" : { \"host\" : \"rxxxxxx.cloud.cm10:3074\", \"client\" : \"47.xxx.xxx.xx:53854\", \"version\" : \"4.0.0\" } }, \"$configServerState\" : { \"opTime\" : { \"ts\" : { \"$timestamp\" : { \"t\" : 1552275017, \"i\" : 2 } }, \"t\" : { \"$numberLong\" : \"3\" } } }, \"$db\" : \"123\" } }, \"result\": \"OK\" }",
                "HostAddress": "11.xxx.xxx.xxx",
                "ExecuteTime": "2019-03-11T03:30:27Z",
                "ThreadID": "139xxxxxxxx",
                "AccountName": "__system;",
                "DBName": "local;"
            },
            {
                "TotalExecutionTimes": 0,
                "Syntax": "{ \"atype\" : \"createIndex\", \"param\" : { \"ns\" : \"123.test1\", \"indexName\" : \"y_1\", \"indexSpec\" : { \"v\" : 2, \"key\" : { \"y\" : 1 }, \"name\" : \"y_1\", \"ns\" : \"123.test1\" } }, \"result\": \"OK\" }",
                "HostAddress": "",
                "ExecuteTime": "2019-03-11T03:30:06Z",
                "ThreadID": "140xxxxxxxx",
                "AccountName": "__system;",
                "DBName": "local;"
            }
        ]
    },
    "PageNumber": 1,
    "TotalRecordCount": 2,
    "RequestId": "3278BEB8-503B-4E46-8F7E-D26E040C9769",
    "PageRecordCount": 30
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|400|InvalidEndTime.Format|Specified end time is not valid.|The error message returned because the end of the time range to query is invalid. Check the format of the specified time.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

