# ModifyInstanceVpcAuthMode {#doc_api_Dds_ModifyInstanceVpcAuthMode .reference}

You can call this operation to enable or disable authentication for a MongoDB instance to allow access from the same VPC as the instance.

Ensure that the instance meets the following conditions when you call this operation:

-   The instance type is replica set or sharded cluster.
-   The database version of the instance is 4.0, and the database minor version is mongodb\_20190408\_3.0.11 and later. You can call [DescribeDBInstanceAttribute](~~62010~~) to query the version information. If the database version is earlier than the supported ones, you can call [UpgradeDBInstanceEngineVersion](~~67608~~) to upgrade the database to a supported version.
-   The network type of the instance is VPC. If the network type is Classic Network, you can call [ModifyDBInstanceNetworkType](~~62138~~) to switch the network type to VPC.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=ModifyInstanceVpcAuthMode) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyInstanceVpcAuthMode|The operation that you want to perform. Set the value to **ModifyInstanceVpcAuthMode**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|VpcAuthMode|String|Yes|Open|Indicates whether to enable authentication to allow access within a VPC. Valid values:

 -   **Open**: Authentication is enabled.
-   **Close**: Authentication is disabled.

 |
|NodeId|String|No|s-bpxxxxxxxx|The ID of the mongos in the specified sharded cluster instance.

 **Note:** This parameter can be used only when the instance type is sharded cluster.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|BA51E9D9-B14A-4542-B6E6-7DE00BECCB8C|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=ModifyInstanceVpcAuthMode
&DBInstanceId=dds-bpxxxxxxxx
&VpcAuthMode=Open
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyInstanceVpcAuthModeResponse>
  <RequestId>BA51E9D9-B14A-4542-B6E6-7DE00BECCB8C</RequestId>
</ModifyInstanceVpcAuthModeResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"BA51E9D9-B14A-4542-B6E6-7DE00BECCB8C"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

