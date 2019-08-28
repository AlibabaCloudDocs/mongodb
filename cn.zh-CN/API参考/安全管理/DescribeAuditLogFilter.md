# DescribeAuditLogFilter {#doc_api_Dds_DescribeAuditLogFilter .reference}

调用DescribeAuditLogFilter接口查询MongoDB实例审计日志采集的日志类型。

调用本接口时，要求实例状态为运行中。

**说明：** 本接口仅适用于副本集实例，暂不支持单节点实例和分片集群实例。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeAuditLogFilter&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|Action|String|否|DescribeAuditLogFilter|要执行的操作，取值： **DescribeAuditLogFilter**。

 |
|RoleType|String|否|primary|实例中节点的角色，取值：

 -   **primary**：主节点。
-   **secondary**：从节点。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Filter|String|admin,slow,insert,query,update,delete,command|数据库操作日志类型，有以下几种类型：

 -   **admin**：运维管控操作。
-   **slow**：慢日志。
-   **query**：查询操作。
-   **insert**：插入操作。
-   **update**：更新操作。
-   **delete**：删除操作。
-   **command**：协议命令。例如aggregate聚合方法。

 |
|RequestId|String|D7C8BA0C-9350-487D-9B70-D69AF27FB1EB|请求ID。

 |
|RoleType|String|primary|节点角色。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeAuditLogFilter
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeAuditLogFilterResponse>
	  <Filter>admin,slow,insert,query,update,delete,command</Filter>
	  <RoleType></RoleType>
	  <RequestId>D7C8BA0C-9350-487D-9B70-D69AF27FB1EB</RequestId>
</DescribeAuditLogFilterResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Filter":"admin,slow,insert,query,update,delete,command",
	"RequestId":"D7C8BA0C-9350-487D-9B70-D69AF27FB1EB",
	"RoleType":""
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

