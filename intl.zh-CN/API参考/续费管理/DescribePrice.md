# DescribePrice

调用DescribePrice查询创建MongoDB实例、升级配置或续费操作产生的费用。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribePrice&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribePrice|系统规定参数，取值：**DescribePrice**。 |
|DBInstances|String|是|\[ \{ "DBInstanceId":"dds-bp1xxxxxxxxxxxxx", "RegionId":"cn-hangzhou", "ZoneId":"cn-hangzhou-f", "Engine":"MongoDB", "EngineVersion":" 4.2", "DBInstanceClass":"dds.mongo.mid", "DBInstanceStorage":10, "ChargeType":"PrePaid", "Period":1 \} \]|包含实例中多个信息的JSON格式字符串。参数说明详情请参见[DescribePrice接口DBInstances参数说明](~~197291~~)。 |
|OrderType|String|是|BUY|订单类型。取值：

 -   BUY：创建实例
-   UPGRADE：变更配置
-   RENEW：续费实例 |
|RegionId|String|否|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~61933~~)查看MongoDB实例可用的地域和可用区。 |
|CommodityCode|String|否|dds\_sharding|集群代码。取值：

 -   dds：副本集版按量付费
-   badds: 副本集版包年包月
-   dds\_sharding: 分片集群版按量付费
-   badds\_sharding： 分片集群版包年包月
-   badds\_sharding\_intl： 分片集群版包年包月（国际站）
-   badds\_sharding\_jp： 分片集群版包年包月（日本站） |
|ProductCode|String|否|dds|产品代码。默认为：**dds**。 |
|BusinessInfo|String|否|\{"AccountPassword":"Pw123456","DBInstanceDescription":"test"\}|附加参数，业务信息。 |
|CouponNo|String|否|youhuiquan\_promotion\_option\_id\_for\_blank|优惠码，默认为：**youhuiquan\_promotion\_option\_id\_for\_blank**。 |
|OrderParamOut|String|否|false|是否返回订单参数。取值：

 -   false：不返回
-   true：返回

 默认为：**false**。 |
|ResourceGroupId|String|否|sg-bpxxxxxxxxxxxxxxxxxx|资源组ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Order|Struct| |订单信息列表。 |
|Coupons|Array of Coupon| |优惠券信息列表。 |
|Coupon| | | |
|CouponNo|String|youhuiquan\_promotion\_option\_id\_for\_blank|优惠券编码。 |
|Description|String|备注示例。|备注。 |
|IsSelected|String|true|是否选中该优惠券。 |
|Name|String|youhuiquan111|优惠券名称。 |
|Currency|String|CNY|币种。 |
|DiscountAmount|String|322.4|订单优惠金额。 |
|OriginalAmount|String|322.4|订单原价。 |
|RuleIds|List|\{"RuleId": \[11111111,11111111,11111111\]\}|活动规则ID合集。 |
|TradeAmount|String|0|订单实际交易价。 |
|OrderParams|String|\{\\"autoPay\\":false\}"|订单参数。输入参数`OrderParamOut`为`true`时返回。 |
|RequestId|String|82530058-D4CF-49A4-96FB-9DD2DF3CE93E|请求ID。 |
|Rules|Array of Rule| |活动规则列表。 |
|Rule| | | |
|Name|String|demoname|规则名称。 |
|RuleDescId|Long|11111111|策略ID。 |
|Title|String|demo|规则标题。 |
|SubOrders|Array of SubOrder| |优惠券对应的规则列表。 |
|SubOrder| | | |
|DiscountAmount|String|322.4|订单优惠金额。 |
|InstanceId|String|dds-bpxxxxxxxx|实例ID。 |
|OriginalAmount|String|322.4|订单原价。 |
|RuleIds|List|\{"RuleId": \[11111111,11111111,11111111\]\}|活动规则ID合集。 |
|TradeAmount|String|0|订单实际交易价格。 |
|TraceId|String|11111111111111111111111111111111|调用链ID。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=DescribePrice
&DBInstances=
[         
    {                 "DBInstanceId":"dds-bp1xxxxxxxxxxxxx",
                      "RegionId":"cn-hangzhou",
                      "ZoneId":"cn-hangzhou-f", 
                      "Engine":"MongoDB",
                      "EngineVersion":" 4.2", 
                      "DBInstanceClass":"dds.mongo.mid",
                      "DBInstanceStorage":10, 
                      "VpcId":null, 
                      "VSwitchId":null, 
                      "ChargeType":"PrePaid",
                      "Period":1          
   }        
]
&OrderType=BUY
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<Order>
    <Currency>CNY</Currency>
    <RuleIds>
        <RuleId>102xxxxxxxxxxxxx</RuleId>
    </RuleIds>
    <TradeAmount>0</TradeAmount>
    <OriginalAmount>4.62</OriginalAmount>
    <Coupons>
    </Coupons>
    <DiscountAmount>4.62</DiscountAmount>
