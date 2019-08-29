# ModifyAuditPolicy {#doc_api_Dds_ModifyAuditPolicy .reference}

调用ModifyAuditPolicy接口设置MongoDB实例的审计日志开关或日志存储时长。

本接口适用于副本集实例和分片集群实例。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=ModifyAuditPolicy&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AuditStatus|String|是|enable|审计日志状态，取值：

 -   **enable**：开启审计日志。
-   **disabled**：关闭审计日志。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|Action|String|否|ModifyAuditPolicy|要执行的操作，取值：**ModifyAuditPolicy**。

 |
|StoragePeriod|Integer|否|30|审计日志存储的天数。取值范围为**1**~**30**，默认为**30**。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|DC04D812-F18D-4568-9B88-F260D9590116|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=ModifyAuditPolicy
&AuditStatus=enable
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyAuditPolicyResponse>
	  <RequestId>DC04D812-F18D-4568-9B88-F260D9590116</RequestId>
</ModifyAuditPolicyResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"DC04D812-F18D-4568-9B88-F260D9590116"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

