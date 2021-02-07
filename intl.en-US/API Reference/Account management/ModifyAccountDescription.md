# ModifyAccountDescription

You can call this operation to modify the description of the root account of an ApsaraDB for MongoDB instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ModifyAccountDescription&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyAccountDescription|The operation that you want to perform. Set the value to **ModifyAccountDescription**. |
|AccountDescription|String|Yes|superadmin|The description of the account.

-   The description must start with a letter, and cannot start with http:// or https://.
-   It must be 2 to 256 characters in length, and can contain letters, digits, underscores \(\_\), and hyphens \(-\). |
|AccountName|String|Yes|root|The name of the account for which you want to modify the description. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|59DE9FC2-7B40-45CF-9011-7327A8A771A2|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=ModifyAccountDescription
&AccountName=root
&AccountDescription=superadmin
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RestoreDBInstanceResponse>
      <RequestId>59DE9FC2-7B40-45CF-9011-7327A8A771A2</RequestId>
</RestoreDBInstanceResponse>
```

`JSON` format

```
{
    "RequestId": "59DE9FC2-7B40-45CF-9011-7327A8A771A2"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

