# DescribeAuditRecords

调用DescribeAuditRecords接口查询MongoDB实例的审计日志。

-   调用本接口时，实例的审计日志须处于开通状态，否则返回的审计日志内容为空。
-   本接口适用于副本集实例和分片集群实例，暂不支持单节点实例。
-   本接口限制每分钟调用30次，如超过这个限制会被限流，请勿高频调用。如需高频调用，请使用Logstore，详情请参见[管理Logstore](~~48990~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeAuditRecords&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeAuditRecords|要执行的操作，取值：**DescribeAuditRecords**。 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 **说明：** 当本参数传入的是分片集群实例ID时，还需要传入**NodeId**参数。 |
|EndTime|String|是|2019-03-13T13:11:14Z|查询结束时间，必须晚于查询开始时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 **说明：** 查询结束时间距查询开始时间不得超过24个小时，超过则调用失败。 |
|StartTime|String|是|2019-03-13T12:11:14Z|查询开始时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。 |
|RegionId|String|否|cn-hangzhou|实例所属的地域ID，您可以通过调用[DescribeDBInstanceAttribute](~~62010~~)进行查询。 |
|NodeId|String|否|d-bpxxxxxxxx|分片集群实例中Mongos节点ID或Shard节点ID。

 **说明：** 当**DBInstanceId**参数传入的是分片集群实例ID时，本参数才可用。 |
|Database|String|否|testdatabase|数据库名，默认为所有数据库。 |
|User|String|否|root|数据库账号，默认为所有账号。 |
|Form|String|否|Stream|审计记录返回的展示类型，取值：

 -   **File**：触发审计日志文件的生成，若传入这个值，只返回公共参数，需再调用[DescribeAuditFiles](~~62162~~)获取文件的下载地址。
-   **Stream**：返回数据流。

 默认为**Stream**。 |
|QueryKeywords|String|否|slow|关键字查询，多个关键字以空格分隔，不超过10个关键字。 |
|PageSize|Integer|否|30|每页记录数，取值：**30**、**50**、**100**，默认值为**30**。 |
|PageNumber|Integer|否|1|页码，大于0，且不超过Integer的最大值，默认值为**1**。 |
|OrderType|String|否|asc|按时间的升降序对查询到的慢日志进行排序。取值：

 -   asc：按时间升序排序。
-   desc：按时间降序排序。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Items|Array of SQLRecord| |审计日志详情列表。 |
|SQLRecord| | | |
|AccountName|String|root|数据库账号名。 |
|DBName|String|test123|数据库名。 |
|ExecuteTime|String|2019-03-11T03:30:27Z|该语句执行的时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。 |
|HostAddress|String|11.xxx.xxx.xxx|客户端IP地址。 |
|ReturnRowCounts|Long|2|返回记录数。 |
|Syntax|String|\{ \\"atype\\" : \\"createCollection\\", \\"param\\" : \{ \\"ns\\" : \\"123.test1\\" \}, \\"result\\": \\"OK\\" \}|执行语句。 |
|TableName|String|C1|MongoDB的集合名称。 |
|ThreadID|String|140682188297984|线程ID。 |
|TotalExecutionTimes|Long|700|消耗时间，单位为微秒。 |
|PageNumber|Integer|1|页码。 |
|PageRecordCount|Integer|30|当前页最大记录数。 |
|RequestId|String|3278BEB8-503B-4E46-8F7E-D26E040C9769|请求ID。 |
|TotalRecordCount|Integer|40|总记录数。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=DescribeAuditRecords
&StartTime=2019-03-13T12:11:14Z
&EndTime=2019-03-13T13:11:14Z
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>
```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidEndTime.Format|Specified end time is not valid.|输入的结束时间无效，请您检查输入的时间格式是否正确。|

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

