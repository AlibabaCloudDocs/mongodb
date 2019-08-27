# RenewDBInstance {#doc_api_Dds_RenewDBInstance .reference}

调用RenewDBInstance接口手动续费包年包月实例。

 **请确保在使用该接口前，已充分了解云数据库MongoDB产品的收费方式和[价格](https://www.aliyun.com/price/product#/mongodb/detail)。** 

该接口仅适用于付费类型为包年包月的实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=RenewDBInstance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RenewDBInstance|要执行的操作，取值：**RenewDBInstance**。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|Period|Integer|是|1|实例续费时长，单位为月。取值：**1~9，12，24，36**。

 |
|CouponNo|String|否|1111111111111111|优惠码，默认为：**youhuiquan\_promotion\_option\_id\_for\_blank**。

 |
|AutoPay|Boolean|否|true|是否自动付费。取值：

 -   **true**：自动付费，请确保账号有足够的余额。
-   **false**：控制台手动付费。具体操作为：登录控制台，在页面右上角选择**费用**\>**进入费用中心**，在**订单管理**找到目标订单进行支付。

 默认值为：**true**。

 |
|BusinessInfo|String|否|\{“ActivityId":"000000000"\}|业务信息。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|OrderId|String|203317xxxxxxxx|生成的订单ID。

 |
|RequestId|String|B118EF45-9633-4EE3-8405-42ED4373721B|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=RenewDBInstance
&DBInstanceId=dds-bpxxxxxxxx
&Period=1
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RenewDBInstanceResponse>
  <OrderId>2033xxxxxxxx</OrderId>
  <RequestId>B118EF45-9633-4EE3-8405-42ED4373721B</RequestId>
</RenewDBInstanceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"B118EF45-9633-4EE3-8405-42ED4373721B",
	"OrderId":"2033xxxxxxxx"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

