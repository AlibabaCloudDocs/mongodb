# ModifySecurityIps {#doc_api_Dds_ModifySecurityIps .reference}

调用ModifySecurityIps接口修改MongoDB实例的IP白名单。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=ModifySecurityIps&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|SecurityIps|String|是|10.23.12.24/24,10.22.22.22|IP白名单分组下的IP列表，多个IP地址请以英文逗号（,）隔开，不可重复，最多1000个。支持如下两种格式：

 -   IP地址形式，例如：10.23.12.24。
-   CIDR形式，例如：10.23.12.24/24（无类域间路由，24表示了地址中前缀的长度，范围为1~32）。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|Action|String|否|ModifySecurityIps|要执行的操作，取值：**ModifySecurityIps**。

 |
|ModifyMode|String|否|Append|修改方式，取值：

 -   **Cover**：覆盖原白名单。
-   **Append**：追加白名单。
-   **Delete**：删除该白名单。

 默认取值为**Cover**。

 |
|SecurityIpGroupName|String|否|allowserver|进行修改的IP白名单所属分组名称，默认为**default**分组。

 |
|SecurityIpGroupAttribute|String|否|test|白名单分组属性。支持大写字母、小写字母、数字，长度最大为120个字符。

 默认为空字符串。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|61B05CCF-EBAB-4BF3-BA67-D77256A721E2|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=ModifySecurityIps
&SecurityIps=10.23.12.24/24,10.22.22.22
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifySecurityIpsResponse>
	  <RequestId>61B05CCF-EBAB-4BF3-BA67-D77256A721E2</RequestId>
</ModifySecurityIpsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"61B05CCF-EBAB-4BF3-BA67-D77256A721E2"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

