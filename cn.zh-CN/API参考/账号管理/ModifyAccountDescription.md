# ModifyAccountDescription {#doc_api_Dds_ModifyAccountDescription .reference}

调用ModifyAccountDescription接口修改MongoDB实例中root账号的备注信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=ModifyAccountDescription&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AccountName|String|是|root|待修改备注信息的账号名。

 |
|AccountDescription|String|是|superadmin|设置账号的备注信息。

 -   不能以http:// 或者 https:// 开头。
-   以中文、英文字母开头。
-   可以包含中文、英文字符、下划线（\_）、连接号（-）和数字，长度为2~256个字符。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|Action|String|否|ModifyAccountDescription|要执行的操作，取值：**ModifyAccountDescription**。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|59DE9FC2-7B40-45CF-9011-7327A8A771A2|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=ModifyAccountDescription
&AccountName=root
&AccountDescription=superadmin
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RestoreDBInstanceResponse>
	  <RequestId>59DE9FC2-7B40-45CF-9011-7327A8A771A2</RequestId>
</RestoreDBInstanceResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"59DE9FC2-7B40-45CF-9011-7327A8A771A2"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

