# RenewDBInstance {#doc_api_Dds_RenewDBInstance .reference}

You can call this operation to manually renew a Subscription instance.

 **Make sure that you fully understand the billing methods and [pricing](https://www.alibabacloud.com/zh/product/apsaradb-for-mongodb/pricing) of ApsaraDB for MongoDB before using this API.** 

This parameter is only applicable to Subscription instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=RenewDBInstance) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RenewDBInstance|The operation that you want to perform. Set the value to **RenewDBInstance**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|Period|Integer|Yes|1|The period you set for the instance to implement payment renewal. Unit: months. Valid values: **1-9, 12, 24, and 36**.

 |
|CouponNo|String|No|1111111111111111|The coupon code. Default value: **youhuiquan\_promotion\_option\_id\_for\_blank**.

 |
|AutoPay|Boolean|No|true|Indicates whether automatic payment is enabled for the instance. Valid values:

 -   **true**: Automatic payment is enabled. Make sure that your account has sufficient balance.
-   **false**: Automatic payment is not enabled. You must make payments in the console. Payment instructions: Log on to the console. In the upper-right corner, click **Billing Management** and select **Billing Management** from the drop-down list. The Billing Management page appears. In the left-side navigation pane, click **Bills**. On the Unpaid tab, click Make a Payment in the Actions column corresponding to the bill you want to pay.

 Default value: **true**.

 |
|BusinessInfo|String|No|\{“ActivityId":"000000000"\}|The business information.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure idempotence of the request. You can use the client to generate this value, but you must ensure that it is unique among different requests. The token can contain only ASCII characters, and cannot exceed 64 characters in length.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OrderId|String|203317xxxxxxxx|The ID generated for the order.

 |
|RequestId|String|B118EF45-9633-4EE3-8405-42ED4373721B|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=RenewDBInstance
&DBInstanceId=dds-bpxxxxxxxx
&Period=1
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<RenewDBInstanceResponse>
  <OrderId>2033xxxxxxxx</OrderId>
  <RequestId>B118EF45-9633-4EE3-8405-42ED4373721B</RequestId> 
</RenewDBInstanceResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"B118EF45-9633-4EE3-8405-42ED4373721B",
	"OrderId":"2033xxxxxxxx"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

