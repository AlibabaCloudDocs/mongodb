# ModifyDBInstanceSSL {#doc_api_Dds_ModifyDBInstanceSSL .reference}

You can call this operation to modify the SSL configuration of a MongoDB instance.

Ensure that the instance meets the following conditions when you call this operation:

-   The instance is in the running state.
-   The instance type is replica set.
-   The database version of the instance is 3.4 or 4.0.

**Note:** Whenever you enable or disable SSL encryption, or update the SSL certificate, the instance will restart. We recommend that you call this operation during off-peak hours.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceSSL) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceSSL|The operation that you want to perform. Set the value to **DescribeDBInstanceSSL**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|SSLAction|String|Yes|Open|The operation that you perform to execute SSL features. Valid values:

 -   **Open**: enables SSL encryption.
-   **Close**: disables SSL encryption.
-   **Update**: updates the SSL certificate.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|6D806B11-078F-4154-BF9F-844F56D08964|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=ModifyDBInstanceSSL
&DBInstanceId=dds-bpxxxxxxxx
&SSLAction=Open
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyDBInstanceSSLResponse>
  <RequestId>6D806B11-078F-4154-BF9F-844F56D08964</RequestId>
</ModifyDBInstanceSSLResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"6D806B11-078F-4154-BF9F-844F56D08964"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|IncorrectDBInstanceState|Current DB instance state does not support this operation.|The error message returned when the operation is not supported while the instance is in its current state. Check whether the specified parameters are correct.|
|403|IncorrectDBInstanceLockMode|Current DB instance lock mode does not support this operation.|The error message returned when the instance is locked.|

[View error codes](https://error-center.aliyun.com/status/product/Dds)

