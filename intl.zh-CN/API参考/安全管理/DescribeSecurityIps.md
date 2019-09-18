# DescribeSecurityIps {#doc_api_Dds_DescribeSecurityIps .reference}

调用DescribeSecurityIps接口查询MongoDB实例的IP白名单。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Dds&api=DescribeSecurityIps&type=RPC&version=2015-12-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DBInstanceId|String|是|dds-bpxxxxxxxx|实例ID。

 |
|Action|String|否|DescribeSecurityIps|要执行的操作，取值：**DescribeSecurityIps**。

 |
|AccessKeyId|String|否|LTAIgbTGpxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|SecurityIpGroups| | |IP白名单分组列表。

 |
|SecurityIpGroupAttribute|String|hidden|IP白名单分组属性，默认为空。

 |
|SecurityIpGroupName|String|default|分组名。

 |
|SecurityIpList|String|47.xxx.xxx.xx,100.xxx.xxx.0/24|分组中包含的IP白名单列表。

 |
|SecurityIps|String|47.xxx.xxx.xx,100.xxx.xxx.0/24|默认分组中包含的IP白名单。

 |
|RequestId|String|FC724D23-2962-479E-ABB1-606C935AE7FD|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/?Action=DescribeSecurityIps
&DBInstanceId=dds-bpxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeSecurityIpsResponse>
	  <SecurityIpGroups>
		    <SecurityIpGroup>
			      <SecurityIpList>114.xxx.xxx.xx</SecurityIpList>
			      <SecurityIpGroupAttribute></SecurityIpGroupAttribute>
			      <SecurityIpGroupName>allowserver</SecurityIpGroupName>
		    </SecurityIpGroup>
		    <SecurityIpGroup>
			      <SecurityIpList>47.xxx.xxx.xx,100.xxx.xxx.0/24</SecurityIpList>
			      <SecurityIpGroupAttribute></SecurityIpGroupAttribute>
			      <SecurityIpGroupName>default</SecurityIpGroupName>
		    </SecurityIpGroup>
	  </SecurityIpGroups>
	  <SecurityIps>47.xxx.xxx.xx,100.xxx.xxx.0/24</SecurityIps>
	  <RequestId>FC724D23-2962-479E-ABB1-606C935AE7FD</RequestId>
</DescribeSecurityIpsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"SecurityIpGroups":{
		"SecurityIpGroup":[
			{
				"SecurityIpList":"114.xxx.xxx.xx",
				"SecurityIpGroupAttribute":"",
				"SecurityIpGroupName":"allowserver"
			},
			{
				"SecurityIpList":"47.xxx.xxx.xx,100.xxx.xxx.0/24",
				"SecurityIpGroupAttribute":"",
				"SecurityIpGroupName":"default"
			}
		]
	},
	"SecurityIps":"47.xxx.xxx.xx,100.xxx.xxx.0/24",
	"RequestId":"FC724D23-2962-479E-ABB1-606C935AE7FD"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Dds)查看更多错误码。

