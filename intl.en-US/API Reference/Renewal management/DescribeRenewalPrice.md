# DescribeRenewalPrice

You can call this operation to query the monthly renewal price of an ApsaraDB for MongoDB instance.

This operation is applicable to subscription instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeRenewalPrice&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeRenewalPrice|The operation that you want to perform. Set the value to **DescribeRenewalPrice**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|BusinessInfo|String|No|\{“ActivityId":"000000000"\}|The business information. It is an additional parameter. |
|CouponNo|String|No|youhuiquan\_promotion\_option\_id\_for\_blank|The coupon code. Default value: **youhuiquan\_promotion\_option\_id\_for\_blank**. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|SubOrders|Array| |The rules matching the coupons. |
|SubOrder| | | |
|DiscountAmount|Float|1144.8|The discount amount of the order. |
|InstanceId|String|dds-bpxxxxxxxx|The ID of the instance. |
|OriginalAmount|Float|1144.8|The original price of the order. |
|RuleIds|List|\{"RuleId": \[11111111,11111111,11111111\]\}|The IDs of the matched rules. |
|TradeAmount|Float|0|The actual price of the order. |
|RequestId|String|EFD65226-08CC-4C4D-B6A4-CB3C382F67B0|The ID of the request. |
|Order|Struct| |The list of orders. |
|Coupons|Array| |An array that consists of the information of coupons. |
|Coupon| | | |
|CouponNo|String|youhuiquan\_promotion\_option\_id\_for\_blank|The coupon number. |
|Description|String|coupondemo|The description of the coupon. |
|IsSelected|String|true|Indicates whether the coupon was selected. |
|Name|String|youhuiquan111|The name of the coupon. |
|Currency|String|CNY|The type of the currency. |
|DiscountAmount|Float|1144.8|The discount amount of the order. |
|OriginalAmount|Float|1144.8|The original price of the order. |
|RuleIds|List|11111111|The IDs of the matched rules. |
|TradeAmount|Float|0|The actual price of the order. |
|Rules|Array| |An array that consists of the information of coupon rules. |
|Rule| | | |
|Name|String|demoname|The name of the rule. |
|RuleDescId|Long|11111111|The ID of the rule. |
|Title|String|demo|The title of the rule. |

## Examples

Sample request

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeRenewalPrice
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeRenewalPriceResponse>
	  <SubOrders>
		    <SubOrder>
			      <RuleIds>
				        <RuleId>11111111</RuleId>
				        <RuleId>11111111</RuleId>
				        <RuleId>11111111</RuleId>
			      </RuleIds>
			      <OriginalAmount>1144.8</OriginalAmount>
			      <TradeAmount>0</TradeAmount>
			      <InstanceId>dds-bpxxxxxxxx</InstanceId>
			      <DiscountAmount>1144.8</DiscountAmount>
		    </SubOrder>
	  </SubOrders>
	  <RequestId>C45C9E98-289B-42F4-84C8-03FD5E29B3EB</RequestId>
	  <Order>
		    <RuleIds>
			      <RuleId>11111111</RuleId>
		    </RuleIds>
		    <OriginalAmount>1144.8</OriginalAmount>
		    <TradeAmount>0</TradeAmount>
		    <Coupons></Coupons>
		    <DiscountAmount>1144.8</DiscountAmount>
		    <Currency>CNY</Currency>
	  </Order>
	  <Rules>
		    <Rule>
			      <Name>demo</Name>
			      <RuleDescId>11111111</RuleDescId>
		    </Rule>
	  </Rules>
</DescribeRenewalPriceResponse>
```

`JSON` format

```
{
    "SubOrders": {
        "SubOrder": [
            {
                "RuleIds": {
                    "RuleId": [
                        11111111,
                        11111111,
                        11111111
                    ]
                },
                "OriginalAmount": 1144.8,
                "TradeAmount": 0,
                "InstanceId": "dds-bpxxxxxxxx",
                "DiscountAmount": 1144.8
            }
        ]
    },
    "RequestId": "C45C9E98-289B-42F4-84C8-03FD5E29B3EB",
    "Order": {
        "RuleIds": {
            "RuleId": [
                11111111
            ]
        },
        "OriginalAmount": 1144.8,
        "TradeAmount": 0,
        "Coupons": {
            "Coupon": []
        },
        "DiscountAmount": 1144.8,
        "Currency": "CNY"
    },
    "Rules": {
        "Rule": [
            {
                "Name": "demo",
                "RuleDescId": 11111111
            }
        ]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

