# CreateNode {#doc_api_Dds_CreateNode .reference}

调用CreateNode接口为MongoDB分片集群实例增加Shard节点或Mongos节点。

 **请确保在使用该接口前，已充分了解云数据库MongoDB产品的收费方式和[价格](https://www.alibabacloud.com/zh/product/apsaradb-for-mongodb/pricing)。** 

该接口仅适用于分片集群实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=CreateNode)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateNode|要执行的操作，取值：**CreateNode**。

 |
|NodeClass|String|是|dds.shard.mid|Shard节点或Mongos节点的规格，规格详情请参见[实例规格表](~~57141~~)。

 |
|NodeType|String|是|shard|Node的类型，取值：

 -   **shard**：Shrad节点。
-   **mongos**：Mongos节点。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|分片集群实例ID。

 |
|NodeStorage|Integer|否|10|Node的磁盘空间，当**NodeType**参数取值为**Shard**时该参数可用，且该参数必须传入。

 -   取值范围：**10**~**2000**，单位为GB。
-   每10GB进行递增。

 |
|AutoPay|Boolean|否|true|是否自动付费。取值：

 -   **true**：自动付费，请确保账号有足够的余额。
-   **false**：控制台手动付费。具体操作为：登录控制台，在右上角选择**费用**\>**进入费用中心**，在**订单管理**页面找到目标订单进行支付。

 默认值为：**true**。

 **说明：** 仅包年包月的实例可传入该参数。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|OrderId|String|2034xxxxxxxx|订单ID。

 |
|RequestId|String|7D48FB19-20CA-4725-A870-3D8F5CE69F14|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=CreateNode
&NodeClass=dds.shard.mid
&NodeType=shard
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateNodeResponse>
  <OrderId>2034xxxxxxxx</OrderId>
  <RequestId>7D48FB19-20CA-4725-A870-3D8F5CE69F14</RequestId>
</CreateNodeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"7D48FB19-20CA-4725-A870-3D8F5CE69F14",
	"OrderId":"2034xxxxxxxx"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

