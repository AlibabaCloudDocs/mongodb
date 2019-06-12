# DescribeSecurityIps {#doc_api_Dds_DescribeSecurityIps .reference}

You can call this operation to query the IP address whitelist of a MongoDB instance.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeSecurityIps) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeSecurityIps|The operation that you want to perform. Set the value to **DescribeSecurityIps**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|SecurityIpGroups| | |The IP address whitelists.

 |
|└SecurityIpGroupAttribute|String|hidden|The attribute of the IP address whitelist. This value is empty by default.

 |
|└SecurityIpGroupName|String|default|The name of the whitelist.

 |
|└SecurityIpList|String|47.xxx.xxx.xx,100.xxx.xxx. 0/24|The IP addresses in the whitelist.

 |
|SecurityIps|String|47.xxx.xxx.xx,100.xxx.xxx. 0/24|The IP addresses in the default whitelist.

 |
|RequestId|String|FC724D23-2962-479E-ABB1-606C935AE7FD|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeSecurityIps
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeSecurityIpsResponse>
  <SecurityIpGroups>
    <SecurityIpGroup>
      <SecurityIpList>114.xxx.xxx.xx</SecurityIpList>
      <SecurityIpGroupAttribute/>
      <SecurityIpGroupName>allowserver</SecurityIpGroupName>
    </SecurityIpGroup>
    <SecurityIpGroup>
      <SecurityIpList>47.xxx.xxx.xx,100.xxx.xxx. 0/24</SecurityIpList>
      <SecurityIpGroupAttribute/>
      <SecurityIpGroupName>default</SecurityIpGroupName>
    </SecurityIpGroup>
  </SecurityIpGroups>
  <SecurityIps>47.xxx.xxx.xx,100.xxx.xxx. 0/24</SecurityIps>
  <RequestId>FC724D23-2962-479E-ABB1-606C935AE7FD</RequestId>
</DescribeSecurityIpsResponse>

```

`JSON` format

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
				"SecurityIpList":"47.xxx.xxx.xx,100.xxx.xxx. 0/24",
				"SecurityIpGroupAttribute":"",
				"SecurityIpGroupName":"default"
			}
		]
	},
	"SecurityIps":"47.xxx.xxx.xx,100.xxx.xxx. 0/24",
	"RequestId":"FC724D23-2962-479E-ABB1-606C935AE7FD"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

