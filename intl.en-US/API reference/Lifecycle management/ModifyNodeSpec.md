# ModifyNodeSpec {#doc_api_Dds_ModifyNodeSpec .reference}

You can call this operation to modify the type and storage space of the nodes in ApsaraDB for MongoDB sharded cluster instances.

 **Make sure that you fully understand the billing methods and [pricing](https://www.alibabacloud.com/zh/product/apsaradb-for-mongodb/pricing) of ApsaraDB for MongoDB before using this API.** 

This operation can be performed only on sharded cluster instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=ModifyNodeSpec) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyNodeSpec|The operation that you want to perform. Set the value to **ModifyNodeSpec**.

 |
|NodeId|String|Yes|d-bpxxxxxxxx|The ID of the shard or mongos in the sharded cluster instance. You can call the [DescribeDBInstanceAttribute](~~61923~~) operation to query the ID.

 **Note:** If you specify this parameter to the ID of a shard, you must also specify the **NodeStorage** parameter.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|NodeClass|String|No|dds.shard.standard|The specification of the shard or mongos. For more information, see [Instance specifications](~~57141~~).

 **Note:** You must specify either this parameter or the **NodeStorage** parameter.

 |
|NodeStorage|Integer|No|20|The storage space set for the shard.

 -   Valid values: **10** to **2000**. Unit: GB.
-   You can only specify this value in 10 GB increments.

 **Note:** 

-   You must specify either this parameter or the **NodeClass** parameter.
-   This parameter is only valid when you specify the **NodeId** parameter to the ID of the shard.

 |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure idempotence of the request. You can use the client to generate this value, but you must ensure that it is unique among different requests. The token can contain only ASCII characters, and cannot exceed 64 characters in length.

 |
|AutoPay|Boolean|No|true|Indicates whether automatic payment is enabled for the instance. Valid values:

 -   **true**: Automatic payment is enabled. Make sure that your account has sufficient balance.
-   **false**: Automatic payment is not enabled. You must make payments in the console. Payment instructions: Log on to the console. In the upper-right corner, click **Billing Management** and select **Billing Management** from the drop-down list. The Billing Management page appears. In the left-side navigation pane, click **Bills**. On the Unpaid tab, click Make a Payment in the Actions column corresponding to the bill you want to pay.

 Default value: **true**.

 |
|EffectiveTime|String|No|Immediately|The time when the modified configuration values take effect. Valid values:

 -   **Immediately**: The configurations take effect immediately.
-   **MaintainTime**: The configurations take effect during the maintenance period of the instance.

 Default value: **Immediately**.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OrderId|String|2033xxxxxxxxx|The ID of the order.

 |
|RequestId|String|EFFC5788-8BB5-41B5-9F15-9CFC5A0E8FCC|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=ModifyNodeSpec
&NodeId=d-bpxxxxxxxx 
&DBInstanceId=dds-bpxxxxxxxx
&NodeClass=dds.shard.standard
&NodeStorage=20
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyNodeSpecResponse>
  <OrderId>2033xxxxxxxxx</OrderId>
  <RequestId>EFFC5788-8BB5-41B5-9F15-9CFC5A0E8FCC</RequestId> 
</ModifyNodeSpecResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"EFFC5788-8BB5-41B5-9F15-9CFC5A0E8FCC",
	"OrderId":"2033xxxxxxxx"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

