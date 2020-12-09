# DescribeMongoDBLogConfig

You can call DescribeMongoDBLogConfig to view the log service configuration of ApsaraDB for MongoDB.

This interface is based on the new version of MongoDB log service. For more information, see [activate new audit logs](~~164542~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeMongoDBLogConfig&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeMongoDBLogConfig|The operation that you want to perform. Set the value to **DescribeMongoDBLogConfig**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. You can call [DescribeDBInstances](~~61939~~) to query. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call [DescribeDBInstanceAttribute](~~62010~~) to query. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IsEtlMetaExist|Integer|1|Whether the rule to distribute logs to Logtail is created. For more information about Logtail, see [Logtail overview](~~28979~~). Valid values:

-   1: Created
-   0 or null: not created |
|IsUserProjectLogstoreExist|Integer|1|Whether the log service project exists in the current region. Valid values:

-   1: Exists
-   0 or null: does not exist |
|RequestId|String|664ECE26-658 A- 47C5-88F6-870B0132E8D2|The ID of the request. |
|UserProjectName|String|nosql-140xxxxxxxxxxxxx-cn-hangzhou|Specifies the name of the project in log service. |

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

## Error code

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

