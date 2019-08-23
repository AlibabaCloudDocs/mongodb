# ResetAccountPassword {#doc_api_Dds_ResetAccountPassword .reference}

调用ResetAccountPassword接口重置MongoDB实例中root账号的密码。

**说明：** 本接口目前仅支持重置实例中root账号的密码。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=ResetAccountPassword&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AccountName|String|是|root|需要重置密码的账号，取值：**root**。

 |
|AccountPassword|String|是|Ali!123456|重置后的密码，即修改后的密码。

 -   密码由大写字母、小写字母、数字、特殊字符中的任意三种组成，特殊字符为!\#$%^&\*\(\)\_+-=
-   密码长度为8-32位

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|Action|String|否|ResetAccountPassword|要执行的操作，取值：**ResetAccountPassword**。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|06CBD06E-ABC9-4121-AB93-3C3820B3E7E6|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=ResetAccountPassword
&AccountName=root
&AccountPassword=Ali!123456
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ResetAccountPasswordResponse>
	  <RequestId>06CBD06E-ABC9-4121-AB93-3C3820B3E7E6</RequestId>
</ResetAccountPasswordResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"06CBD06E-ABC9-4121-AB93-3C3820B3E7E6"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

