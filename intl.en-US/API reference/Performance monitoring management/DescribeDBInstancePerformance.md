# DescribeDBInstancePerformance {#doc_api_Dds_DescribeDBInstancePerformance .reference}

You can call this operation to query the performance data of a MongoDB instance.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeDBInstancePerformance) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDBInstancePerformance|The operation that you want to perform. Set the value to **DescribeDBInstancePerformance**.

 |
|Key|String|Yes|MongoDB\_DetailedSpaceUsage|The performance indicator. For more information about valid values, see [Performance parameters](~~64048~~).

 **Note:** Separate multiple indicators with commas \(,\).

 |
|StartTime|String|Yes|2019-03-11T12:30Z|The beginning of the time range that you want to query. The time is in the *yyyy-MM-dd*T*HH:mm*Z format.

 |
|EndTime|String|Yes|2019-03-11T12:30Z|The end of the time range that you want to query. The time is in the *yyyy-MM-dd*T*HH:mm*Z format.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** If you specify this parameter to the ID of a sharded cluster instance, you must also specify the **NodeId** parameter.

 |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the mongos or shard in a sharded cluster instance. You can specify this parameter to query the performance of a single node.

 **Note:** This parameter is only valid when you specify the **DBInstanceId** parameter to the ID of a sharded cluster instance.

 |
|RoleId|String|No|60xxxxx|The role ID of a node in a instance. You can call [DescribeReplicaSetRole](~~62134~~) to query role IDs.

 **Note:** This parameter is only valid when you specify the **DBInstanceId** parameter to the ID of a standalone instance or a replica set instance.

 |
|ReplicaSetRole|String|No|Primary|The role of a node in a replica set instance. Valid values:

 -   Primary
-   Secondary

 **Note:** This parameter is only valid when you specify the **DBInstanceId** parameter to the ID of a standalone instance or a replica set instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|267F98DC-367D-4F20-B137-8B5B664D1C5D|The ID of the request.

 |
|StartTime|String|2019-03-11T12:20Z|The beginning of the time range that you want to query. The time is in the *yyyy-MM-dd*T*HH:mm*Z format.

 |
|EndTime|String|2019-03-11T12:30Z|The end of the time range that you want to query. The time is in the *yyyy-MM-dd*T*HH:mm*Z format.

 |
|PerformanceKeys| | |A list of performance indicator information.

 |
|└Key|String|MongoDB\_DetailedSpaceUsage|Performance indicator.

 |
|└PerformanceValues| | |A list of values of performance indicators.

 |
|└Date|String|2019-03-11T12:21:51Z|The date and time when the value is generated.

 |
|└Value|String|0.6|The value of a performance indicator.

 |
|└Unit|String|MB|The unit of the indicator value.

 |
|└ValueFormat|String|cpu\_usage|The format of the performance indicator value. If the performance indicator contains multiple fields, the fields are separated with ampersands \(**&**\).

 For example, if you query disk space usage, the returned ValueFormat is **ins\_size&data\_size&log\_size**.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeDBInstancePerformance
&Key=MongoDB_DetailedSpaceUsage
&StartTime=2019-03-11T12:30Z
&EndTime=2019-03-11T12:30Z
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeDBInstancePerformanceResponse>
  <RequestId>267F98DC-367D-4F20-B137-8B5B664D1C5D</RequestId>
  <PerformanceKeys>
    <PerformanceKey>
      <Key>MongoDB_DetailedSpaceUsage</Key>
      <PerformanceValues>
        <PerformanceValue>
          <Value>1768&amp;1282&amp;486</Value>
          <Date>2019-03-11T12:21:51Z</Date>
        </PerformanceValue>
        <PerformanceValue>
          <Value>1768&amp;1282&amp;486</Value>
          <Date>2019-03-11T12:26:52Z</Date>
        </PerformanceValue>
      </PerformanceValues>
      <Unit>MB</Unit>
      <ValueFormat>ins_size&amp;data_size&amp;log_size</ValueFormat>
    </PerformanceKey>
  </PerformanceKeys>
  <EndTime>2019-03-11T12:30Z</EndTime>
  <StartTime>2019-03-11T12:20Z</StartTime>
</DescribeDBInstancePerformanceResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"267F98DC-367D-4F20-B137-8B5B664D1C5D",
	"PerformanceKeys":{
		"PerformanceKey":[
			{
				"Key":"MongoDB_DetailedSpaceUsage",
				"PerformanceValues":{
					"PerformanceValue":[
						{
							"Value":"1768&1282&486",
							"Date":"2019-03-11T12:21:51Z"
						},
						{
							"Value":"1768&1282&486",
							"Date":"2019-03-11T12:26:52Z"
						}
					]
				},
				"Unit":"MB",
				"ValueFormat":"ins_size&data_size&log_size"
			}
		]
	},
	"EndTime":"2019-03-11T12:30Z",
	"StartTime":"2019-03-11T12:20Z"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

