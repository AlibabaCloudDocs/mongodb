# ModifyDBInstanceSpec {#doc_api_Dds_ModifyDBInstanceSpec .reference}

调用ModifyDBInstanceSpec接口变更MongoDB单节点或副本集实例的规格或存储空间。

 **请确保在使用该接口前，已充分了解云数据库MongoDB产品的收费方式和[价格](https://www.alibabacloud.com/zh/product/apsaradb-for-mongodb/pricing)。** 

该接口仅适用于单节点实例和副本集实例。分片集群实例如需变更配置，您可以根据需求通过调用[ModifyNodeSpec](~~61923~~)、[CreateNode](~~61911~~)或[DeleteNode](~~61922~~)接口来实现。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceSpec)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDBInstanceSpec|系统规定参数，取值：**ModifyDBInstanceSpec**。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|DBInstanceClass|String|否|dds.mongo.standard|实例规格，详情请参考[实例规格表](~~57141~~)。

 **说明：** 本参数和**DBInstanceStorage**参数两者中必须传入一项。

 |
|DBInstanceStorage|String|否|50|实例的存储空间。

 -   取值范围：10~3000，单位为GB，具体取值受实例规格约束，详情请参考[实例规格表](~~57141~~)。
-   每10GB递增。

 **说明：** 

-   本参数和**DBInstanceClass**参数两者中必须传入一项。
-   仅按量付费的副本集实例支持降配存储空间，且存储空间必须大于当前已使用的存储空间。

 |
|OrderType|String|否|UPGRADE|变配类型，取值：

 -   UPGRADE：升级配置。
-   DOWNGRADE：降级配置，默认为降级配置。

 **说明：** 当实例付费方式为包年包月时，本参数才可用。

 |
|AutoPay|Boolean|否|true|是否自动付费。取值：

 -   **true**：自动付费，请确保账号有足够的余额。
-   **false**：控制台手动付费。具体操作为：登录控制台，在页面右上角选择**费用**\>**进入费用中心**，在**订单管理**找到目标订单进行支付。

 默认值为：**true**。

 |
|BusinessInfo|String|否|\{“ActivityId":"000000000"\}|业务信息。

 |
|ReplicationFactor|String|否|3|设置实例的节点个数。

 -   副本集实例取值为**3，5，7**。
-   单节点实例取值固定为**1**。

 |
|CouponNo|String|否|youhuiquan\_promotion\_option\_id\_for\_blank|优惠码，默认为：**youhuiquan\_promotion\_option\_id\_for\_blank**。

 |
|EffectiveTime|String|否|Immediately|变更配置的生效时间，取值：

 -   **Immediately**：立即生效。
-   **MaintainTime**：在实例的可运维时间段内生效。

 默认为**Immediately**。

 |
|RegionId|String|否|cn-hangzhou|实例所属的地域ID，您可以通过调用[DescribeDBInstanceAttribute](~~62010~~)进行查询。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|OrderId|String|2033xxxxxxxx|订单ID。

 |
|RequestId|String|C5662998-62BE-4C7F-961D-7DFE775DD813|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=ModifyDBInstanceSpec
&DBInstanceId=dds-bpxxxxxxxx
&DBInstanceStorage=50
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceSpecResponse>
  <OrderId>2033xxxxxxxx</OrderId>
  <RequestId>C5662998-62BE-4C7F-961D-7DFE775DD813</RequestId>
</ModifyDBInstanceSpecResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"C5662998-62BE-4C7F-961D-7DFE775DD813",
	"OrderId":"2033xxxxxxxx"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

