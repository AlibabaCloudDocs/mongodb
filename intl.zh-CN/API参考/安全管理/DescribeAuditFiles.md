# DescribeAuditFiles {#doc_api_Dds_DescribeAuditFiles .reference}

调用DescribeAuditFiles接口查询MongoDB实例的审计日志文件。

本接口适用于副本集实例和分片集群实例，暂不支持单节点实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=DescribeAuditFiles)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeAuditFiles|要执行的操作，取值：**DescribeAuditFiles**。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|NodeId|String|否|d-bpxxxxxxxx|分片集群实例中Mongos节点ID或Shard节点ID。

 **说明：** 如不传入则返回所有Mongos节点和Shard节点的审计日志。

 |
|PageSize|Integer|否|30|每页记录数，取值： **30、50、100**，默认值为**30**。

 |
|PageNumber|Integer|否|1|页码，取值为大于0且不超过Integer数据类型的的最大值，默认值为**1**。

 |
|RegionId|String|否|cn-hangzhou|实例所属的地域ID，您可以通过调用[DescribeDBInstanceAttribute](~~62010~~)进行查询。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Items| | |审计文件信息列表。

 |
|└FileID|Integer|406505|文件ID。

 |
|└LogDownloadURL|String|http://xxxxxxxx.oss-cn-hangzhou.aliyuncs.com/custinsxxxxxx/custinsxxxxxx\_xxxxxx.csv|审计日志文件的下载链接。

 **说明：** 若当前不可下载，则为空串。

 |
|└LogEndTime|String|2019-03-12T09:23:15Z|审计日志结束时间，格式为*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。

 |
|└LogSize|Long|98|审计日志文件的大小，单位为Byte。

 |
|└LogStartTime|String|2019-03-11T08:19:29Z|审计日志起始时间，格式为*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。

 |
|└LogStatus|String|Success|审计日志文件状态。

 -   **Success**：归档完成。
-   **Failed**：归档失败。
-   **Generating**：归档中。
-   **Initializing**：未开始。

 |
|PageNumber|Integer|1|页码。

 |
|PageRecordCount|Integer|1|当前页记录数。

 |
|RequestId|String|F8CA8312-530A-413A-9129-F2BB32A8D404|请求ID。

 |
|TotalRecordCount|Integer|1|总记录数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeAuditFiles
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidDBInstanceClass.NotFound|Specified DB instance class is not found.|该实例规格不存在，请您检查输入的参数是否正确。|
|403|IncorrectDBInstanceType|Current DB instance type does not support this operation.|当前的实例类型不支持此操作。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

