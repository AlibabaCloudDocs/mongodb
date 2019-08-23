# DescribeKernelReleaseNotes {#doc_api_Dds_DescribeKernelReleaseNotes .reference}

调用DescribeKernelReleaseNotes接口查询MongoDB实例的小版本发布日志。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeKernelReleaseNotes&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DescribeKernelReleaseNotes|要执行的操作，取值： **DescribeKernelReleaseNotes**。

 |
|KernelVersion|String|否|mongodb\_20180522\_0.4.8|数据库小版本号，例如：**mongodb\_20180522\_0.4.8**。

 -   如果传入该参数，返回大于该版本的版本号列表。
-   如果不传入该参数，返回所有版本号列表。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|ReleaseNotes| | |版本发布日志信息列表。

 |
|KernelVersion|String|mongodb\_20180619\_0.4.9|版本号。

 |
|ReleaseNote|String|放开sharding某集合开关balancer的限制|发布日志。

 |
|RequestId|String|F01D4DDA-CB72-4083-B399-AF4642294FE6|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeKernelReleaseNotes
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeKernelReleaseNotesResponse>
	  <RequestId>F01D4DDA-CB72-4083-B399-AF4642294FE6</RequestId>
	  <ReleaseNotes>
		    <ReleaseNote>
			      <KernelVersion>mongodb_20180619_0.4.9</KernelVersion>
			      <ReleaseNote>放开sharding某集合开关balancer的限制</ReleaseNote>
		    </ReleaseNote>
	  </ReleaseNotes>
</DescribeKernelReleaseNotesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"F01D4DDA-CB72-4083-B399-AF4642294FE6",
	"ReleaseNotes":{
		"ReleaseNote":[
			{
				"KernelVersion":"mongodb_20180619_0.4.9",
				"ReleaseNote":"放开sharding某集合开关balancer的限制"
			}
		]
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

