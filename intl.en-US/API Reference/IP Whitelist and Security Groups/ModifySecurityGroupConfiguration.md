# ModifySecurityGroupConfiguration

You can call this operation to modify an ECS Security group that is bound to an ApsaraDB for MongoDB instance.

**Note:** For a sharded cluster instance, the bound ECS security group takes effect only for mongos nodes.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ModifySecurityGroupConfiguration&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifySecurityGroupConfiguration|The operation that you want to perform. Set the value to **ModifySecurityGroupConfiguration**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|SecurityGroupId|String|Yes|sg-bpxxxxxxxx|The ID of the ECS security group.

**Note:**

-   You can bind up to 10 ECS security groups to an ApsaraDB for MongoDB instance.
-   You can call the [DescribeSecurityGroup](~~25556~~) operation of ECS to query the security groups in the specified region. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|E062C482-1A4B-469E-938C-96D28CFAE42E|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=ModifySecurityGroupConfiguration
&DBInstanceId=dds-bpxxxxxxxx
&SecurityGroupId=sg-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RequestId>E062C482-1A4B-469E-938C-96D28CFAE42E</RequestId>
```

`JSON` format

```
{
    "RequestId": "E062C482-1A4B-469E-938C-96D28CFAE42E"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

