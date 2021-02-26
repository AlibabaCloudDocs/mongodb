# ModifyDBInstanceMonitor

调用ModifyDBInstanceMonitor接口设置MongoDB实例的监控采集粒度。

**由于监控采集粒度调整功能下线，本接口暂不可用。**

调用本接口时，实例必须满足以下条件：

-   实例为副本集实例或分片集群实例。
-   实例的版本为3.4（最新的小版本）或4.0。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=ModifyDBInstanceMonitor&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDBInstanceMonitor|要执行的操作，取值：**ModifyDBInstanceMonitor**。 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。 |
|Granularity|String|是|1|设置监控采集粒度，取值：**1**或**300**，单位为秒。 |
|RegionId|String|否|cn-hangzhou|地域ID，您可以调用[DescribeRegions](~~61933~~)查询。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|EFD65226-08CC-4C4D-B6A4-CB3C382F67B0|请求ID。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=ModifyDBInstanceMonitor
&DBInstanceId=dds-bpxxxxxxxx
&Granularity=1
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifyDBInstanceMonitorResponse>
	  <RequestId>EFD65226-08CC-4C4D-B6A4-CB3C382F67B0</RequestId>
</ModifyDBInstanceMonitorResponse>
```

`JSON`格式

```
{
	"RequestId": "EFD65226-08CC-4C4D-B6A4-CB3C382F67B0"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

