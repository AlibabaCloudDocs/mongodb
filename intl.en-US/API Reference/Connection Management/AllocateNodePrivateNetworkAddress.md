# AllocateNodePrivateNetworkAddress

You can call this operation to apply for an internal endpoint for a shard or Configserver node of an ApsaraDB for MongoDB sharded cluster instance.

This operation is applicable only to sharded cluster instances. For more information, see [Apply for a connection string of a shard or Configserver node](~~134037~~).

**Note:** The requested endpoint can only be accessed over the internal network. If you want to access the endpoint over the public network, call the [AllocatePublicNetworkAddress](~~67602~~) operation to apply for a public endpoint.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=AllocateNodePrivateNetworkAddress&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AllocateNodePrivateNetworkAddress|The operation that you want to perform. Set the value to **AllocateNodePrivateNetworkAddress**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the sharded cluster instance. |
|NodeId|String|Yes|d-bpxxxxxxxx|The ID of the shard or Configserver node.

 **Note:** You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the ID of the shard or Configserver node. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |
|ZoneId|String|No|cn-hangzhou-b|The zone ID of the instance.

 **Note:** You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the zone ID of the instance. |
|AccountName|String|No|shardcsaccount|The name of the account.

 **Note:**

-   The name must be 4 to 16 characters in length and can contain lowercase letters, digits, and underscores \(\_\). It must start with a lowercase letter.
-   You need to set the account and password only when you apply for the endpoint of a shard or Configserver node for the first time. The account and password are required for all shard and Configserver nodes.
-   The permissions of this account are fixed to read-only. |
|AccountPassword|String|No|Test123456|The password for the account.

 -   The password must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include `! #$%^&*()_+-=`
-   The password must be 8 to 32 characters in length. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|EFD65226-08CC-4C4D-B6A4-CB3C382F67B0|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=AllocateNodePrivateNetworkAddress
&DBInstanceId=dds-bpxxxxxxxx
&NodeId=d-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<AllocateNodePrivateNetworkAddressResponse>
	  <RequestId>EFD65226-08CC-4C4D-B6A4-CB3C382F67B0</RequestId>
</AllocateNodePrivateNetworkAddressResponse>
```

`JSON` format

```
{
	"RequestId":"0FDDC511-7252-4A4A-ADDA-5CB1BF63873D"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

