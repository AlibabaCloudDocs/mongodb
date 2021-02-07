# ModifyInstanceVpcAuthMode

You can call this operation to enable or disable password-free access from the same VPC as an ApsaraDB for MongoDB instance.

Before you call this operation, make sure that the following requirements are met:

-   A replica set or sharded cluster instance is used.
-   The database version of the instance is 4.0 \(with the minor version of mongodb\_20190408\_3.0.11 or later\) or 4.2. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to view the database engine version of the instance. If necessary, you can call the [UpgradeDBInstanceEngineVersion](~~67608~~) operation to upgrade the database engine.
-   The instance is in a VPC. If the network type is Classic Network, you can call the [ModifyDBInstanceNetworkType](~~62138~~) opeartion to switch the network type to VPC.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ModifyInstanceVpcAuthMode&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyInstanceVpcAuthMode|The operation that you want to perform. Set the value to **ModifyInstanceVpcAuthMode**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the region ID of the instance. |
|NodeId|String|No|s-bpxxxxxxxx|The ID of the mongos node in the specified sharded cluster instance.

 **Note:** This parameter can be used only when the instance type is sharded cluster. |
|VpcAuthMode|String|No|Open|Specifies whether to enable authentication to allow access within a VPC. Valid values:

 -   **Open**: enables password-free access.
-   **Close**: disables password-free access. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|BA51E9D9-B14A-4542-B6E6-7DE00BECCB8C|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=ModifyInstanceVpcAuthMode
&DBInstanceId=dds-bpxxxxxxxx
&VpcAuthMode=Open
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyInstanceVpcAuthModeResponse>
	  <RequestId>BA51E9D9-B14A-4542-B6E6-7DE00BECCB8C</RequestId>
</ModifyInstanceVpcAuthModeResponse>
```

`JSON` format

```
{
	"RequestId": "BA51E9D9-B14A-4542-B6E6-7DE00BECCB8C"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

