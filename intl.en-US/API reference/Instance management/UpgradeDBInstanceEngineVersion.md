# UpgradeDBInstanceEngineVersion {#doc_api_Dds_UpgradeDBInstanceEngineVersion .reference}

You can call this operation to upgrade the database version of a MongoDB instance.

This operation is applicable to replica set instances and sharded cluster instances. UpgradeDBInstanceEngineVersion cannot be performed on standalone instances.

The instance must be in the running state when you call this operation.

**Note:** 

 

-   The storage engine of the instance is binding on the selection of database versions. For more information, see [Version and storage engines](~~61906~~).

-   The database version cannot be downgraded after the database version is upgraded.
-   The instance will be automatically restarted for two to three times during the upgrade process. Make sure that the instance is executed during off-peak hours.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=UpgradeDBInstanceEngineVersion) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|EngineVersion|String|Yes|4.0|The target database version to be upgraded to. Valid values: **3.4** and **4.0**.

 **Note:** The target database version must be later than the current database version of the instance.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|Action|String|No|UpgradeDBInstanceEngineVersion|The operation that you want to perform. Set the value to **UpgradeDBInstanceEngineVersion**.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|C4907B00-A208-4E0C-A636-AA85140E406C|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=UpgradeDBInstanceEngineVersion
&EngineVersion=4.0
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<UpgradeDBInstanceEngineVersionResponse>
  <RequestId>C4907B00-A208-4E0C-A636-AA85140E406C</RequestId>
</UpgradeDBInstanceEngineVersionResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"C4907B00-A208-4E0C-A636-AA85140E406C"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

