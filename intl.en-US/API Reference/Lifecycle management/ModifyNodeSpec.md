# ModifyNodeSpec

You can call this operation to modify the instance type and storage capacity of a node of an ApsaraDB for MongoDB sharded cluster instance.

Before you call this operation, make sure that you understand the billing methods and [pricing](https://www.alibabacloud.com/zh/product/apsaradb-for-mongodb/pricing) of ApsaraDB for MongoDB.

This operation applies to only sharded cluster instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ModifyNodeSpec&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyNodeSpec|The operation that you want to perform. Set the value to **ModifyNodeSpec**. |
|NodeId|String|Yes|d-bpxxxxxxxx|The ID of the shard or mongos node that you want to modify. You can call the [DescribeDBInstanceAttribute](~~61923~~) operation to query the ID.

 **Note:** If you set this parameter to the ID of the shard node, you must also specify the **NodeStorage** parameter. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|NodeClass|String|No|dds.shard.standard|The specifications of the shard or mongos node. For more information, see [Instance types](~~57141~~).

 **Note:** You must specify one of the **NodeClass** and NodeStorage parameters. |
|NodeStorage|Integer|No|20|The storage capacity of the shard node.

 -   Valid values: **10** to **2000**. Unit: GB.
-   The value must be a multiple of 10 GB.

 **Note:**

-   You must specify one of the **NodeClass** and NodeStorage parameters.
-   This parameter takes effect only when the **NodeId** parameter is set to the ID of the shard node. |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The token can contain only ASCII characters and cannot exceed 64 characters in length. |
|AutoPay|Boolean|No|true|Specifies whether to enable automatic payment for the instance. Valid values:

 -   **true**: enables automatic payment. Make sure that your account has sufficient balance.
-   **false**: disables automatic payment. You must perform the following operations to pay for the instance: Log on to the ApsaraDB for MongoDB console. In the top navigation bar, click **Expenses**. The **Billing Management** page appears. In the left-side navigation pane, click **Orders**. On the page that appears, find the order and complete the payment.

 Default value: **true**. |
|EffectiveTime|String|No|Immediately|The time when the modified configuration values take effect. Valid values:

 -   **Immediately**: The settings immediately take effect.
-   **MaintainTime**: The settings take effect during the maintenance window of the instance.

 Default value: **Immediately**. |
|FromApp|String|No|OpenApi|The source of the request. Valid values:

 -   **OpenApi**: the ApsaraDB for MongoDB API
-   **mongo\_buy**: the ApsaraDB for MongoDB console |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |
|OrderType|String|No|UPGRADE|The type of the order. Valid values:

 -   **UPGRADE**
-   **DOWNGRADE** |
|ReadonlyReplicas|Integer|No|5|The number of the read-only nodes in the shard node. Valid values: **0** to **5**. Default value: **0**.

 **Note:** This parameter is available only for ApsaraDB for MongoDB instances that are purchased on the Alibaba Cloud China site. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OrderId|String|2033xxxxxxxxx|The ID of the order. |
|RequestId|String|EFFC5788-8BB5-41B5-9F15-9CFC5A0E8FCC|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=ModifyNodeSpec
&NodeId=d-bpxxxxxxxx
&DBInstanceId=dds-bpxxxxxxxx
&NodeClass=dds.shard.standard
&NodeStorage=20
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyNodeSpecResponse>
	  <OrderId>2033xxxxxxxxx</OrderId>
	  <RequestId>EFFC5788-8BB5-41B5-9F15-9CFC5A0E8FCC</RequestId>
</ModifyNodeSpecResponse>
```

`JSON` format

```
{
    "OrderId": "2033xxxxxxxx",
    "RequestId": "EFFC5788-8BB5-41B5-9F15-9CFC5A0E8FCC"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

