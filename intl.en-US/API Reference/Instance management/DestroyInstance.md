# DestroyInstance

You can call this operation to release an ApsaraDB for MongoDB instance.

Before you call this operation, make sure that the following requirements are met:

-   The billing method of the instance is subscription.
-   The instance has expired and is in the **Locking** state.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DestroyInstance&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Position|Type|Required|Example|Description|
|---------|--------|----|--------|-------|-----------|
|Action|Query|String|Yes|DestroyInstance|The operation that you want to perform. Set the value to **DestroyInstance**. |
|InstanceId|Query|String|No|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** **InstanceId** and **DBInstanceId** serve the same function. You need only to specify one of them. |
|DBInstanceId|Query|String|No|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** **InstanceId** and **DBInstanceId** serve the same function. You need only to specify one of them. |
|ClientToken|Query|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The token can contain only ASCII characters and cannot exceed 64 characters in length. |
|RegionId|Host|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to view the region ID of the instance. |
|ResourceGroupId|Query|String|No|rg-axxxxxxxx|The ID of the resource group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DestroyInstance
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` fomat

```
<DestroyInstanceResponse>
	  <RequestId>65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
</DestroyInstanceResponse>
```

`JSON` format

```
{
"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

