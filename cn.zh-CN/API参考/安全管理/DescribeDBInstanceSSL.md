# DescribeDBInstanceSSL {#doc_api_Dds_DescribeDBInstanceSSL .reference}

调用DescribeDBInstanceSSL接口查询MongoDB实例的SSL设置详情。

调用该接口时，实例必须满足以下条件：

-   实例状态为运行中。
-   实例类型为副本集实例。
-   实例的数据库版本为3.4或4.0版本。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeDBInstanceSSL&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDBInstanceSSL|要执行的操作，取值： **DescribeDBInstanceSSL**。

 |
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|RegionId|String|否|cn-hangzhou|实例所属的地域ID，您可以通过调用[DescribeDBInstanceAttribute](~~62010~~)进行查询。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|SSLExpiredTime|String|2020-03-11T02:28:25Z|SSL证书的过期时间，格式为*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|RequestId|String|36BB1BC2-789C-4BBA-A519-C5B388E4B0D4|请求ID。

 |
|SSLStatus|String|Open|SSL功能的状态。

 -   **Open**：SSL功能已开启。
-   **Closed**：SSL功能已关闭。

 |
|CertCommonName|String|dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com|SSL证书名称。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeDBInstanceSSL
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDBInstanceSSLResponse>
	  <SSLExpiredTime>2020-03-11T02:28:25Z</SSLExpiredTime>
	  <RequestId>36BB1BC2-789C-4BBA-A519-C5B388E4B0D4</RequestId>
	  <SSLStatus>Open</SSLStatus>
	  <CertCommonName>dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com</CertCommonName>
</DescribeDBInstanceSSLResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"SSLExpiredTime":"2020-03-11T02:28:25Z",
	"RequestId":"36BB1BC2-789C-4BBA-A519-C5B388E4B0D4",
	"SSLStatus":"Open",
	"CertCommonName":"dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

