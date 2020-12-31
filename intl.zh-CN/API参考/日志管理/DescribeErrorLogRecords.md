# DescribeErrorLogRecords

调用DescribeErrorLogRecords接口查询MongoDB实例的错误日志。

-   本接口适用于副本集实例和分片集群实例，暂不支持单节点实例。
-   本接口限制每分钟调用30次，如超过这个限制会被限流，请勿高频调用。如需高频调用，请使用Logstore，详情请参见[管理Logstore](~~48990~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeErrorLogRecords&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeErrorLogRecords|要执行的操作，取值：**DescribeErrorLogRecords**。 |
|StartTime|String|是|2019-01-01T12:10Z|查询开始时间，格式为*YYYY-MM-DD*T*HH:MM*Z（UTC时间）。 |
|EndTime|String|是|2019-01-02T12:10Z|查询结束时间，必须晚于查询开始时间，格式为*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 **说明：** 当本参数传入的是分片集群实例ID时，还需要传入**NodeId**参数。 |
|NodeId|String|否|d-bpxxxxxxxx|分片集群实例中Mongos节点ID或Shard节点ID。

 **说明：** 当**DBInstanceId**参数传入的是分片集群实例ID时，本参数才可用。 |
|RoleType|String|否|primary|实例中节点的角色。取值：

 -   **primary**：主节点。
-   **secondary**：从节点。

 **说明：** 当**NodeId**参数传入的是Mongos节点ID时，本参数取值只能为**primary**。 |
|DBName|String|否|mongodbtest|数据库名。 |
|PageSize|Integer|否|30|每页记录数，取值范围：**30**~**100**。 |
|PageNumber|Integer|否|1|页码，取值为大于0且不超过Integer数据类型的最大值，默认值为**1**。 |
|RegionId|String|否|cn-hangzhou|实例所属的地域ID，您可以通过调用[DescribeDBInstanceAttribute](~~62010~~)进行查询。 |
|ResourceGroupId|String|否|sg-bpxxxxxxxxxxxxxxxxxx|资源组ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Engine|String|MongoDB|当前数据库的引擎类型。 |
|Items|Array of LogRecords| |错误日志明细列表。 |
|LogRecords| | | |
|Category|String|NETWORK|日志类别。返回值：

 -   NETWORK：网络链接日志。
-   ACCESS：访问控制日志。
-   -：普通日志。
-   COMMAND：慢日志。
-   SHARDING：集群日志。
-   STORAGE：存储引擎日志。
-   CONNPOOL：连接池日志。
-   ASIO：异步IO日志。
-   WRITE：慢更新日志。 |
|ConnInfo|String|conn18xxxxxx|日志连接信息。 |
|Content|String|xxxxxxxx|日志信息。 |
|CreateTime|String|2019-02-26T12:09:34Z|日志生成时间，格式为*YYYY-MM-DD*T*HH:MM:SS*Z（UTC时间）。 |
|Id|Integer|1111111111|日志ID。 |
|PageNumber|Integer|1|页码。 |
|PageRecordCount|Integer|1|每页的记录数。 |
|RequestId|String|68BCBEC2-1E66-471F-A1A8-E3C60C0A80B0|请求ID。 |
|TotalRecordCount|Integer|1|总记录数。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=DescribeErrorLogRecords
&StartTime=2019-01-01T12:10Z
&EndTime=2019-01-02T12:10Z
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>
```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

