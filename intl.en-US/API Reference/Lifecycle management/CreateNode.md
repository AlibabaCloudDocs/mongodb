# CreateNode

You can call this operation to create a shard or mongos node for an ApsaraDB for MongoDB sharded cluster instance.

Before you call this operation, make sure that you understand the billing methods and [pricing](https://www.alibabacloud.com/zh/product/apsaradb-for-mongodb/pricing) of ApsaraDB for MongoDB.

This operation applies to only sharded cluster instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=CreateNode&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateNode|The operation that you want to perform. Set the value to **CreateNode**. |
|NodeClass|String|Yes|dds.shard.mid|The specifications of the shard or mongos node. For more information, see [Instance specifications](~~57141~~). |
|NodeType|String|Yes|shard|The type of the node. Valid values:

 -   **shard**
-   **mongos** |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the sharded cluster instance. |
|NodeStorage|Integer|No|10|The storage capacity of the node. This parameter is available and required if you set the **NodeType** parameter to **Shard**.

 -   Valid values: **10** to **2000**. Unit: GB.
-   The value must be a multiple of 10 GB. |
|FromApp|String|No|OpenApi|The source of the request. Valid values:

 -   **OpenApi**: the ApsaraDB for MongoDB API
-   **mongo\_buy**: the ApsaraDB for MongoDB console |
|AutoPay|Boolean|No|true|Specifies whether to enable automatic payment. Valid values:

 -   **true**: enables automatic payment. Make sure that your account has sufficient balance.
-   **false**: disables automatic payment. You must perform the following operations to pay for the instance: Log on to the ApsaraDB for MongoDB console. In the top navigation bar, click **Expenses**. The **Billing Management** page appears. In the left-side navigation pane, click **Orders**. On the page that appears, find the order and complete the payment.

 Default value: **true**.

 **Note:** This parameter is applicable to only subscription instances. |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The token can contain only ASCII characters and cannot exceed 64 characters in length. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |
|ReadonlyReplicas|Integer|No|5|The number of the read-only nodes in the shard node. Valid values: **0** to **5**. Default value: **0**.

 **Note:** This parameter is available only for ApsaraDB for MongoDB instances that are purchased on the Alibaba Cloud China site. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NodeId|String|d-bpxxxxxxxxxxxxxx|The ID of the node. |
|OrderId|String|2034xxxxxxxx|The ID of the order. |
|RequestId|String|7D48FB19-20CA-4725-A870-3D8F5CE69F14|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=CreateNode
&NodeClass=dds.shard.mid
&NodeType=shard
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateNodeResponse>
	  <OrderId>2034xxxxxxxx</OrderId>
	  <RequestId>7D48FB19-20CA-4725-A870-3D8F5CE69F14</RequestId>
</CreateNodeResponse>
```

`JSON` format

```
{"RequestId":"7D48FB19-20CA-4725-A870-3D8F5CE69F14",
	"NodeId":"d-bpxxxxxxxxxxxxxx",
	"OrderId":"2034xxxxxxxx"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

