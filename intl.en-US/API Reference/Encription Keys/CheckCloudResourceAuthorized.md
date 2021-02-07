# CheckCloudResourceAuthorized

You can call this operation to check whether KMS keys are authorized to ApsaraDB for MongoDB instances.

Before you enable Transparent Data Encryption \(TDE\) by calling the [ModifyDBInstanceTDE](~~131267~~) operation, you can call this operation to check whether KMS keys are authorized to ApsaraDB for MongoDB instances.

**Note:** TDE cannot be enabled if KMS keys are not authorized to ApsaraDB for MongoDB instances. You can <xref href="https://workorder-intl.console.aliyun.com/console.htm\#/ticket/createIndex" format="html" scope="external" props="intl"\>submit a ticket</xref\><xref href="https://selfservice.console.aliyun.com/ticket/createIndex" format="html" scope="external" props="china"\>submit a ticket</xref\> to modify the authorization information.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=CheckCloudResourceAuthorized&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CheckCloudResourceAuthorized|The operation that you want to perform. Set the value to **CheckCloudResourceAuthorized**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|TargetRegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the region ID of the instance. |
|RegionId|String|No|cn-hangzhou|The region ID. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|A0181AC4-F186-46ED-87CA-100C70B86729|The ID of the request. |
|AuthorizationState|Integer|1|Indicates whether KMS keys are authorized to ApsaraDB for MongoDB instances. Valid values:

 -   **0**: KMS keys are not authorized.
-   **1**: KMS keys are authorized.
-   **2**: KMS is not enabled. |
|RoleArn|String|acs:ram::140xxxxxxxx:role/aliyunrdsinstanceencryptiondefaultrole|The role information of the authorized Alibaba Resource Name \(ARN\).

 **Note:** This parameter is returned only when the value of the **AuthorizationState** parameter is **1**. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=CheckCloudResourceAuthorized
&DBInstanceId=dds-bpxxxxxxxx
&TargetRegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RequestId>A0181AC4-F186-46ED-87CA-100C70B86729</RequestId>
<AuthorizationState>1</AuthorizationState>
<RoleArn>acs:ram::140xxxxxxxx:role/aliyunrdsinstanceencryptiondefaultrole</RoleArn>
```

`JSON` format

```
{
	"RequestId": "A0181AC4-F186-46ED-87CA-100C70B86729",
	"AuthorizationState": 1,
	"RoleArn": "acs:ram::140xxxxxxxx:role/aliyunrdsinstanceencryptiondefaultrole"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

