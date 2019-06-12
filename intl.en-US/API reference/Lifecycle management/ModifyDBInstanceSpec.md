# ModifyDBInstanceSpec {#doc_api_Dds_ModifyDBInstanceSpec .reference}

You can call this operation to modify the specification or storage space of ApsaraDB for MongoDB replica set instances.

 **Make sure that you fully understand the billing methods and [pricing](https://www.alibabacloud.com/zh/product/apsaradb-for-mongodb/pricing) of ApsaraDB for MongoDB before using this API.** 

This parameter is only applicable to replica set instances. You can call the [ModifyNodeSpec](~~61923~~), [CreateNode](~~61911~~), or [DeleteNode](~~61922~~) operations to modify the configurations of sharded cluster instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceSpec) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceSpec|The operation that you want to perform. Set the value to **ModifyDBInstanceSpec**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|DBInstanceClass|String|No|dds.mongo.standard|The specification of the instance. For more information, see [Instance specifications](~~57141~~).

 **Note:** You must specify either this parameter or the **DBInstanceStorage** parameter.

 |
|DBInstanceStorage|String|No|50|The storage space of the instance.

 -   Valid values: 10 to 3000. Unit: GB. The values that can be specified for this parameter are dependent on the instance specification. For more information, see [Instance specifications](~~57141~~).
-   You can only specify this value in 10 GB increments.

 **Note:** 

 

-   You must specify either this parameter or the **DBInstanceStorage** parameter.

-   Storage space can be scaled down only on replica set instances whose billing method is Subscription. The storage space you scale down must be greater than the used storage space.

 |
|OrderType|String|No|UPGRADE|The type of configuration changes performed. Valid values:

 -   UPGRADE: The specifications are upgraded.
-   DOWNGRADE: The specifications are downgraded. This is the default value.

 **Note:** This parameter is only applicable to instances whose billing method is Subscription.

 |
|AutoPay|Boolean|No|true|Indicates whether automatic payment is enabled for the instance. Valid values:

 -   **true**: Automatic payment is enabled. Make sure that your account has sufficient balance.
-   **false**: Automatic payment is not enabled. You must make payments in the console. Payment instructions: Log on to the console. In the upper-right corner, click **Billing Management** and select **Billing Management** from the drop-down list. The Billing Management page appears. In the left-side navigation pane, click **Bills**. On the Unpaid tab, click Make a Payment in the Actions column corresponding to the bill you want to pay.

 Default value: **true**.

 |
|BusinessInfo|String|No|\{“ActivityId":"000000000"\}|The business information.

 |
|ReplicationFactor|String|No|3|The number of nodes in the replica set instance. Valid values: **3, 5, and 7**. Default value: **3**.

 |
|CouponNo|String|No|youhuiquan\_promotion\_option\_id\_for\_blank|The coupon code. Default value: **youhuiquan\_promotion\_option\_id\_for\_blank**.

 |
|EffectiveTime|String|No|Immediately|The time when the modified configuration values take effect. Valid values:

 -   **Immediately**: The configurations take effect immediately.
-   **MaintainTime**: The configurations take effect during the maintenance period of the instance.

 Default value**: Immediately**.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OrderId|String|2033xxxxxxxx|The ID of the order.

 |
|RequestId|String|C5662998-62BE-4C7F-961D-7DFE775DD813|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=ModifyDBInstanceSpec
&DBInstanceId=dds-bpxxxxxxxx
&DBInstanceStorage=50
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyDBInstanceSpecResponse>
  <OrderId>2033xxxxxxxx</OrderId>
  <RequestId>C5662998-62BE-4C7F-961D-7DFE775DD813</RequestId>
</ModifyDBInstanceSpecResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"C5662998-62BE-4C7F-961D-7DFE775DD813",
	"OrderId":"2033xxxxxxxx"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

