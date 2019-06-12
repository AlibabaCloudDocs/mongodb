# UpgradeDBInstanceKernelVersion {#doc_api_Dds_UpgradeDBInstanceKernelVersion .reference}

You can call this operation to upgrade the minor database version of a MongoDB instance.

The instance must be in the running state when you call this operation.

**Note:** 

 

-   This operation is applicable to replica set instances and sharded cluster instances. UpgradeDBInstanceKernelVersion cannot be performed on standalone instances.

-   The instance will be restarted once during the upgrade. Perform this operation during off-peak hours.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=UpgradeDBInstanceKernelVersion) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|No|UpgradeDBInstanceKernelVersion|The operation that you want to perform. Set the value to **UpgradeDBInstanceKernelVersion**.

 |
|DBInstanceId|String|No|dds-bpxxxxxxxx|The ID of the instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|27B9A130-7C4B-40D9-84E8-2FC081097AAC|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=UpgradeDBInstanceKernelVersion
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<UpgradeDBInstanceKernelVersionResponse>
  <RequestId>27B9A130-7C4B-40D9-84E8-2FC081097AAC</RequestId> 
</UpgradeDBInstanceKernelVersionResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"27B9A130-7C4B-40D9-84E8-2FC081097AAC"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

