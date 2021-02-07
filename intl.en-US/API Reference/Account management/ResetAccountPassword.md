# ResetAccountPassword

You can call this operation to reset the password of the root account of an ApsaraDB for MongoDB instance.

**Note:** This operation can reset only the password of the root account of an instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ResetAccountPassword&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ResetAccountPassword|The operation that you want to perform. Set the value to **ResetAccountPassword**. |
|AccountName|String|Yes|root|The account for which you want to reset the password. Set the value to**root**. |
|AccountPassword|String|Yes|Ali! 123456|The new password.

-   The password must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include `! # $ % ^ & * ( ) _ + - =`
-   The password must be 8 to 32 characters in length. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|06CBD06E-ABC9-4121-AB93-3C3820B3E7E6|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=ResetAccountPassword
&AccountName=root
&AccountPassword=Ali! 123456
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ResetAccountPasswordResponse>
      <RequestId>06CBD06E-ABC9-4121-AB93-3C3820B3E7E6</RequestId>
</ResetAccountPasswordResponse>
```

`JSON` format

```
{
    "RequestId": "06CBD06E-ABC9-4121-AB93-3C3820B3E7E6"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

