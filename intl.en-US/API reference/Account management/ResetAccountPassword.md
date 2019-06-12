# ResetAccountPassword {#doc_api_Dds_ResetAccountPassword .reference}

You can call this operation to reset the password of the root account of a MongoDB instance.

**Note:** This operation can reset only the password of the root account of an instance.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=ResetAccountPassword) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ResetAccountPassword|The operation that you want to perform. Set the value to **ResetAccountPassword**.

 |
|AccountName|String|Yes|root|The account for which you want to reset the password. Valid value: **root**.

 |
|AccountPassword|String|Yes|Ali! 123456|The new password.

 -   The password must contain characters from at least three of the following categories: uppercase letters, lowercase letters, digits, and special characters. Special characters include !\#$%^&\*\(\)\_+-=
-   The password must be 8 to 32 characters in length.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|06CBD06E-ABC9-4121-AB93-3C3820B3E7E6|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=ResetAccountPassword
&AccountName=root
&AccountPassword=Ali! 123456
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ResetAccountPasswordResponse>
  <RequestId>06CBD06E-ABC9-4121-AB93-3C3820B3E7E6</RequestId>
</ResetAccountPasswordResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"06CBD06E-ABC9-4121-AB93-3C3820B3E7E6"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

