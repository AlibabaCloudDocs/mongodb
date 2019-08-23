# DestroyInstance {#doc_api_Dds_DestroyInstance .reference}

调用DestroyInstance接口销毁MongoDB实例。

调用本接口时，实例必须满足以下条件：

-   实例的付费类型为包年包月。
-   实例到期，且状态处于**锁定中**。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DestroyInstance&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DestroyInstance|要执行的操作，取值：**DestroyInstance**。

 |
|InstanceId|String|否|dds-bpxxxxxxxx|实例ID。

 **说明：** **InstanceId**参数与**DBInstanceId**参数作用相同，只需选择一个传入即可。

 |
|DBInstanceId|String|否|dds-bpxxxxxxxx|实例ID。

 **说明：** **InstanceId**参数与**DBInstanceId**参数作用相同，只需选择一个传入即可。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DestroyInstance
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DestroyInstanceResponse>
	  <RequestId>65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
</DestroyInstanceResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Dds)查看更多错误码。

