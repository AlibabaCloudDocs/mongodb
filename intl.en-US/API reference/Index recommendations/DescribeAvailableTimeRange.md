# DescribeAvailableTimeRange {#doc_api_Dds_DescribeAvailableTimeRange .reference}

You can call this operation to query the analysis period and generation status of the index analysis report on an ApsaraDB for MongoDB instance.

Ensure that the instance meets the following conditions when you call this operation:

-   The region of the instance is China \(Hangzhou\), China \(Shanghai\), China \(Shenzhen\), China \(Qingdao\), or China \(Beijing\).
-   The instance type is replica set or sharded cluster.
-   The log audit function must be enabled for the instance.

**Note:** You can call the [CreateRecommendationTask](~~95527~~) operation to create an online task to analyze the indexes that were generated at any time within seven days \(accurate to the hour\). After the analysis is completed, the results are automatically converted to queriable data.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeAvailableTimeRange) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAvailableTimeRange|The operation that you want to perform. Set the value to **DescribeAvailableTimeRange**.

 |
|InstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 **Note:** If you specify this parameter to the ID of a sharded cluster instance, you must also specify the **NodeId** parameter.

 |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the shard in the specified sharded cluster instance.

 **Note:** This parameter is only valid when you specify the **DBInstanceId** parameter to the ID of a sharded cluster instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|TimeRange| | |The time range in which the generation status of the index report is queried.

 |
|└EndTime|String|2019-03-12T16Z|The end of the time range that you want to query. The time is in the *yyyy-MM-dd*T*HH*Z format.

 |
|└NodeId|String|d-bpxxxxxxxx|The ID of the shard in the specified sharded cluster instance.

 **Note:** This parameter is returned when the instance type is sharded cluster.

 |
|└StartTime|String|2019-03-11T16Z|The beginning of the time range that you want to query. The time is in the *yyyy-MM-dd*T*HH*Z format.

 |
|└Status|String|Success|The generation status of the index recommendation report.

 -   **Success**
-   **Creating**
-   **Failure**

 |
|└TaskId|String|3223xxxx|The ID of the task.

 |
|RequestId|String|5C344679-EDD7-4BC1-964B-DDE01C507BE5|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeAvailableTimeRange
&InstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeAvailableTimeRangeResponse>
  <TimeRange>
    <TimeRange>
      <Status>Success</Status>
      <EndTime>2019-03-12T16Z</EndTime>
      <TaskId>3223xxxx</TaskId>
      <StartTime>2019-03-11T16Z</StartTime>
    </TimeRange>
  </TimeRange>
  <RequestId>5C344679-EDD7-4BC1-964B-DDE01C507BE5</RequestId>
</DescribeAvailableTimeRangeResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"TimeRange":{
		"TimeRange":[
			{
				"Status":"Success",
				"EndTime":"2019-03-12T16Z",
				"StartTime":"2019-03-11T16Z",
				"TaskId":"3223xxxx"
			}
		]
	},
	"RequestId":"5C344679-EDD7-4BC1-964B-DDE01C507BE5"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

