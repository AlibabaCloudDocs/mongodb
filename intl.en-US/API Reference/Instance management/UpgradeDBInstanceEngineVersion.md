# UpgradeDBInstanceEngineVersion

You can call this operation to upgrade the database version of an ApsaraDB for MongoDB instance.

The instance must be in the running state when you call this operation.

**Note:**

-   The available database versions are subject to the storage engine used by the instance. For more information, see [MongoDB versions and storage engines](~~61906~~). You can also call the [DescribeAvailableEngineVersion](~~141355~~) operation to query the available database versions.
-   The database version cannot be downgraded after it is upgraded.
-   The instance is automatically restarted for two to three times during the upgrade process. Make sure that you upgrade the instance during off-peak hours.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=UpgradeDBInstanceEngineVersion&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpgradeDBInstanceEngineVersion|The operation that you want to perform. Set the value to **UpgradeDBInstanceEngineVersion**. |
|EngineVersion|String|Yes|4.0|The database version to which you want to upgrade the instance. Valid values: **3.4**, **4.0**, or **4.2**.

**Note:** The target database version must be later than the current database version of the instance. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|RegionId|String|No|cn-hangzhou|The ID of the region where the instance is deployed. You can call the [DescribeRegions](~~61933~~) operation to query the region ID. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|C4907B00-A208-4E0C-A636-AA85140E406C|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=UpgradeDBInstanceEngineVersion
&EngineVersion=4.0
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UpgradeDBInstanceEngineVersionResponse>
      <RequestId>C4907B00-A208-4E0C-A636-AA85140E406C</RequestId>
</UpgradeDBInstanceEngineVersionResponse>
```

`JSON` format

```
{
    "RequestId": "C4907B00-A208-4E0C-A636-AA85140E406C"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

