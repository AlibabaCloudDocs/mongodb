# DescribeSlowLogRecords

You can call this operation to query entries in the slow query log of an ApsaraDB for MongoDB instance.

-   This operation is applicable to replica set instances and sharded cluster instances, but cannot be performed on standalone instances.
-   You can call this operation up to 30 times per minute. To call this operation at a higher frequency, use a Logstore. For more information, see [Manage a Logstore](~~48990~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeSlowLogRecords&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeSlowLogRecords|The operation that you want to perform. Set the value to **DescribeSlowLogRecords**. |
|StartTime|String|Yes|2019-02-24T12:10Z|The beginning of the time range to query. Specify the time in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC. |
|EndTime|String|Yes|2019-02-26T12:10Z|The end of the time range to query. The end time must be later than the start time. The time range cannot exceed one month. Specify the time in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

**Note:** If you set this parameter to the ID of a sharded cluster instance, you must also specify the **NodeId** parameter. |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the shard.

**Note:** This parameter is valid only if you set the **DBInstanceId** parameter to the ID of a sharded cluster instance. |
|DBName|String|No|mongodbtest|The name of the database. |
|PageSize|Integer|No|30|The number of entries to return on each page. Valid values: **30** to **100** |
|PageNumber|Integer|No|1|The number of the page to return. The value must be a positive integer. Default value: **1**. |
|RegionId|String|No|cn-hangzhou|The ID of the region where the instance is deployed. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the region ID. |
|OrderType|String|No|asc|The order of time in which the log entries to return are sorted. Valid values:

-   asc: The log entries are sorted by time in ascending order.
-   desc: The log entries are sorted by time in descending order. |
|ResourceGroupId|String|No|sg-bpxxxxxxxxxxxxxxxxxx|The ID of the resource group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Engine|String|MongoDB|The database engine. |
|Items|Array| |The list of entries in the slow query log. |
|LogRecords| | | |
|AccountName|String|root|The user name of the database account that performs the operation. |
|DBName|String|mongodbtest|The name of the database. |
|DocsExamined|Long|1000000|The number of documents that are scanned during the operation. |
|ExecutionStartTime|String|2019-02-25T01:41:28Z|The start time of the operation. Specify the time in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|HostAddress|String|47.xxx.xxx.xx|The host IP address that is used to connect to the database. |
|KeysExamined|Long|0|The data entries that are scanned during indexing. |
|QueryTimes|String|600|The execution time of the statement. Unit: milliseconds. |
|ReturnRowCounts|Long|0|The number of entries returned. |
|SQLText|String|\{\\"op\\":\\"query\\",\\"ns\\":\\"mongodbtest.customer\\",\\"query\\":\{\\"find\\":\\"customer\\",\\"filter\\":\{\\"name\\":\\"jack\\"\}\}\}|The SQL statement that is executed during the slow operation. |
|TableName|String|C1|The name of the ApsaraDB for MongoDB collection. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageRecordCount|Integer|1|The number of log entries on the page. |
|RequestId|String|414A4E5-4C36-4461-95FC-23757A20B5F8|The ID of the request. |
|TotalRecordCount|Integer|1|The total number of entries. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeSlowLogRecords
&StartTime=2019-02-24T12:10Z
&EndTime=2019-02-26T12:10Z
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
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

```
{
    "Items": {
        "LogRecords": [
            {
                "ReturnRowCounts": 0,
                "KeysExamined": "0",
                "HostAddress": "47.110.74.177",
                "SQLText": "{\"op\":\"query\",\"ns\":\"mongodbtest.customer\",\"query\":{\"find\":\"customer\",\"filter\":{\"name\":\"ajackeyifeo1w\"}}}",
                "ExecutionStartTime": "2019-02-25T01:41:28Z",
                "AccountName": "root",
                "QueryTimes": 600,
                "DocsExamined": "1000000",
                "DBName": "mongodbtest"
            }
        ]
    },
    "PageNumber": 1,
    "TotalRecordCount": 1,
    "RequestId": "5414A4E5-4C36-4461-95FC-23757A20B5F8",
    "Engine": "MongoDB",
    "PageRecordCount": 1
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

