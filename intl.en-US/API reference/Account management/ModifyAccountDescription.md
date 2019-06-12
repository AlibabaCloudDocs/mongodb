# ModifyAccountDescription {#doc_api_Dds_ModifyAccountDescription .reference}

You can call this operation to modify the description of the root account of a MongoDB instance.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=ModifyAccountDescription) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyAccountDescription|The operation that you want to perform. Set the value to **ModifyAccountDescription**.

 |
|AccountName|String|Yes|root|The name of the account for which you want to modify the description.

 |
|AccountDescription|String|Yes|superadmin|The description of the account.

 -   It cannot start with http:// or https://.
-   It must start with a letter.
-   It must be 2 to 256 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\).

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|59DE9FC2-7B40-45CF-9011-7327A8A771A2|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=ModifyAccountDescription
&AccountName=root
&AccountDescription=superadmin
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<RestoreDBInstanceResponse>
  <RequestId>59DE9FC2-7B40-45CF-9011-7327A8A771A2</RequestId>
</RestoreDBInstanceResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"59DE9FC2-7B40-45CF-9011-7327A8A771A2"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

