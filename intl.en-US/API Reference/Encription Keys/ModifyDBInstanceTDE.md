# ModifyDBInstanceTDE

You can call this operation to modify the transparent data encryption \(TDE\) status of an ApsaraDB for MongoDB instance.

TDE can be used to perform real-time I/O encryption and decryption on data files. Data is encrypted before being written to disks, and decrypted before being read from disks to the memory. For more information, see [Configure TDE](~~131048~~).

**Note:** After TDE is enabled, it cannot be disabled.

Before you call this operation, make sure that the following requirements are met:

-   A replica set or sharded cluster instance is used.
-   The storage engine of the instance is WiredTiger.
-   The database engine version of the instance is 4.0 or 4.2. If the database engine version is earlier than 4.0, you can call the [UpgradeDBInstanceEngineVersion](~~67608~~) operation to upgrade the database engine.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceTDE&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description |
|---------|----|--------|-------|------------|
|Action|String|Yes|ModifyDBInstanceTDE|The operation that you want to perform. Set the value to **ModifyDBInstanceTDE**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of an instance. |
|TDEStatus|String|Yes|enabled|The TDE status. Set the value to **Enabled**.

 **Note:** Exercise caution when enabling TDE. After TDE is enabled, it cannot be disabled. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the region ID of the instance. |
|EncryptorName|String|No|aes-256-cbc|The encryption method. Set the value to **AES-256-CBC**.

 **Note:** This parameter is valid only when you specify the **TEDStatus** parameter to **enabled**. |
|EncryptionKey|String|No|749c1df7-xxxx-xxxx-xxxx-xxxxxxxxxxxx|The custom key. |
|RoleARN|String|No|acs:ram::123456789012\*\*\*\*:role/adminrole|The ARN of the role. It is in the format of `acs:ram::$accountID:role/$roleName`.

 **Note:**

-   `$accountID`: indicates the ID of the Alibaba Cloud account that owns the RAM role. To view the account ID, log on to the Alibaba Cloud Management Console, move your pointer over your profile picture in the upper-right corner, and then click Security Settings.
-   `$roleName`: indicates the name of the RAM role. To view the RAM role name, perform the following steps: Log on to the RAM console. In the left-side navigation pane, click RAM Roles. In the RAM Role Name column on the page that appears, you can view the name of the RAM role. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|434D7127-6229-4355-BA50-7A3685A725DF|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=ModifyDBInstanceTDE
&DBInstanceId=dds-bpxxxxxxxx
&TDEStatus=enabled
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDBInstanceTDEResponse>
	  <RequestId>434D7127-6229-4355-BA50-7A3685A725DF</RequestId>
</ModifyDBInstanceTDEResponse>
```

`JSON` format

```
{
	"RequestId": "434D7127-6229-4355-BA50-7A3685A725DF"
}
```

## Error code

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|IncorrectDBInstanceState|Current DB instance state does not support this operation.|The error message returned because the operation is not supported while the instance is in its current state. Check whether the specified parameters are correct.|
|403|IncorrectDBInstanceLockMode|Current DB instance lock mode does not support this operation.|The error message returned because the instance is locked.|

For more information about error codes, visit [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

