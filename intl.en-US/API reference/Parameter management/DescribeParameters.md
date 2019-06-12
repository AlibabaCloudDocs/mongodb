# DescribeParameters {#doc_api_Dds_DescribeParameters .reference}

You can call this operation to query information about the parameter configuration of ApsaraDB for MongoDB instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeParameters) simplifies API usage. You can use OpenAPI explorer to perform operations such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeParameters|The operation that you want to perform. Set the value to **DescribeParameters**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** If you specify this parameter to the ID of a sharded cluster instance, you must also specify the **NodeId** parameter.

 |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the mongos or shard in the specified sharded cluster instance.

 **Note:** This parameter is only valid when you specify the **DBInstanceId** parameter to the ID of a sharded cluster instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ConfigParameters| | |The list of configured parameters and their details.

 |
|└CheckingCode|String|\[0-65536\]|The range of the parameter value.

 |
|└ForceRestart|Boolean|true|Indicates whether a restart is required for parameter modifications to take effect.

 -   **false**: A restart is not required. Modifications take effect immediately after they are made.
-   **true**: A restart is required for modifications to take effect.

 |
|└ModifiableStatus|Boolean|true|Indicates whether the parameter is modifiable.

 -   **false**
-   **true**

 |
|└ParameterDescription|String|The threshold in milliseconds at which the database profiler considers a query slow, default is 100.|The description of the parameter.

 |
|└ParameterName|String|operationProfiling.slowOpThresholdMs|The name of the parameter.

 |
|└ParameterValue|String|200|The value of the parameter.

 |
|RequestId|String|3ADD0C7D-2D2A-4F15-88FF-E7AC9B9FDCC8|The ID of the request.

 |
|RunningParameters| | |The configuration of running parameters.

 |
|└CheckingCode|String|\[33554432-268435456\]|The range of the parameter value.

 |
|└ForceRestart|Boolean|false|Indicates whether a restart is required for parameter modifications to take effect.

 -   **false**: A restart is not required. Modifications take effect immediately after they are made.
-   **true**: A restart is required for modifications to take effect.

 |
|└ModifiableStatus|Boolean|true|Indicates whether the parameter is modifiable.

 -   **false**
-   **true**

 |
|└ParameterDescription|String|The maximum memory bytes that sort stage may use, default is 33554432\(i.e. 32MB\)|The description of the parameter.

 |
|└ParameterName|String|setParameter.internalQueryExecMaxBlockingSortBytes|The name of the parameter.

 |
|└ParameterValue|String|33554432|The value of the parameter.

 |
|EngineVersion|String|4.0|The version number of the database.

 |
|Engine|String|mongodb|The database engine. Default value: **mongodb**.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeParameters
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeParametersResponse>
  <ConfigParameters>
    <Parameter>
      <ParameterDescription>The threshold in milliseconds at which the database profiler considers a query slow, default is 100. </ParameterDescription>
      <ParameterValue>200</ParameterValue>
      <CheckingCode>[0-65536]</CheckingCode>
      <ForceRestart>false</ForceRestart>
      <ModifiableStatus>true</ModifiableStatus>
      <ParameterName>operationProfiling.slowOpThresholdMs</ParameterName>
    </Parameter>
  </ConfigParameters>
  <RequestId>3ADD0C7D-2D2A-4F15-88FF-E7AC9B9FDCC8</RequestId>
  <RunningParameters>
    <Parameter>
      <ParameterDescription/>
      <ParameterValue>zlib</ParameterValue>
      <CheckingCode>snappy|zlib|disabled</CheckingCode>
      <ForceRestart>true</ForceRestart>
      <ModifiableStatus>true</ModifiableStatus>
      <ParameterName>net.compression.compressors</ParameterName>
    </Parameter>
    <Parameter>
      <ParameterDescription>The level of database profiling, which inserts information about operation performance into the system.profile collection. 'off' for no profiling, 'slowOp' for only includes slow operations, 'all' for includes all operations, default is 'slowOp'. </ParameterDescription>
      <ParameterValue>slowOp</ParameterValue>
      <CheckingCode>off|slowOp|all</CheckingCode>
      <ForceRestart>false</ForceRestart>
      <ModifiableStatus>true</ModifiableStatus>
      <ParameterName>operationProfiling.mode</ParameterName>
    </Parameter>
    <Parameter>
      <ParameterDescription>The threshold in milliseconds at which the database profiler considers a query slow, default is 100. </ParameterDescription>
      <ParameterValue>220</ParameterValue>
      <CheckingCode>[0-65536]</CheckingCode>
      <ForceRestart>false</ForceRestart>
      <ModifiableStatus>true</ModifiableStatus>
      <ParameterName>operationProfiling.slowOpThresholdMs</ParameterName>
    </Parameter>
    <Parameter>
      <ParameterDescription>The expiration threshold in milliseconds for idle cursors before MongoDB removes them; i.e. MongoDB removes cursors that have been idle for the specified cursorTimeoutMillis. default is 600000(i.e. 10 minutes)</ParameterDescription>
      <ParameterValue>600000</ParameterValue>
      <CheckingCode>[1-2147483647]</CheckingCode>
      <ForceRestart>false</ForceRestart>
      <ModifiableStatus>true</ModifiableStatus>
      <ParameterName>setParameter.cursorTimeoutMillis</ParameterName>
    </Parameter>
    <Parameter>
      <ParameterDescription>The maximum memory bytes that sort stage may use, default is 33554432(i.e. 32MB)</ParameterDescription>
      <ParameterValue>33554432</ParameterValue>
      <CheckingCode>[33554432-268435456]</CheckingCode>
      <ForceRestart>false</ForceRestart>
      <ModifiableStatus>true</ModifiableStatus>
      <ParameterName>setParameter.internalQueryExecMaxBlockingSortBytes</ParameterName>
    </Parameter>
  </RunningParameters>
  <EngineVersion>4.0</EngineVersion>
  <Engine>mongodb</Engine>
</DescribeParametersResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"ConfigParameters":{
		"Parameter":[
			{
				"ParameterDescription":"The threshold in milliseconds at which the database profiler considers a query slow, default is 100.",
				"ParameterValue":"200",
				"ForceRestart":false,
				"CheckingCode":"[0-65536]",
				"ModifiableStatus":true,
				"ParameterName":"operationProfiling.slowOpThresholdMs"
			}
		]
	},
	"RequestId":"3ADD0C7D-2D2A-4F15-88FF-E7AC9B9FDCC8",
	"RunningParameters":{
		"Parameter":[
			{
				"ParameterDescription":"",
				"ParameterValue":"zlib",
				"ForceRestart":"true",
				"CheckingCode":"snappy|zlib|disabled",
				"ModifiableStatus":"true",
				"ParameterName":"net.compression.compressors"
			},
			{
				"ParameterDescription":"The level of database profiling, which inserts information about operation performance into the system.profile collection. 'off' for no profiling, 'slowOp' for only includes slow operations, 'all' for includes all operations, default is 'slowOp'.",
				"ParameterValue":"slowOp",
				"ForceRestart":"false",
				"CheckingCode":"off|slowOp|all",
				"ModifiableStatus":"true",
				"ParameterName":"operationProfiling.mode"
			},
			{
				"ParameterDescription":"The threshold in milliseconds at which the database profiler considers a query slow, default is 100.",
				"ParameterValue":"220",
				"ForceRestart":"false",
				"CheckingCode":"[0-65536]",
				"ModifiableStatus":"true",
				"ParameterName":"operationProfiling.slowOpThresholdMs"
			},
			{
				"ParameterDescription":"The expiration threshold in milliseconds for idle cursors before MongoDB removes them; i.e. MongoDB removes cursors that have been idle for the specified cursorTimeoutMillis. default is 600000(i.e. 10 minutes)",
				"ParameterValue":"600000",
				"ForceRestart":"false",
				"CheckingCode":"[1-2147483647]",
				"ModifiableStatus":"true",
				"ParameterName":"setParameter.cursorTimeoutMillis"
			},
			{
				"ParameterDescription":"The maximum memory bytes that sort stage may use, default is 33554432(i.e. 32MB)",
				"ParameterValue":"33554432",
				"ForceRestart":"false",
				"CheckingCode":"[33554432-268435456]",
				"ModifiableStatus":"true",
				"ParameterName":"setParameter.internalQueryExecMaxBlockingSortBytes"
			}
		]
	},
	"EngineVersion":"4.0",
	"Engine":"mongodb"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidDBInstanceClass.NotFound|Specified DB instance class is not found.|The error message returned when the specified instance type does not exists. Verify the specified instance type.|
|403|IncorrectDBInstanceType|Current DB instance type does not support this operation.|The error message returned when the current operation is not supported by the instance type of the specified instance.|

[View error codes](https://error-center.aliyun.com/status/product/Dds)

