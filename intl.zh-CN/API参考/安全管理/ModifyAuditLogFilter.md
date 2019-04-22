# ModifyAuditLogFilter {#doc_api_Dds_ModifyAuditLogFilter .reference}

调用ModifyAuditLogFilter接口修改MongoDB实例审计日志的采集类型。

调用本接口时，要求实例状态为运行中。

本接口仅适用于副本集实例，暂不支持单节点实例和分片集群实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=ModifyAuditLogFilter)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyAuditLogFilter|要执行的操作，取值： **ModifyAuditLogFilter**。

 |
|Filter|String|是|insert,query,update,delete|设置审计日志的采集类型。

 -   **admin**：运维管控操作。
-   **slow**：慢日志。
-   **query**：查询操作。
-   **insert**：插入操作。
-   **update**：更新操作。
-   **delete**：删除操作。
-   **command**：协议命令。例如aggregate聚合方法。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|RoleType|String|否|primary|实例中节点的角色，取值：

 -   **primary**：主节点。
-   **secondary**：从节点。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|E209BE2B-F264-4B9D-81F6-A5A5FB1FBF28|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=ModifyAuditLogFilter
&Filter=insert,query,update,delete
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyAuditLogFilterResponse>
  <RequestId>E209BE2B-F264-4B9D-81F6-A5A5FB1FBF28</RequestId>
</ModifyAuditLogFilterResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"E209BE2B-F264-4B9D-81F6-A5A5FB1FBF28"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

