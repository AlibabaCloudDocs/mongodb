# ReleasePublicNetworkAddress

You can call this operation to release the public endpoint of an ApsaraDB for MongoDB instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ReleasePublicNetworkAddress&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ReleasePublicNetworkAddress|The operation that you want to perform. Set the value to **ReleasePublicNetworkAddress**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

**Note:** If you set this parameter to the ID of a sharded cluster instance, you must also specify the **NodeId** parameter. |
|NodeId|String|No|s-bpxxxxxxxx|A sharded cluster instance consists of three components: mongos, shard, and Configserver.

**Note:**

-   This parameter is valid only if you set the **DBInstanceId** parameter to the ID of a sharded cluster instance.
-   You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the ID of the mongos, shard, or Configserver node. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1D6AFE36-1AF5-4DE4-A954-672159D4CC69|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=ReleasePublicNetworkAddress
&DBInstanceId=dds-bpxxxxxxxx
&s-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` fomat

```
<ReleasePublicNetworkAddressResponse>
      <RequestId>B6D17591-B48B-4D31-9CD6-9B9796B2270A</RequestId>
</ReleasePublicNetworkAddressResponse>
```

`JSON` format

```
{
    "RequestId": "1D6AFE36-1AF5-4DE4-A954-672159D4CC69"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

