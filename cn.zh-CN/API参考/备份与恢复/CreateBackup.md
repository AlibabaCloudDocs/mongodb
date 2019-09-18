# CreateBackup {#doc_api_Dds_CreateBackup .reference}

调用CreateBackup接口手动备份MongoDB实例。

调用该接口时，要求实例状态为运行中。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=CreateBackup&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DBInstanceId|String|是|d-bpxxxxxxxx|实例ID。

 |
|Action|String|否|CreateBackup|要执行的操作，取值： **CreateBackup**。

 |
|BackupMethod|String|否|Logical|实例的备份方式，取值：

 -   **Logical**：逻辑备份。
-   **Physical**：物理备份，默认为物理备份。

 **说明：** 仅副本集和分片集群实例支持选择备份方式。单节点实例无需传入本参数，固定为快照备份。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|BackupId|String|5664xxxx|备份ID。

 |
|RequestId|String|7016B12F-7F64-40A4-BAFF-013F02AC82FC|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=CreateBackup
DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateBackupResponse>
	  <RequestId>7016B12F-7F64-40A4-BAFF-013F02AC82FC</RequestId>
	  <BackupId>5664xxxx</BackupId>
</CreateBackupResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"7016B12F-7F64-40A4-BAFF-013F02AC82FC",
	"BackupId":"5664xxxx"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

