# ModifyDBInstanceNetworkType {#doc_api_Dds_ModifyDBInstanceNetworkType .reference}

You can call this operation to change the network type of a MongoDB instance.

This operation is applicable to replica set instances and sharded cluster instances. ModifyDBInstanceNetworkType cannot be performed on standalone instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceNetworkType) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceNetworkType|The operation that you want to perform. Set the value to **ModifyDBInstanceNetworkType**.

 |
|NetworkType|String|Yes|VPC|The network type to switch to. Valid values:

 -   **VPC**: changes the network type to VPC.
-   **Classic**: changes the network type to classic network.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|VpcId|String|No|vpc-bpxxxxxxxx|The ID of the VPC.

 **Note:** This parameter must be specified when **NetworkType** is set to **VPC**.

 |
|VSwitchId|String|No|vsw-bpxxxxxxxx|The VSwitch ID of the VPC.

 **Note:** This parameter must be specified when **NetworkType** is set to **VPC**.

 |
|RetainClassic|String|No|True|Indicates whether to retain the original classic network address when you change the network type to VPC. Valid values:

 -   **True**: retains the original classic network address.
-   **False**: does not retain the original classic network address.

 **Note:** 

 

-   This parameter can be specified only when **NetworkType** is set to **VPC**.

-   When this parameter is set to **True**, you must also specify the **ClassicExpiredDays** parameter.

 |
|ClassicExpiredDays|Integer|No|30|The retention period of the original classic network address when you change the network type to VPC. Valid values: **14**, **30**, **60**, and **120**. Unit: days.

 **Note:** 

 

-   This parameter can be specified only when **NetworkType** is set to **VPC**.

-   This parameter must be specified when **RetainClassic** is set to **True**.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|7A9807F0-1301-4154-9849-6497E94A04DB|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=ModifyDBInstanceNetworkType
&NetworkType=VPC 
&DBInstanceId=dds-bpxxxxxxxx
&VpcId=vpc-bpxxxxxxxx
&VSwitchId=vsw-bpxxxxxxxx
&RetainClassic=True
&ClassicExpiredDays=30
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyDBInstanceNetworkTypeResponse>
  <RequestId>7A9807F0-1301-4154-9849-6497E94A04DB</RequestId> 
</ModifyDBInstanceNetworkTypeResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"7A9807F0-1301-4154-9849-6497E94A04DB"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

