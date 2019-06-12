# CreateRecommendationTask {#doc_api_Dds_CreateRecommendationTask .reference}

You can call this operation to create index analysis tasks for an AsparaDB for MongoDB instance.

Ensure that the instance meets the following conditions when you call this operation:

-   The region of the instance is China \(Hangzhou\), China \(Shanghai\), China \(Shenzhen\), China \(Qingdao\), or China \(Beijing\).
-   The instance type is replica set or sharded cluster.
-   The log audit function is enabled for the instance.

**Note:** 

 

-   After calling this operation to create index analysis tasks, you can call the [DescribeAvailableTimeRange](~~95534~~) operation to query corresponding tasks and their statuses.

-   This API can be called up to 10 times each day.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=CreateRecommendationTask) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateRecommendationTask|The operation that you want to perform. Set the value to **CreateRecommendationTask**.

 |
|StartTime|String|Yes|2019-01-01T12Z|The beginning of the time range that you want to query. The time is in the *yyyy-MM-dd*T*HH*Z format.

 **Note:** The value of **StartTime** must be later than the time when the log audit function was enabled.

 |
|EndTime|String|Yes|2019-01-01T18Z|The end of the time range that you want to query. The value of EndTime must be later than the value of StartTime. The time is in the *yyyy-MM-dd*T*HH*Z format.

 **Note:** The maximum time range is 7 days.

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
|RequestId|String|009D2572-6839-43C0-8D89-44DB46CBA2EA|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=CreateRecommendationTask
&StartTime=2019-01-01T12Z
&EndTime=2019-01-01T18Z
&InstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CreateRecommendationTaskResponse>
  <RequestId>009D2572-6839-43C0-8D89-44DB46CBA2EA</RequestId>
</CreateRecommendationTaskResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"009D2572-6839-43C0-8D89-44DB46CBA2EA"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidEndTime.Format|Specified end time is not valid.|The error message returned when the end time is invalid. Check the format of the specified time.|

[View error codes](https://error-center.aliyun.com/status/product/Dds)

