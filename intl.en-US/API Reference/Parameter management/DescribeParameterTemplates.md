# DescribeParameterTemplates

You can call this operation to query the list of default parameter templates for ApsaraDB for MongoDB instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeParameterTemplates&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeParameterTemplates|The operation that you want to perform. Set the value to **DescribeParameterTemplates**. |
|Engine|String|Yes|mongodb|The database engine of the instance. Set the value to **mongodb**. |
|EngineVersion|String|Yes|4.0|The version of the database engine. Valid values: **3.4**, **4.0**, and **4.2**.

数据库版本号。取值：**3.4**、**4.0**、**4.2**或**4.4**。 |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Parameters|Array of TemplateRecord| |Details about parameter templates. |
|TemplateRecord| | | |
|CheckingCode|String|\[0-65536\]|The valid values of the parameter. |
|ForceModify|Boolean|true|Indicates whether the parameter is modifiable.

 -   **false**
-   **true** |
|ForceRestart|Boolean|false|Indicates whether a restart is required for parameter modifications to take effect.

 -   **false**: A restart is not required. Modifications take effect immediately.
-   **true**: A restart is required for modifications to take effect. |
|ParameterDescription|String|The threshold in milliseconds at which the database profiler considers a query slow, default is 100.|The description of the parameter. |
|ParameterName|String|operationProfiling.slowOpThresholdMs|The name of the parameter. |
|ParameterValue|String|100|The default value of the parameter. |
|RequestId|String|76B66D95-0670-4199-A8B1-E362286CD015|The ID of the request. |
|ParameterCount|String|5|The number of parameters. |
|EngineVersion|String|4.0|The version of the database engine. |
|Engine|String|mongodb|The database engine of the instance. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeParameterTemplates
&Engine=mongodb
&EngineVersion=4.0
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeParameterTemplatesResponse>
	  <Parameters>
		    <TemplateRecord>
			      <ForceModify>true</ForceModify>
			      <ParameterDescription></ParameterDescription>
			      <ParameterValue>snappy</ParameterValue>
			      <CheckingCode>snappy|zlib|disabled</CheckingCode>
			      <ForceRestart>true</ForceRestart>
			      <ParameterName>net.compression.compressors</ParameterName>
		    </TemplateRecord>
		    <TemplateRecord>
			      <ForceModify>true</ForceModify>
			      <ParameterDescription>The level of database profiling, which inserts information about operation performance into the system.profile collection. 'off' for no profiling, 'slowOp' for only includes slow operations, 'all' for includes all operations, default is 'slowOp'. </ParameterDescription>
			      <ParameterValue>slowOp</ParameterValue>
			      <CheckingCode>off|slowOp|all</CheckingCode>
			      <ForceRestart>false</ForceRestart>
			      <ParameterName>operationProfiling.mode</ParameterName>
		    </TemplateRecord>
		    <TemplateRecord>
			      <ForceModify>true</ForceModify>
			      <ParameterDescription>The threshold in milliseconds at which the database profiler considers a query slow, default is 100. </ParameterDescription>
			      <ParameterValue>100</ParameterValue>
			      <CheckingCode>[0-65536]</CheckingCode>
			      <ForceRestart>false</ForceRestart>
			      <ParameterName>operationProfiling.slowOpThresholdMs</ParameterName>
		    </TemplateRecord>
		    <TemplateRecord>
			      <ForceModify>true</ForceModify>
			      <ParameterDescription>The expiration threshold in milliseconds for idle cursors before MongoDB removes them; i.e. MongoDB removes cursors that have been idle for the specified cursorTimeoutMillis. default is 600000(i.e. 10 minutes)</ParameterDescription>
			      <ParameterValue>600000</ParameterValue>
			      <CheckingCode>[1-2147483647]</CheckingCode>
			      <ForceRestart>false</ForceRestart>
			      <ParameterName>setParameter.cursorTimeoutMillis</ParameterName>
		    </TemplateRecord>
		    <TemplateRecord>
			      <ForceModify>true</ForceModify>
			      <ParameterDescription>The maximum memory bytes that sort stage may use, default is 33554432(i.e. 32MB)</ParameterDescription>
			      <ParameterValue>33554432</ParameterValue>
			      <CheckingCode>[33554432-268435456]</CheckingCode>
			      <ForceRestart>false</ForceRestart>
			      <ParameterName>setParameter.internalQueryExecMaxBlockingSortBytes</ParameterName>
		    </TemplateRecord>
	  </Parameters>
	  <RequestId>76B66D95-0670-4199-A8B1-E362286CD015</RequestId>
	  <ParameterCount>5</ParameterCount>
	  <EngineVersion>4.0</EngineVersion>
	  <Engine>mongodb</Engine>
</DescribeParameterTemplatesResponse>
```

`JSON` format

```
{
	"Parameters": {
		"TemplateRecord": [
			{
				"ForceModify": true,
				"ParameterDescription": "",
				"ParameterValue": "snappy",
				"CheckingCode": "snappy|zlib|disabled",
				"ForceRestart": true,
				"ParameterName": "net.compression.compressors"
			},
			{
				"ForceModify": true,
				"ParameterDescription": "The level of database profiling, which inserts information about operation performance into the system.profile collection. 'off' for no profiling, 'slowOp' for only includes slow operations, 'all' for includes all operations, default is 'slowOp'.",
				"ParameterValue": "slowOp",
				"CheckingCode": "off|slowOp|all",
				"ForceRestart": false,
				"ParameterName": "operationProfiling.mode"
			},
			{
				"ForceModify": true,
				"ParameterDescription": "The threshold in milliseconds at which the database profiler considers a query slow, default is 100.",
				"ParameterValue": "100",
				"CheckingCode": "[0-65536]",
				"ForceRestart": false,
				"ParameterName": "operationProfiling.slowOpThresholdMs"
			},
			{
				"ForceModify": true,
				"ParameterDescription": "The expiration threshold in milliseconds for idle cursors before MongoDB removes them; i.e. MongoDB removes cursors that have been idle for the specified cursorTimeoutMillis. default is 600000(i.e. 10 minutes)",
				"ParameterValue": "600000",
				"CheckingCode": "[1-2147483647]",
				"ForceRestart": false,
				"ParameterName": "setParameter.cursorTimeoutMillis"
			},
			{
				"ForceModify": true,
				"ParameterDescription": "The maximum memory bytes that sort stage may use, default is 33554432(i.e. 32MB)",
				"ParameterValue": "33554432",
				"CheckingCode": "[33554432-268435456]",
				"ForceRestart": false,
				"ParameterName": "setParameter.internalQueryExecMaxBlockingSortBytes"
			}
		]
	},
	"RequestId": "76B66D95-0670-4199-A8B1-E362286CD015",
	"ParameterCount": "5",
	"EngineVersion": "4.0",
	"Engine": "mongodb"
}
```

## Error codes

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

