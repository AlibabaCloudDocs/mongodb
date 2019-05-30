# DescribeDBInstancePerformance {#doc_api_Dds_DescribeDBInstancePerformance .reference}

调用DescribeDBInstancePerformance接口查询MongoDB实例性能数据。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Dds&api=DescribeDBInstancePerformance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDBInstancePerformance|要执行的操作，取值：**DescribeDBInstancePerformance**。

 |
|Key|String|是|MongoDB\_DetailedSpaceUsage|性能指标，取值详情请参见[性能参数表](~~64048~~)。

 **说明：** 如需传入多个指标使用英文逗号（,）分隔。

 |
|StartTime|String|是|2019-03-11T12:30Z|查询开始时间，格式为*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。

 |
|EndTime|String|是|2019-03-11T12:30Z|查询结束时间，必须晚于查询开始时间，格式为*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 **说明：** 当本参数传入的是分片集群实例ID时，还需要传入**NodeId**参数。

 |
|NodeId|String|否|d-bpxxxxxxxx|分片集群实例中Mongos节点ID或Shard节点ID，可用于查询单个节点的性能情况。

 **说明：** 当**DBInstanceId**参数传入的是分片集群实例ID时，本参数才可用。

 |
|RoleId|String|否|60xxxxx|实例的节点角色ID，可通过[DescribeReplicaSetRole](~~62134~~)接口查询。

 **说明：** 当**DBInstanceId**参数传入的是单节点实例ID或副本集实例ID时，本参数才可用。

 |
|ReplicaSetRole|String|否|Primary|副本集实例的节点角色，取值：

 -   Primary：主节点。
-   Secondary：从节点。

 **说明：** 当**DBInstanceId**参数传入的是单节点实例ID或副本集实例ID时，本参数才可用。

 |
|RegionId|String|否|cn-hangzhou|实例所属的地域ID，您可以通过调用[DescribeDBInstanceAttribute](~~62010~~)进行查询。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|267F98DC-367D-4F20-B137-8B5B664D1C5D|请求ID。

 |
|StartTime|String|2019-03-11T12:20Z|查询开始时间，格式为*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。

 |
|EndTime|String|2019-03-11T12:30Z|查询结束时间，格式为*yyyy-MM-dd*T*HH:mm*Z（UTC时间）。

 |
|PerformanceKeys| | |性能指标信息列表。

 |
|└Key|String|MongoDB\_DetailedSpaceUsage|性能指标。

 |
|└PerformanceValues| | |性能指标值列表。

 |
|└Date|String|2019-03-11T12:21:51Z|性能指标值产生的日期。

 |
|└Value|String|0.6|性能指标值。

 |
|└Unit|String|MB|展示单位。

 |
|└ValueFormat|String|cpu\_usage|性能指标值的格式。如果该性能指标包含多个字段，通常以**&**分隔。

 例如查询磁盘空间使用量，返回的ValueFormat即为**ins\_size&data\_size&log\_size**。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeDBInstancePerformance
&Key=MongoDB_DetailedSpaceUsage
&StartTime=2019-03-11T12:30Z
&EndTime=2019-03-11T12:30Z
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Dds)

