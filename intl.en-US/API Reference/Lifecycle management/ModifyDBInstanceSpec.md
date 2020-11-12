# ModifyDBInstanceSpec

You can call this operation to modify the specifications or storage space of an ApsaraDB for MongoDB instance.

Before you call this operation, make sure that you understand the billing methods and [pricing](https://www.alibabacloud.com/zh/product/apsaradb-for-mongodb/pricing) of ApsaraDB for MongoDB.

This operation is only applicable to standalone instances and replica set instances. You can call the [ModifyNodeSpec](~~61923~~), [CreateNode](~~61911~~), and [DeleteNode](~~61922~~) operations to modify the configurations of sharded cluster instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceSpec&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceSpec|The operation that you want to perform. Set the value to**ModifyDBInstanceSpec**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of an instance. |
|DBInstanceClass|String|No|dds.mongo.standard|The type of the instance. For more information, see [Instance types](~~57141~~).

**Note:** You must specify either this parameter or the**DBInstanceStorage**parameter. |
|DBInstanceStorage|String|No|50|The storage space of the instance.

-   Valid values: **10** to **3000**. Unit: GB. The values that can be specified for this parameter are dependent on the instance specifications. For more information, see [Instance types](~~57141~~).
-   The value must be a multiple of 10 GB.

**Note:**

-   You must specify either this parameter or the**DBInstanceStorage**parameter.
-   Storage space can be scaled down only on replica set instances whose billing method is Subscription. The storage space you scale down must be greater than the used storage space. |
|OrderType|String|No|UPGRADE|The type of configuration changes performed. Default value: DOWNGRADE. Valid values:

-   **UPGRADE**: The specifications are upgraded.
-   **DOWNGRADE**: The specifications are downgraded.

**Note:** This parameter is only applicable to instances whose billing method is subscription. |
|AutoPay|Boolean|No|true|Indicates whether automatic payment is enabled for the instance. Valid values:

-   **true**: enables automatic payment. Make sure that your account has sufficient balance.
-   **false**: Automatic payment is not enabled. You must make payments in the console. Payment instructions: Log on to the console. In the upper-right corner, click **Billing Management** and select **Billing Management** from the drop-down list. The Billing Management page appears. In the left-side navigation pane, click **Bills**. On the Unpaid tab, click Make a Payment in the Actions column corresponding to the bill you want to pay.

Default value: **true**. |
|BusinessInfo|String|No|\{“ActivityId":"000000000"\}|The business information. |
|ReplicationFactor|String|No|3|The number of data nodes.

-   Valid values for a replica set instance: **3, 5, and 7**.
-   Valid values for a standalone instance: **1**. |
|CouponNo|String|No|youhuiquan\_promotion\_option\_id\_for\_blank|The coupon code. Default value:**youhuiquan\_promotion\_option\_id\_for\_blank**. |
|EffectiveTime|String|No|Immediately|The time when the modified configuration values take effect. Valid values:

-   **Immediately**: The settings take effect immediately.
-   **MaintainTime**: The instance will be migrated during the maintenance period of the instance.

Default value: **Immediately**. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the region ID of the instance. |
|ReadonlyReplicas|String|No|1|The number of read-only nodes. Valide values: **1** to **5**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OrderId|String|2033xxxxxxxx|The ID of the order. |
|RequestId|String|C5662998-62BE-4C7F-961D-7DFE775DD813|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=ModifyDBInstanceSpec
&DBInstanceId=dds-bpxxxxxxxx
&DBInstanceStorage=50
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDBInstanceSpecResponse>    
      <OrderId>2033xxxxxxxx</OrderId>
      <RequestId>C5662998-62BE-4C7F-961D-7DFE775DD813</RequestId>
</ModifyDBInstanceSpecResponse>
```

`JSON` format

```
{
    "OrderId": "2033xxxxxxxx",
    "RequestId": "C5662998-62BE-4C7F-961D-7DFE775DD813"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

