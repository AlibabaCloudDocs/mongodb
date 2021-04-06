# DescribeDBInstanceMonitor

调用DescribeDBInstanceMonitor接口查询MongoDB实例的监控采集粒度。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeDBInstanceMonitor&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDBInstanceMonitor|要执行的操作，取值：**DescribeDBInstanceMonitor**。 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。 |
|RegionId|String|否|cn-hangzhou|地域ID，您可以调用[DescribeRegions](~~61933~~)查询。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Granularity|String|1|监控采集粒度。返回值为**1**或**300**，单位为秒。 |
|RequestId|String|EFD65226-08CC-4C4D-B6A4-CB3C382F67B0|请求ID。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=DescribeDBInstanceMonitor
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeDBInstanceMonitorResponse>
	  <Granularity>1</Granularity>
	  <RequestId>EFD65226-08CC-4C4D-B6A4-CB3C382F67B0</RequestId>
</DescribeDBInstanceMonitorResponse>
```

`JSON` 格式

```
{
	"Granularity": 1,
	"RequestId": "EFD65226-08CC-4C4D-B6A4-CB3C382F67B0"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

