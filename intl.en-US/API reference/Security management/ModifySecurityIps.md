# ModifySecurityIps {#doc_api_Dds_ModifySecurityIps .reference}

You can call this operation to modify the IP address whitelist of the MongoDB instance.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=ModifySecurityIps) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifySecurityIps|The operation that you want to perform. Set the value to **ModifySecurityIps**.

 |
|SecurityIps|String|Yes|10.23.12.24/24,10.22.22.22|The IP addresses in an IP address whitelist. Separate multiple IP addresses with commas \(,\). You can add a maximum of 1,000 different IP addresses to a whitelist. You can add IP addresses in the following formats:

 -   Standard IP address format, such as 10.23.12.24.
-   Classless Inter-Domain Routing \(CIDR\) blocks, such as 10.23.12.24/24, where 24 indicates the prefix of the CIDR block is 24-bit. You can replace 24 with a value ranging from 1 to 32.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|ModifyMode|String|No|Append|The method of modification. Valid values:

 -   **Cover**: overwrites the whitelist.
-   **Append**: appends data to the whitelist.
-   **Delete**: deletes the whitelist.

 The default value is **Cover**.

 |
|SecurityIpGroupName|String|No|allowserver|The name of the IP address whitelist to be modified. The default value is **default**.

 |
|SecurityIpGroupAttribute|String|No|test|The attributes of an IP address whitelist. It can contain a maximum of 120 characters in length and can contain uppercase letters, lowercase letters, and digits.

 This value is empty by default.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|61B05CCF-EBAB-4BF3-BA67-D77256A721E2|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=ModifySecurityIps
&SecurityIps=10.23.12.24/24,10.22.22.22 
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifySecurityIpsResponse>
  <RequestId>61B05CCF-EBAB-4BF3-BA67-D77256A721E2</RequestId>
</ModifySecurityIpsResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"61B05CCF-EBAB-4BF3-BA67-D77256A721E2"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

