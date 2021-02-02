# ModifyDBInstanceSSL

You can call this operation to modify the SSL configuration of a MongoDB instance.

Before you call this operation, make sure that the following requirements are met:

-   The instance is in the running state.
-   The instance type is replica set.
-   The database version of the instance is 3.4 or 4.0.

**Note:** When you enable or disable SSL encryption or update the SSL certificate, the instance restarts. We recommend that you call this operation during off-peak hours.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceSSL&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|No|ModifyDBInstanceSSL|The operation that you want to perform. Set the value to **ModifyDBInstanceSSL**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|SSLAction|String|Yes|Open|The operation that you perform to execute SSL features. Valid values:

-   **Open**: enables SSL encryption.
-   **Close**: disables SSL encryption.
-   **Update**: updates the SSL certificate. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeDBInstanceAttribute](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|6D806B11-078F-4154-BF9F-844F56D08964|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=ModifyDBInstanceSSL
&DBInstanceId=dds-bpxxxxxxxx
&SSLAction=Open
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDBInstanceSSLResponse>
      <RequestId>6D806B11-078F-4154-BF9F-844F56D08964</RequestId>
</ModifyDBInstanceSSLResponse>
```

`JSON` format

```
{
    "RequestId": "6D806B11-078F-4154-BF9F-844F56D08964"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|IncorrectDBInstanceState|Current DB instance state does not support this operation.|The error message returned because the operation is not supported when the instance is in its current state. Check whether the specified parameters are correct.|
|403|IncorrectDBInstanceLockMode|Current DB instance lock mode does not support this operation.|The error message returned because the instance is locked.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

