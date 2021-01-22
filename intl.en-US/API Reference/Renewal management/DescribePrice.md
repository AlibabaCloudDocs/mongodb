# DescribePrice

You can call this operation to query the fees incurred when you create, upgrade, or renew an ApsaraDB for MongoDB instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribePrice&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribePrice|The operation that you want to perform. Set the value to **DescribePrice**. |
|DBInstances|String|Yes|\[ \{ "DBInstanceId":"dds-bp1xxxxxxxxxxxxx", "RegionId":"cn-hangzhou", "ZoneId":"cn-hangzhou-f", "Engine":"MongoDB", "EngineVersion":" 4.2", "DBInstanceClass":"dds.mongo.mid", "DBInstanceStorage":10, "ChargeType":"PrePaid", "Period":1 \} \]|A JSON string that contains the details of the ApsaraDB for MongoDB instance. For more information, see [Details of the DBInstances parameter in the DescribePrice operation](~~197291~~). |
|OrderType|String|Yes|BUY|The type of the order. Valid values:

-   BUY: instance creation
-   UPGRADE: instance configuration modification
-   RENEW: instance renewal |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query available regions and zones in which the ApsaraDB for MongoDB instance can be created. |
|CommodityCode|String|No|dds\_sharding|The code of the cluster. Valid values:

-   dds: a replica set instance that uses the pay-as-you-go billing method
-   badds: a replica set instance that uses the subscription billing method
-   dds\_sharding: a sharded cluster instance that uses the pay-as-you-go billing method
-   badds\_sharding: a sharded cluster instance that uses the subscription billing method
-   badds\_sharding\_intl: a sharded cluster instance that uses the subscription billing method and is available on the International site \(alibabacloud.com\)
-   badds\_sharding\_jp: a sharded cluster instance that uses the subscription billing method and is available on the Japan site \(jp.alibabacloud.com\) |
|ProductCode|String|No|dds|The code of the product. Default value: **dds**. |
|BusinessInfo|String|No|\{"AccountPassword":"Pw123456","DBInstanceDescription":"test"\}|The additional information. |
|CouponNo|String|No|youhuiquan\_promotion\_option\_id\_for\_blank|The coupon code. Default value: **youhuiquan\_promotion\_option\_id\_for\_blank**. |
|OrderParamOut|String|No|false|Specifies whether to return the parameters about the order. Valid values:

-   false: returns no parameters.
-   true: returns parameters.

Default value: **false**. |
|ResourceGroupId|String|No|sg-bpxxxxxxxxxxxxxxxxxx|The ID of the resource group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Order|Struct| |Details about the order. |
|Coupons|Array of Coupon| |Details about the coupons. |
|Coupon| | | |
|CouponNo|String|youhuiquan\_promotion\_option\_id\_for\_blank|The coupon code. |
|Description|String|Example description|The description of the coupon. |
|IsSelected|String|true|Indicates whether the coupon was selected. |
|Name|String|youhuiquan111|The name of the coupon. |
|Currency|String|CNY|The currency of the coupon. |
|DiscountAmount|String|322.4|The discount amount of the order. |
|OriginalAmount|String|322.4|The original price of the order. |
|RuleIds|List|\{"RuleId": \[11111111,11111111,11111111\]\}|The list of one or more promotion rule IDs. |
|TradeAmount|String|0|The final price of the order. |
|OrderParams|String|\{\\"autoPay\\":false\}"|The order parameters. This parameter is returned if the `OrderParamOut` parameter is set to `true`. |
|RequestId|String|82530058-D4CF-49A4-96FB-9DD2DF3CE93E|The ID of the request. |
|Rules|Array of Rule| |Details about the promotion rules. |
|Rule| | | |
|Name|String|demoname|The name of the rule. |
|RuleDescId|Long|11111111|The ID of the rule. |
|Title|String|demo|The title of the rule. |
|SubOrders|Array of SubOrder| |Details about the rules that match the coupon. |
|SubOrder| | | |
|DiscountAmount|String|322.4|The discount amount of the order. |
|InstanceId|String|dds-bpxxxxxxxx|The ID of the instance. |
|OriginalAmount|String|322.4|The original price of the order. |
|RuleIds|List|\{"RuleId": \[11111111,11111111,11111111\]\}|The list of one or more promotion rule IDs. |
|TradeAmount|String|0|The final price of the order. |
|TraceId|String|11111111111111111111111111111111|The ID of the trace. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribePrice
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
&<Common request parameters>
```

Sample responses

`XML` fomat

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
<OrderParams>{"autoPay":false,"autoUseCoupon":false,"bid":"26842","buyerId":140xxxxxxxxxxxxx,"commodities":[{"chargeType":"PREPAY","commodityCode":"badds","components":[{"componentCode":"dds_region","free":false,"moduleAttrStatus":3,"moduleParams":{},"properties":[{"code":"dds_region","name":"China (Hangzhou)","value":"cn-hangzhou"}]},{"componentCode":"dds_dbtype","free":false,"moduleAttrStatus":3,"moduleParams":{},"properties":[{"code":"dds_dbtype","name":"MongoDB","value":"MongoDB"}]},{"componentCode":"dds_dbversion","free":false,"moduleAttrStatus":3,"moduleParams":{},"properties":[{"code":"dds_dbversion","name":" 4.2","value":" 4.2"}]},{"componentCode":"dds_class","free":false,"moduleAttrStatus":3,"moduleParams":{},"properties":[{"code":"dds_class","name":"dds.mongo.mid","value":"dds.mongo.mid"}]},{"componentCode":"dds_storage","free":false,"moduleAttrStatus":3,"moduleParams":{},"properties":[{"code":"dds_storage","name":"10","value":"10"}]},{"componentCode":"replication_factor","free":false,"moduleAttrStatus":3,"moduleParams":{},"properties":[{"code":"replication_factor","name":"5","value":"5"}]},{"componentCode":"readonly_replicas","free":false,"moduleAttrStatus":3,"moduleParams":{},"properties":[{"code":"readonly_replicas","name":"0","value":"0"}]}],"duration":1,"free":false,"instanceId":"dds-bp1xxxxxxxxxxxxx","migrateOrder":false,"orderParams":{},"orderType":"UPGRADE","periodAlign":false,"prePayPostCharge":false,"pricingCycle":"Day","quantity":1,"renewChange":false,"specUpdate":false,"syncToSubscription":false,"upgradeInquireFinancialValue":true}],"fromApp":"OpenApi","orderParams":{"promotion_input_param":"{\"promotionFilter\":{\"youhui_quan\":true},\"promotionOptionCode\":\"youhui_quan\",\"promotionOptionNo\":\"youhuiquan_promotion_option_id_for_blank\"}"},"rateWithTax":false,"requestId":"82530058-D4CF-49A4-96FB-9DD2DF3CE93E","token":"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx","userId":140xxxxxxxxxxxxx}</OrderParams>
<Rules>
    <Rule>
        <RuleDescId>102xxxxxxxxxxxxx</RuleDescId>
        <Name>Sample coupon</Name>
    </Rule>
</Rules>
```

