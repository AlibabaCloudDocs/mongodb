# DescribeMongoDBLogConfig

调用DescribeMongoDBLogConfig查看MongoDB日志服务的配置。

该接口基于新版MongoDB日志服务，更多信息请参见[开通新版审计日志](~~164542~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeMongoDBLogConfig&type=RPC&version=2015-12-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeMongoDBLogConfig|要执行的操作。取值：**DescribeMongoDBLogConfig**。 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。您可以通过调用[DescribeDBInstances](~~61939~~)进行查询。 |
|RegionId|String|否|cn-hangzhou|实例所属的地域ID。您可以通过调用[DescribeDBInstanceAttribute](~~62010~~)进行查询。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|IsEtlMetaExist|Integer|1|是否已创建将日志分发到Logtail的规则，有关Logtail的详细信息，请参见[Logtail简介](~~28979~~)。取值：

 -   1：已创建
-   0或null：未创建 |
|IsUserProjectLogstoreExist|Integer|1|当前地域中是否存在日志服务project。取值：

 -   1：存在
-   0或null：不存在 |
|RequestId|String|664ECE26-658A-47C5-88F6-870B0132E8D2|请求ID。 |
|UserProjectName|String|nosql-140xxxxxxxxxxxxx-cn-hangzhou|日志服务project的名称。 |

## 示例

请求示例

```
http(s)://mongodb.aliyuncs.com/?Action=DescribeMongoDBLogConfig
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<UserProjectName>nosql-140xxxxxxxxxxxxx-cn-hangzhou</UserProjectName>
<RequestId>FECF2277-3EA1-4CD9-AEB9-E7DED5E84E35</RequestId>
<IsUserProjectLogstoreExist>1</IsUserProjectLogstoreExist>
<IsEtlMetaExist>1</IsEtlMetaExist>
```

`JSON` 格式

```
{
	"UserProjectName": "nosql-140xxxxxxxxxxxxx-cn-hangzhou",
	"RequestId": "FECF2277-3EA1-4CD9-AEB9-E7DED5E84E35",
	"IsUserProjectLogstoreExist": 1,
	"IsEtlMetaExist": 1
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

