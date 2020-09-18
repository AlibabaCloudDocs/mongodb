# DescribeErrorLogRecords

You can call this operation to query the error log of an ApsaraDB for MongoDB instance.

-   This operation is applicable to replica set instances and sharded cluster instances, but cannot be performed on standalone instances.
-   You can call this operation up to 30 times per minute. To call this operation at a higher frequency, use a Logstore. For more information, see [Manage a Logstore](~~48990~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeErrorLogRecords&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeErrorLogRecords|The operation that you want to perform. Set the value to **DescribeErrorLogRecords**. |
|StartTime|String|Yes|2019-01-01T12:10Z|The beginning of the time range to query. Specify the time in the *YYYY-MM-DD*T*HH:MM*Z format. The time must be in UTC. |
|EndTime|String|Yes|2019-01-02T12:10Z|The end of the time range to query. The end time must be later than the start time. Specify the time in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

**Note:** If you set this parameter to the ID of a sharded cluster instance, you must also specify the **NodeId** parameter. |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the mongos or shard in the specified sharded cluster instance.

**Note:** This parameter is valid only if you set the **DBInstanceId** parameter to the ID of a sharded cluster instance. |
|RoleType|String|No|primary|The role of the node in the instance. Valid values:

-   **primary**
-   **secondary**

**Note:** If you set **NodeId** to the ID of a mongos, the value of this parameter must be **primary**. |
|DBName|String|No|mongodbtest|The name of the database. |
|PageSize|Integer|No|30|The number of entries to return on each page. Valid values: **30** to **100** |
|PageNumber|Integer|No|1|The number of the page to return. The value must be a positive integer. Default value: **1**. |
|RegionId|String|No|cn-hangzhou|The ID of the region where the instance is deployed. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the region ID. |
|ResourceGroupId|String|No|sg-bpxxxxxxxxxxxxxxxxxx|The ID of the resource group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Engine|String|MongoDB|The database engine. |
|Items|Array| |The list of entries in the error log. |
|LogRecords| | | |
|Category|String|NETWORK|The category of the log entry. Valid values: Valid values:

-   NETWORK: network connections
-   ACCESS: access control
-   -: general information
-   COMMAND: slow queries
-   SHARDING: cluster
-   STORAGE: storage engine
-   CONNPOOL: connection pool
-   ASIO: asynchronous I/O operations
-   WRITE: slow updates |
|ConnInfo|String|conn18xxxxxx|The log connection information. |
|Content|String|xxxxxxxx|The content of the log entry. |
|CreateTime|String|2019-02-26T12:09:34Z|The time when the log entry was generated. Specify the time in the *YYYY-MM-DD*T*HH:MM:SS*Z format. The time must be in UTC. |
|Id|Integer|1111111111|The ID of the log entry. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageRecordCount|Integer|1|The number of entries returned per page. |
|RequestId|String|68BCBEC2-1E66-471F-A1A8-E3C60C0A80B0|The ID of the request. |
|TotalRecordCount|Integer|1|The total number of entries. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeErrorLogRecords
&StartTime=2019-01-01T12:10Z
&EndTime=2019-01-02T12:10Z
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeErrorLogRecordsResponse>
      <Items>
            <LogRecords>
                  <Category>NETWORK</Category>
                  <CreateTime>2019-02-26T12:09:34Z</CreateTime>
                  <ConnInfo>conn18xxxxxx</ConnInfo>
                  <Content>xxxxxxxx</Content>
            </LogRecords>
      </Items>
      <PageNumber>1</PageNumber>
      <TotalRecordCount>2</TotalRecordCount>
      <RequestId>68BCBEC2-1E66-471F-A1A8-E3C60C0A80B0</RequestId>
</DescribeErrorLogRecordsResponse>
```

`JSON` format

```
{
    "Items": {
        "LogRecords": [
            {
                "Category": "NETWORK",
                "CreateTime": "2019-02-26T12:09:34Z",
                "ConnInfo": "conn18xxxxxx",
                "Content": "xxxxxxxx"
            }
        ]
    },
    "PageNumber": 1,
    "TotalRecordCount": 2,
    "RequestId": "68BCBEC2-1E66-471F-A1A8-E3C60C0A80B0"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