`JSON` format

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
    "OrderParams": "{\"autoPay\":false,\"autoUseCoupon\":false,\"bid\":\"26842\",\"buyerId\":140xxxxxxxxxxxxx,\"commodities\":[{\"chargeType\":\"PREPAY\",\"commodityCode\":\"badds\",\"components\":[{\"componentCode\":\"dds_region\",\"free\":false,\"moduleAttrStatus\":3,\"moduleParams\":{},\"properties\":[{\"code\":\"dds_region\",\"name\":\"China (Hangzhou)\",\"value\":\"cn-hangzhou\"}]},{\"componentCode\":\"dds_dbtype\",\"free\":false,\"moduleAttrStatus\":3,\"moduleParams\":{},\"properties\":[{\"code\":\"dds_dbtype\",\"name\":\"MongoDB\",\"value\":\"MongoDB\"}]},{\"componentCode\":\"dds_dbversion\",\"free\":false,\"moduleAttrStatus\":3,\"moduleParams\":{},\"properties\":[{\"code\":\"dds_dbversion\",\"name\":\" 4.2\",\"value\":\" 4.2\"}]},{\"componentCode\":\"dds_class\",\"free\":false,\"moduleAttrStatus\":3,\"moduleParams\":{},\"properties\":[{\"code\":\"dds_class\",\"name\":\"dds.mongo.mid\",\"value\":\"dds.mongo.mid\"}]},{\"componentCode\":\"dds_storage\",\"free\":false,\"moduleAttrStatus\":3,\"moduleParams\":{},\"properties\":[{\"code\":\"dds_storage\",\"name\":\"10\",\"value\":\"10\"}]},{\"componentCode\":\"replication_factor\",\"free\":false,\"moduleAttrStatus\":3,\"moduleParams\":{},\"properties\":[{\"code\":\"replication_factor\",\"name\":\"5\",\"value\":\"5\"}]},{\"componentCode\":\"readonly_replicas\",\"free\":false,\"moduleAttrStatus\":3,\"moduleParams\":{},\"properties\":[{\"code\":\"readonly_replicas\",\"name\":\"0\",\"value\":\"0\"}]}],\"duration\":1,\"free\":false,\"instanceId\":\"dds-bp1xxxxxxxxxxxxx\",\"migrateOrder\":false,\"orderParams\":{},\"orderType\":\"UPGRADE\",\"periodAlign\":false,\"prePayPostCharge\":false,\"pricingCycle\":\"Day\",\"quantity\":1,\"renewChange\":false,\"specUpdate\":false,\"syncToSubscription\":false,\"upgradeInquireFinancialValue\":true}],\"fromApp\":\"OpenApi\",\"orderParams\":{\"promotion_input_param\":\"{\\\"promotionFilter\\\":{\\\"youhui_quan\\\":true},\\\"promotionOptionCode\\\":\\\"youhui_quan\\\",\\\"promotionOptionNo\\\":\\\"youhuiquan_promotion_option_id_for_blank\\\"}\"},\"rateWithTax\":false,\"requestId\":\"82530058-D4CF-49A4-96FB-9DD2DF3CE93E\",\"token\":\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\",\"userId\":140xxxxxxxxxxxxx}",
    "Rules": {
        "Rule": [
            {
                "RuleDescId": "102xxxxxxxxxxxxx",
                "Name": "Sample coupon"
            }
        ]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

