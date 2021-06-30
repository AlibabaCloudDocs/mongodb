# DescribeSlowLogRecords

调用DescribeSlowLogRecords接口查询MongoDB实例运行出现的慢日志明细。

-   本接口仅适用于副本集实例和分片集群实例。
-   本接口限制每分钟调用30次，如超过这个限制会被限流，请勿高频调用。如需高频调用，请使用Logstore，详情请参见[管理Logstore](~~48990~~)。
-   如果是2021年06月06日后新购买的实例，您需要先开通审计日志功能，并设置需要审计的操作类型（包含**admin**和**slow**），然后查看此后出现的慢日志。

    **说明：**

    -   您可以通过调用接口[ModifyAuditPolicy](~~131941~~)开启或关闭审计日志。
    -   您可以通过调用接口[ModifyAuditLogFilter](~~89033~~)设置需要审计的操作类型。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeSlowLogRecords&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeSlowLogRecords|系统规定参数。取值：**DescribeSlowLogRecords**。 |
|RegionId|String|否|cn-hangzhou|实例所属的地域ID。

 **说明：** 您可以通过调用接口[DescribeDBInstanceAttribute](~~62010~~)查询。 |
|DBInstanceId|String|是|dds-bp1fc7e65108\*\*\*\*|实例ID。

 **说明：** 如果是分片集群实例，您还需要配置`NodeId`。 |
|NodeId|String|否|d-bp18b06ebc21\*\*\*\*|Shard节点ID。

 **说明：** 如果`DBInstanceId`配置的是分片集群实例的ID，需要配置该参数。 |
|StartTime|String|是|2019-02-24T 12:10:10Z|查询开始时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。 |
|EndTime|String|是|2019-02-24T 13:10:10Z|查询结束时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 **说明：**

-   必须晚于查询开始时间。
-   查询结束时间距查询开始时间不得超过24个小时，超过则调用失败。 |
|DBName|String|否|mongodbtest|数据库名。 |
|PageSize|Integer|否|30|每页记录数，取值范围为**30**~**100**。 |
|PageNumber|Integer|否|1|页码，取值为大于0且不超过Integer数据类型的最大值，默认值为**1**。 |
|OrderType|String|否|asc|按时间的升降序对查询到的慢日志进行排序。取值如下：

 -   asc：按时间升序排序。
-   desc：按时间降序排序。 |
|ResourceGroupId|String|否|rg-acfmyiu4ekp\*\*\*\*|资源组ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|TotalRecordCount|Integer|1|总记录数。 |
|PageRecordCount|Integer|1|本页慢操作日志明细的个数。 |
|RequestId|String|414A4E5-4C36-4461-95FC-23757A20\*\*\*\*|请求ID。 |
|PageNumber|Integer|1|页码，取值为大于0且不超过Integer数据类型的最大值，默认值为**1**。 |
|Items|Array of LogRecords| |慢日志明细列表。 |
|LogRecords| | | |
|ExecutionStartTime|String|2019-02-25T 01:41:28Z|操作执行的开始时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。 |
|HostAddress|String|192.168.XX.XX|连接数据库的主机地址。 |
|QueryTimes|String|600|该语句的执行时长，单位为毫秒。 |
|TableName|String|C1|MongoDB的集合名称。 |
|SQLText|String|\{\\"op\\":\\"query\\",\\"ns\\":\\"mongodbtest.customer\\",\\"query\\":\{\\"find\\":\\"customer\\",\\"filter\\":\{\\"name\\":\\"jack\\"\}\}\}|慢操作执行的语句。 |
|ReturnRowCounts|Long|0|返回行数。 |
|KeysExamined|Long|0|索引扫描行数。 |
|DBName|String|mongodbtest|数据库名。 |
|DocsExamined|Long|1000000|该操作执行时扫描的文档数。 |
|AccountName|String|root|执行该操作的数据库用户名。 |
|Engine|String|MongoDB|当前数据库的引擎类型。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=DescribeSlowLogRecords
&DBInstanceId=dds-bp1fc7e65108****
&NodeId=d-bp18b06ebc21****
&StartTime=2019-02-24T 12:10:10Z
&EndTime=2019-02-24T 13:10:10Z
&DBName=mongodbtest
&PageSize=30
&PageNumber=1
&OrderType=asc
&ResourceGroupId=rg-acfmyiu4ekp****
&公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeSlowLogRecordsResponse>
    <TotalRecordCount>1</TotalRecordCount>
    <PageRecordCount>1</PageRecordCount>
    <RequestId>414A4E5-4C36-4461-95FC-23757A20****</RequestId>
    <PageNumber>1</PageNumber>
    <Items>
        <ExecutionStartTime>2019-02-25T 01:41:28Z</ExecutionStartTime>
        <HostAddress>192.168.XX.XX</HostAddress>
        <QueryTimes>600</QueryTimes>
        <TableName>C1</TableName>
        <SQLText>{\"op\":\"query\",\"ns\":\"mongodbtest.customer\",\"query\":{\"find\":\"customer\",\"filter\":{\"name\":\"jack\"}}}</SQLText>
        <ReturnRowCounts>0</ReturnRowCounts>
        <KeysExamined>0</KeysExamined>
        <DBName>mongodbtest</DBName>
        <DocsExamined>1000000</DocsExamined>
        <AccountName>root</AccountName>
    </Items>
    <Engine>MongoDB</Engine>
</DescribeSlowLogRecordsResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "TotalRecordCount" : 1,
  "PageRecordCount" : 1,
  "RequestId" : "414A4E5-4C36-4461-95FC-23757A20****",
  "PageNumber" : 1,
  "Items" : [ {
    "ExecutionStartTime" : "2019-02-25T 01:41:28Z",
    "HostAddress" : "192.168.XX.XX",
    "QueryTimes" : "600",
    "TableName" : "C1",
    "SQLText" : "{\\\"op\\\":\\\"query\\\",\\\"ns\\\":\\\"mongodbtest.customer\\\",\\\"query\\\":{\\\"find\\\":\\\"customer\\\",\\\"filter\\\":{\\\"name\\\":\\\"jack\\\"}}}",
    "ReturnRowCounts" : 0,
    "KeysExamined" : 0,
    "DBName" : "mongodbtest",
    "DocsExamined" : 1000000,
    "AccountName" : "root"
  } ],
  "Engine" : "MongoDB"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