</Order>
<RequestId>82530058-D4CF-49A4-96FB-9DD2DF3CE93E</RequestId>
<SubOrders>
</SubOrders>
<OrderParams>{"autoPay":false,"autoUseCoupon":false,"bid":"26842","buyerId":140xxxxxxxxxxxxx,"commodities":[{"chargeType":"PREPAY","commodityCode":"badds","components":[{"componentCode":"dds_region","free":false,"moduleAttrStatus":3,"moduleParams":{},"properties":[{"code":"dds_region","name":"华东1（杭州）","value":"cn-hangzhou"}]},{"componentCode":"dds_dbtype","free":false,"moduleAttrStatus":3,"moduleParams":{},"properties":[{"code":"dds_dbtype","name":"MongoDB","value":"MongoDB"}]},{"componentCode":"dds_dbversion","free":false,"moduleAttrStatus":3,"moduleParams":{},"properties":[{"code":"dds_dbversion","name":" 4.2","value":" 4.2"}]},{"componentCode":"dds_class","free":false,"moduleAttrStatus":3,"moduleParams":{},"properties":[{"code":"dds_class","name":"dds.mongo.mid","value":"dds.mongo.mid"}]},{"componentCode":"dds_storage","free":false,"moduleAttrStatus":3,"moduleParams":{},"properties":[{"code":"dds_storage","name":"10","value":"10"}]},{"componentCode":"replication_factor","free":false,"moduleAttrStatus":3,"moduleParams":{},"properties":[{"code":"replication_factor","name":"5","value":"5"}]},{"componentCode":"readonly_replicas","free":false,"moduleAttrStatus":3,"moduleParams":{},"properties":[{"code":"readonly_replicas","name":"0","value":"0"}]}],"duration":1,"free":false,"instanceId":"dds-bp1xxxxxxxxxxxxx","migrateOrder":false,"orderParams":{},"orderType":"UPGRADE","periodAlign":false,"prePayPostCharge":false,"pricingCycle":"Day","quantity":1,"renewChange":false,"specUpdate":false,"syncToSubscription":false,"upgradeInquireFinancialValue":true}],"fromApp":"OpenApi","orderParams":{"promotion_input_param":"{\"promotionFilter\":{\"youhui_quan\":true},\"promotionOptionCode\":\"youhui_quan\",\"promotionOptionNo\":\"youhuiquan_promotion_option_id_for_blank\"}"},"rateWithTax":false,"requestId":"82530058-D4CF-49A4-96FB-9DD2DF3CE93E","token":"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx","userId":140xxxxxxxxxxxxx}</OrderParams>
<Rules>
    <Rule>
        <RuleDescId>102xxxxxxxxxxxxx</RuleDescId>
        <Name>优惠券示例</Name>
    </Rule>
</Rules>
```

`JSON` 格式

```
{
	"Order": {
		"Currency": "CNY",
		"RuleIds": {
			"RuleId": [
				"102xxxxxxxxxxxxx"
			]
		},
		"TradeAmount": 0,
		"OriginalAmount": 4.62,
		"Coupons": {
			"Coupon": []
		},
		"DiscountAmount": 4.62
	},
	"RequestId": "82530058-D4CF-49A4-96FB-9DD2DF3CE93E",
	"SubOrders": {
		"SubOrder": []
	},
	"OrderParams": "{\"autoPay\":false,\"autoUseCoupon\":false,\"bid\":\"26842\",\"buyerId\":140xxxxxxxxxxxxx,\"commodities\":[{\"chargeType\":\"PREPAY\",\"commodityCode\":\"badds\",\"components\":[{\"componentCode\":\"dds_region\",\"free\":false,\"moduleAttrStatus\":3,\"moduleParams\":{},\"properties\":[{\"code\":\"dds_region\",\"name\":\"华东1（杭州）\",\"value\":\"cn-hangzhou\"}]},{\"componentCode\":\"dds_dbtype\",\"free\":false,\"moduleAttrStatus\":3,\"moduleParams\":{},\"properties\":[{\"code\":\"dds_dbtype\",\"name\":\"MongoDB\",\"value\":\"MongoDB\"}]},{\"componentCode\":\"dds_dbversion\",\"free\":false,\"moduleAttrStatus\":3,\"moduleParams\":{},\"properties\":[{\"code\":\"dds_dbversion\",\"name\":\" 4.2\",\"value\":\" 4.2\"}]},{\"componentCode\":\"dds_class\",\"free\":false,\"moduleAttrStatus\":3,\"moduleParams\":{},\"properties\":[{\"code\":\"dds_class\",\"name\":\"dds.mongo.mid\",\"value\":\"dds.mongo.mid\"}]},{\"componentCode\":\"dds_storage\",\"free\":false,\"moduleAttrStatus\":3,\"moduleParams\":{},\"properties\":[{\"code\":\"dds_storage\",\"name\":\"10\",\"value\":\"10\"}]},{\"componentCode\":\"replication_factor\",\"free\":false,\"moduleAttrStatus\":3,\"moduleParams\":{},\"properties\":[{\"code\":\"replication_factor\",\"name\":\"5\",\"value\":\"5\"}]},{\"componentCode\":\"readonly_replicas\",\"free\":false,\"moduleAttrStatus\":3,\"moduleParams\":{},\"properties\":[{\"code\":\"readonly_replicas\",\"name\":\"0\",\"value\":\"0\"}]}],\"duration\":1,\"free\":false,\"instanceId\":\"dds-bp1xxxxxxxxxxxxx\",\"migrateOrder\":false,\"orderParams\":{},\"orderType\":\"UPGRADE\",\"periodAlign\":false,\"prePayPostCharge\":false,\"pricingCycle\":\"Day\",\"quantity\":1,\"renewChange\":false,\"specUpdate\":false,\"syncToSubscription\":false,\"upgradeInquireFinancialValue\":true}],\"fromApp\":\"OpenApi\",\"orderParams\":{\"promotion_input_param\":\"{\\\"promotionFilter\\\":{\\\"youhui_quan\\\":true},\\\"promotionOptionCode\\\":\\\"youhui_quan\\\",\\\"promotionOptionNo\\\":\\\"youhuiquan_promotion_option_id_for_blank\\\"}\"},\"rateWithTax\":false,\"requestId\":\"82530058-D4CF-49A4-96FB-9DD2DF3CE93E\",\"token\":\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\",\"userId\":140xxxxxxxxxxxxx}",
	"Rules": {
		"Rule": [
			{
				"RuleDescId": "102xxxxxxxxxxxxx",
				"Name": "优惠券示例"
			}
		]
	}
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

