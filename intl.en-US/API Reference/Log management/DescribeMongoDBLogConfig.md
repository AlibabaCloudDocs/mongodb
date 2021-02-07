# DescribeMongoDBLogConfig

You can call this operation to query the log feature configurations of an ApsaraDB for MongoDB instance.

This operation is based on the new log feature of ApsaraDB for MongoDB. For more information, see [Enable the new audit log feature](~~164542~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeMongoDBLogConfig&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeMongoDBLogConfig|The operation that you want to perform. Set the value to **DescribeMongoDBLogConfig**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. You can call the [DescribeDBInstances](~~61939~~) operation to query the ID of the instance. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IsEtlMetaExist|Integer|1|Indicates whether a rule to distribute logs to Logtail is created. For more information, see [Logtail overview](~~28979~~). Valid values:

-   1: A rule to distribute logs to Logtail is created
-   0 or null: A rule to distribute logs to Logtail is not created. |
|IsUserProjectLogstoreExist|Integer|1|Indicates whether a Log Service project exists in the current region. Valid values:

-   1: A Log Service project exists in the current region.
-   0 or null: A Log Service project does not exist in the current region. |
|RequestId|String|664ECE26-658A-47C5-88F6-870B0132E8D2|The ID of the request. |
|UserProjectName|String|nosql-140xxxxxxxxxxxxx-cn-hangzhou|The name of the Log Service project. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeMongoDBLogConfig
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UserProjectName>nosql-140xxxxxxxxxxxxx-cn-hangzhou</UserProjectName>
<RequestId>FECF2277-3EA1-4CD9-AEB9-E7DED5E84E35</RequestId>
<IsUserProjectLogstoreExist>1</IsUserProjectLogstoreExist>
<IsEtlMetaExist>1</IsEtlMetaExist>
```

`JSON` format

```
{
    "UserProjectName": "nosql-140xxxxxxxxxxxxx-cn-hangzhou",
    "RequestId": "FECF2277-3EA1-4CD9-AEB9-E7DED5E84E35",
    "IsUserProjectLogstoreExist": 1,
    "IsEtlMetaExist": 1
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

