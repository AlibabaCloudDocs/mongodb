# ReleaseNodePrivateNetworkAddress

You can call this operation to release the internal endpoint of the shard or Configserver node of a sharded cluster instance.

This operation is applicable only to sharded cluster instances. For more information, see [Release the connection string of a shard or Configserver node](~~134067~~).

**Note:** This operation releases the internal endpoint of the node. If you have also applied for a public endpoint for the node and want to release the public endpoint, you can call the [ReleasePublicNetworkAddress](~~67604~~) operation to release the public endpoint.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ReleaseNodePrivateNetworkAddress&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ReleaseNodePrivateNetworkAddress|The operation that you want to perform. Set the value to **ReleaseNodePrivateNetworkAddress**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the sharded cluster instance. |
|NodeId|String|Yes|d-bpxxxxxxxx|The ID of the shard or Configserver node.

 **Note:** You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the ID of the shard or Configserver node. |
|NetworkType|String|Yes|VPC|The network type of the internal endpoint. Valid values:

 -   **VPC**
-   **Classic**

 **Note:** You can call the [DescribeShardingNetworkAddress](~~62135~~) operation to query the network type of the internal endpoint. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|0FDDC511-7252-4A4A-ADDA-5CB1BF63873D|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=ReleaseNodePrivateNetworkAddress
&DBInstanceId=dds-bpxxxxxxxx
&NodeId=d-bpxxxxxxxx
&NetworkType=VPC
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ReleaseNodePrivateNetworkAddressResponse>
	  <RequestId>EFD65226-08CC-4C4D-B6A4-CB3C382F67B0</RequestId>
</ReleaseNodePrivateNetworkAddressResponse>
```

`JSON` format

```
{
	"RequestId":"0FDDC511-7252-4A4A-ADDA-5CB1BF63873D"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

