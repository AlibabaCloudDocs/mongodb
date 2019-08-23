# ModifyNodeSpec {#doc_api_Dds_ModifyNodeSpec .reference}

调用ModifyNodeSpec接口变更MongoDB分片集群实例中节点的规格和存储空间。

 **请确保在使用该接口前，已充分了解云数据库MongoDB产品的收费方式和[价格](https://www.aliyun.com/price/product#/mongodb/detail)。** 

该接口仅适用于分片集群实例。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=ModifyNodeSpec&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|NodeId|String|是|d-bpxxxxxxxx|分片集群实例中Shard节点ID或Mongos节点ID，您可以通过调用[DescribeDBInstanceAttribute](~~61923~~)接口进行查询。

 **说明：** 当传入的值为Shard节点ID时，还需要传入**NodeStorage**参数。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|Action|String|否|ModifyNodeSpec|要执行的操作，取值：**ModifyNodeSpec**。

 |
|NodeClass|String|否|dds.shard.standard|Shard节点或Mongos节点的规格，规格详情请参考[实例规格表](~~57141~~)。

 **说明：** 本参数和**NodeStorage**参数两者必须传入一个。

 |
|NodeStorage|Integer|否|20|设置Shard节点的存储空间。

 -   取值范围：**10**~**2000**，单位为GB。
-   每10GB进行递增。

 **说明：** 

-   本参数和**NodeClass**参数两者必须传入一个。
-   当**NodeId**传入的值为Shard节点ID时，本参数才可用。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|AutoPay|Boolean|否|true|是否自动付费。取值：

 -   **true**：自动付费，请确保账号有足够的余额。
-   **false**：控制台手动付费。具体操作为：登录控制台，在右上角选择**费用**\>进入**费用中心**，在**订单管理**找到目标订单进行支付。

 默认值为：**true**。

 |
|EffectiveTime|String|否|Immediately|变更配置的生效时间，取值：

 -   **Immediately**：立即生效。
-   **MaintainTime**：实例可运维时间段内生效。

 默认值为**Immediately**。

 |
|FromApp|String|否|OpenApi|请求来源，取值：

 -   **OpenApi**：请求来源为OpenApi。
-   **mongo\_buy**：请求来源为控制台。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|OrderId|String|2033xxxxxxxxx|订单ID。

 |
|RequestId|String|EFFC5788-8BB5-41B5-9F15-9CFC5A0E8FCC|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=ModifyNodeSpec
&NodeId=d-bpxxxxxxxx
&DBInstanceId=dds-bpxxxxxxxx
&NodeClass=dds.shard.standard
&NodeStorage=20
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyNodeSpecResponse>
	  <OrderId>2033xxxxxxxxx</OrderId>
	  <RequestId>EFFC5788-8BB5-41B5-9F15-9CFC5A0E8FCC</RequestId>
</ModifyNodeSpecResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"EFFC5788-8BB5-41B5-9F15-9CFC5A0E8FCC",
	"OrderId":"2033xxxxxxxx"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

