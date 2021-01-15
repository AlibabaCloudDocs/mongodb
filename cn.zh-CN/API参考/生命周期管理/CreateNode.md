# CreateNode

调用CreateNode接口为MongoDB分片集群实例增加Shard节点或Mongos节点。

请确保在使用该接口前，已充分了解MongoDB产品的收费方式和[价格](https://www.aliyun.com/price/product#/mongodb/detail)。

该接口仅适用于分片集群实例。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=CreateNode&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateNode|要执行的操作，取值：**CreateNode**。 |
|NodeClass|String|是|dds.shard.mid|Shard节点或Mongos节点的规格，规格详情请参见[实例规格表](~~57141~~)。 |
|NodeType|String|是|shard|Node的类型，取值：

 -   **shard**：Shrad节点。
-   **mongos**：Mongos节点。 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|分片集群实例ID。 |
|NodeStorage|Integer|否|10|Node的磁盘空间，当**NodeType**参数取值为**Shard**时该参数可用，且该参数必须传入。

 -   取值范围：**10**~**2000**，单位为GB。
-   每10GB进行递增。 |
|FromApp|String|否|OpenApi|请求来源，取值：

 -   **OpenApi**：请求来源为OpenApi。
-   **mongo\_buy**：请求来源为控制台。 |
|AutoPay|Boolean|否|true|是否自动付费。取值：

 -   **true**：自动付费，请确保账号有足够的余额。
-   **false**：控制台手动付费。具体操作为：登录控制台，在右上角选择**费用**\>**进入费用中心**，在**订单管理**页面找到目标订单进行支付。

 默认值为：**true**。

 **说明：** 仅包年包月的实例可传入该参数。 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。 |
|RegionId|String|否|cn-hangzhou|地域ID，您可以调用[DescribeRegions](~~61933~~)查询。 |
|ReadonlyReplicas|Integer|否|5|设置Shard节点中只读节点的个数。取值范围：**0**~**5**。默认值：**0**。

 **说明：** 当前仅中国站支持本参数。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|NodeId|String|d-bpxxxxxxxxxxxxxx|节点ID。 |
|OrderId|String|2034xxxxxxxx|订单ID。 |
|RequestId|String|7D48FB19-20CA-4725-A870-3D8F5CE69F14|请求ID。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=CreateNode
&NodeClass=dds.shard.mid
&NodeType=shard
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateNodeResponse>
	  <OrderId>2034xxxxxxxx</OrderId>
	  <RequestId>7D48FB19-20CA-4725-A870-3D8F5CE69F14</RequestId>
</CreateNodeResponse>
```

`JSON` 格式

```
{"RequestId":"7D48FB19-20CA-4725-A870-3D8F5CE69F14",
	"NodeId":"d-bpxxxxxxxxxxxxxx",
	"OrderId":"2034xxxxxxxx"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

