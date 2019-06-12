# CreateNode {#doc_api_Dds_CreateNode .reference}

You can call this operation to create shards or mongos for ApsaraDB for MongoDB sharded cluster instances.

 **Make sure that you fully understand the billing methods and [pricing](https://www.alibabacloud.com/zh/product/apsaradb-for-mongodb/pricing) of ApsaraDB for MongoDB before using this API.** 

This operation can be performed only on sharded cluster instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=CreateNode) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateNode|The operation that you want to perform. Set the value to **CreateNode**.

 |
|NodeClass|String|Yes|dds.shard.mid|The specification of the shard or mongos. For more information, see [Instance specifications](~~57141~~).

 |
|NodeType|String|Yes|shard|The type of the node. Valid values:

 -   **shard**
-   **mongos**

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the sharded cluster instance.

 |
|NodeStorage|Integer|No|10|The storage space of the node. You must specify this parameter if the value of the **NodeType** parameter is **Shard**.

 -   Valid values: **10** to **2000**. Unit: GB.
-   You can only specify this value in 10 GB increments.

 |
|AutoPay|Boolean|No|true|Indicates whether automatic payment is enabled for the instance. Valid values:

 -   **true**: Automatic payment is enabled. Make sure that your account has sufficient balance.
-   **false**: Automatic payment is not enabled. You must make payments in the console. Payment instructions: Log on to the console. In the upper-right corner, click **Billing Management** and select **Billing Management** from the drop-down list. The Billing Management page appears. In the left-side navigation pane, click **Bills**. On the Unpaid tab, click Make a Payment in the Actions column corresponding to the bill you want to pay.

 Default value: **true**.

 **Note:** This parameter is only applicable to Subscription-based instances.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure idempotence of the request. You can use the client to generate this value, but you must ensure that it is unique among different requests. The token can contain only ASCII characters, and cannot exceed 64 characters in length.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OrderId|String|2034xxxxxxxx|The ID of the order.

 |
|RequestId|String|7D48FB19-20CA-4725-A870-3D8F5CE69F14|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=CreateNode
&NodeClass=dds.shard.mid
&NodeType=shard
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CreateNodeResponse>
  <OrderId>2034xxxxxxxx</OrderId>
  <RequestId>7D48FB19-20CA-4725-A870-3D8F5CE69F14</RequestId> 
</CreateNodeResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"7D48FB19-20CA-4725-A870-3D8F5CE69F14",
	"OrderId":"2034xxxxxxxx"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

