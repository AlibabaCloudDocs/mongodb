# ModifyDBInstanceMaintainTime {#doc_api_Dds_ModifyDBInstanceMaintainTime .reference}

调用ModifyDBInstanceMaintainTime接口修改MongoDB实例的可维护时间。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceMaintainTime)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDBInstanceMaintainTime|要执行的操作，取值：**ModifyDBInstanceMaintainTime**。

 |
|MaintainStartTime|String|是|01:00Z|实例可运维时间段的开始时间，格式为*HH:mm*Z（UTC时间）。

 |
|MaintainEndTime|String|是|02:00Z|实例可运维时间段的结束时间，格式为*HH:mm*Z（UTC时间）。

 **说明：** 开始时间至结束时间的范围须为1小时，例如**MaintainStartTime**为**01:00Z**，则**MaintainEndTime**必须为**02:00Z**。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|RegionId|String|否|cn-hangzhou|实例所属的地域ID，您可以通过调用[DescribeDBInstanceAttribute](~~62010~~)进行查询。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|A9310426-C763-42A2-A3AD-70A8DA204531|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=ModifyDBInstanceMaintainTime
&MaintainStartTime=01:00Z
&MaintainEndTime=02:00Z
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceMaintainTimeResponse>
  <RequestId>A9310426-C763-42A2-A3AD-70A8DA204531</RequestId>
</ModifyDBInstanceMaintainTimeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"A9310426-C763-42A2-A3AD-70A8DA204531"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

