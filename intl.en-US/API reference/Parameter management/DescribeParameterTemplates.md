# DescribeParameterTemplates {#doc_api_Dds_DescribeParameterTemplates .reference}

You can call this operation to query the list of default parameter templates for ApsaraDB for MongoDB instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeParameterTemplates) simplifies API usage. You can use OpenAPI explorer to perform operations such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeParameterTemplates|The operation that you want to perform. Set the value to **DescribeParameterTemplates**.

 |
|Engine|String|Yes|mongodb|The database engine. Set the value to **mongodb**.

 |
|EngineVersion|String|Yes|4.0|The version number of the database. Valid values: **3.2**, **3.4**, **and 4.0**.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Parameters| | |The parameter templates.

 |
|└CheckingCode|String|\[0-65536\]|The range of the parameter value.

 |
|└ForceModify|Boolean|true|Indicates whether the parameter is modifiable.

 -   **false**
-   **true**

 |
|└ForceRestart|Boolean|false|Indicates whether a restart is required for parameter modifications to take effect.

 -   **false**: A restart is not required. Modifications take effect immediately after they are made.
-   **true**: A restart is required for modifications to take effect.

 |
|└ParameterDescription|String|The threshold in milliseconds at which the database profiler considers a query slow, default is 100.|The description of the parameter.

 |
|└ParameterName|String|operationProfiling.slowOpThresholdMs|The name of the parameter.

 |
|└ParameterValue|String|100|The default value of the parameter.

 |
|RequestId|String|76B66D95-0670-4199-A8B1-E362286CD015|The ID of the request.

 |
|ParameterCount|String|5|The number of parameters.

 |
|EngineVersion|String|4.0|The version number of the database.

 |
|Engine|String|mongodb|The database engine.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeParameterTemplates
&Engine=mongodb
&EngineVersion=4.0
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeParameterTemplatesResponse>
  <Parameters>
    <TemplateRecord>
      <ForceModify>true</ForceModify>
      <ParameterDescription/>
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

``` {#json_return_success_demo}
{
	"Parameters":{
		"TemplateRecord":[
			{
				"ForceModify":true,
				"ParameterDescription":"",
				"ParameterValue":"snappy",
				"ForceRestart":true,
				"CheckingCode":"snappy|zlib|disabled",
				"ParameterName":"net.compression.compressors"
			},
			{
				"ForceModify":true,
				"ParameterDescription":"The level of database profiling, which inserts information about operation performance into the system.profile collection. 'off' for no profiling, 'slowOp' for only includes slow operations, 'all' for includes all operations, default is 'slowOp'.",
				"ParameterValue":"slowOp",
				"ForceRestart":false,
				"CheckingCode":"off|slowOp|all",
				"ParameterName":"operationProfiling.mode"
			},
			{
				"ForceModify":true,
				"ParameterDescription":"The threshold in milliseconds at which the database profiler considers a query slow, default is 100.",
				"ParameterValue":"100",
				"ForceRestart":false,
				"CheckingCode":"[0-65536]",
				"ParameterName":"operationProfiling.slowOpThresholdMs"
			},
			{
				"ForceModify":true,
				"ParameterDescription":"The expiration threshold in milliseconds for idle cursors before MongoDB removes them; i.e. MongoDB removes cursors that have been idle for the specified cursorTimeoutMillis. default is 600000(i.e. 10 minutes)",
				"ParameterValue":"600000",
				"ForceRestart":false,
				"CheckingCode":"[1-2147483647]",
				"ParameterName":"setParameter.cursorTimeoutMillis"
			},
			{
				"ForceModify":true,
				"ParameterDescription":"The maximum memory bytes that sort stage may use, default is 33554432(i.e. 32MB)",
				"ParameterValue":"33554432",
				"ForceRestart":false,
				"CheckingCode":"[33554432-268435456]",
				"ParameterName":"setParameter.internalQueryExecMaxBlockingSortBytes"
			}
		]
	},
	"RequestId":"76B66D95-0670-4199-A8B1-E362286CD015",
	"ParameterCount":"5",
	"EngineVersion":"4.0",
	"Engine":"mongodb"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

