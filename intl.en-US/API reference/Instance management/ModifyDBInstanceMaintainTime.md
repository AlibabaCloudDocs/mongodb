# ModifyDBInstanceMaintainTime {#doc_api_Dds_ModifyDBInstanceMaintainTime .reference}

You can call this operation to modify the O&M period of a MongoDB instance.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceMaintainTime) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceMaintainTime|The operation that you want to perform. Set the value to **ModifyDBInstanceMaintainTime**.

 |
|MaintainStartTime|String|Yes|01:00Z|The start time of the instance O&M period. The format is *HH: mm*Z.

 |
|MaintainEndTime|String|Yes|02:00Z|The end time of the instance O&M period. The format is *HH: mm*Z.

 **Note:** The difference between the start time and end time must be one hour. For example, if **MaintainStartTime** is **01:00Z**, **MaintainEndTime** must be **02:00Z**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|A9310426-C763-42A2-A3AD-70A8DA204531|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=ModifyDBInstanceMaintainTime
&MaintainStartTime=01:00Z
&MaintainEndTime=02:00Z
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyDBInstanceMaintainTimeResponse> 
  <RequestId>A9310426-C763-42A2-A3AD-70A8DA204531</RequestId> 
</ModifyDBInstanceMaintainTimeResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"A9310426-C763-42A2-A3AD-70A8DA204531"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

