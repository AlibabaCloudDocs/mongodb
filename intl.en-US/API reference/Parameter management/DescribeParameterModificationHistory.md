# DescribeParameterModificationHistory {#doc_api_Dds_DescribeParameterModificationHistory .reference}

You can call this operation to query the modification records of MongoDB instance parameters.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeParameterModificationHistory) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeParameterModificationHistory|The operation that you want to perform. Set the value to **DescribeParameterModificationHistroy**.

 |
|StartTime|String|Yes|2019-01-01T12:10Z|The beginning of the time range that you want to query. The time is in the *yyyy-MM-dd*T*HH:mm*Z format.

 |
|EndTime|String|Yes|2019-01-02T12:10Z|The end of the time range that you want to query. The time is in the *yyyy-MM-dd*T*HH:mm*Z format.

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
|HistoricalParameters| | |A list of parameter modification records.

 |
|└ModifyTime|String|2019-03-12T07:58:24Z|The time when the parameter was modified. The time is in the *yyyy-MM-dd*T*HH:mm:ss*Z format.

 |
|└NewParameterValue|String|200|The parameter value after modification.

 |
|└OldParameterValue|String|100|The parameter value before modification.

 |
|└ParameterName|String|operationProfiling.slowOpThresholdMs|The name of the modified parameter.

 |
|RequestId|String|B1BB6E0E-B4EF-4145-81FA-A07719860248|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeParameterModificationHistory
&StartTime=2019-01-01T12:10Z
&EndTime=2019-01-02T12:10Z
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeParameterModificationHistoryResponse>
  <HistoricalParameters>
    <HistoricalParameter>
      <OldParameterValue>100</OldParameterValue>
      <ModifyTime>2019-03-12T07:58:24Z</ModifyTime>
      <NewParameterValue>200</NewParameterValue>
      <ParameterName>operationProfiling.slowOpThresholdMs</ParameterName>
    </HistoricalParameter>
  </HistoricalParameters>
  <RequestId>B1BB6E0E-B4EF-4145-81FA-A07719860248</RequestId>
</DescribeParameterModificationHistoryResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"HistoricalParameters":{
		"HistoricalParameter":[
			{
				"OldParameterValue":"100",
				"ModifyTime":"2019-03-12T07:58:24Z",
				"NewParameterValue":"200",
				"ParameterName":"operationProfiling.slowOpThresholdMs"
			}
		]
	},
	"RequestId":"B1BB6E0E-B4EF-4145-81FA-A07719860248"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

