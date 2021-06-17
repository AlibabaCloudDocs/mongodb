# CreateNode

调用CreateNode接口为MongoDB分片集群实例增加Shard节点或Mongos节点。

请确保在使用该接口前，已充分了解MongoDB产品的收费方式和[价格](https://www.alibabacloud.com/zh/product/apsaradb-for-mongodb/pricing)。

该接口仅适用于分片集群实例。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=CreateNode&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateNode|系统规定参数。取值：**CreateNode**。 |
|RegionId|String|否|cn-hangzhou|地域ID，您可以调用[DescribeRegions](~~61933~~)查询。 |
|DBInstanceId|String|是|dds-bp11501cd7b5\*\*\*\*|分片集群实例ID。 |
|NodeClass|String|是|dds.shard.mid|Shard节点或Mongos节点的规格，规格详情请参见[实例规格表](~~57141~~)。 |
|NodeStorage|Integer|否|10|Node的磁盘空间，取值范围为10~2000 GB，步长为10 GB。

 **说明：** 当节点类型为**Shard**时，需要配置该参数。 |
|NodeType|String|是|shard|节点类型，取值如下：

 -   **shard**：Shrad节点。
-   **mongos**：Mongos节点。 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCz\*\*\*\*|用于保证请求的幂等性。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。 |
|FromApp|String|否|mongo\_buy|请求来源，取值如下：

 -   **OpenApi**：请求来源为OpenAPI。
-   **mongo\_buy**：请求来源为控制台。 |
|AutoPay|Boolean|否|true|是否自动付费。取值如下：

 -   **true**：自动付费，请确保账号有足够的余额。
-   **false**：控制台手动付费。您可以单击控制台右上角的**费用**，进入**费用中心**页面，选择**订单管理** \> **我的订单**，在**订单列表**页面找到目标订单进行支付。

 默认值为：**true**。

 **说明：** 当付费类型为包年包月时，需要配置该参数。 |
|ReadonlyReplicas|Integer|否|5|设置Shard节点中只读节点的个数。取值范围为0~5。默认为0。

 **说明：** 当前仅中国站支持本参数。 |
|BusinessInfo|String|否|\{“ActivityId":"000000000"\}|附加参数，业务信息。 |
|CouponNo|String|否|youhuiquan\_promotion\_option\_id\_for\_blank|优惠码，默认为：**youhuiquan\_promotion\_option\_id\_for\_blank**。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|7D48FB19-20CA-4725-A870-3D8F5CE6\*\*\*\*|请求ID。 |
|NodeId|String|d-bp1b234bf7a4\*\*\*\*|节点ID。 |
|OrderId|String|20951063702\*\*\*\*|订单ID。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=CreateNode
&DBInstanceId=dds-bp11501cd7b5****
&NodeClass=dds.shard.mid
&NodeStorage=10
&NodeType=shard
&ClientToken=ETnLKlblzczshOTUbOCz****
&FromApp=mongo_buy
&AutoPay=true
&ReadonlyReplicas=5
&BusinessInfo={“ActivityId":"000000000"}
&CouponNo=youhuiquan_promotion_option_id_for_blank
&公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<CreateNodeResponse>
    <RequestId>7D48FB19-20CA-4725-A870-3D8F5CE6****</RequestId>
    <NodeId>d-bp1b234bf7a4****</NodeId>
    <OrderId>20951063702****</OrderId>
</CreateNodeResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "7D48FB19-20CA-4725-A870-3D8F5CE6****",
  "NodeId" : "d-bp1b234bf7a4****",
  "OrderId" : "20951063702****"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

