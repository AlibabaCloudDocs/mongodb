# ModifySecurityIps

You can call this operation to modify the IP address whitelist of an ApsaraDB for MongoDB instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=ModifySecurityIps&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifySecurityIps|The operation that you want to perform. Set the value to **ModifySecurityIps**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of an instance. |
|SecurityIps|String|Yes|10.23.12.24/24,10.22.22.22|The IP addresses in an IP address whitelist. Separate multiple IP addresses with commas \(,\). You can add a maximum of 1,000 different IP addresses to a whitelist. You can add IP addresses in one of the following two formats:

 -   IP addresses. Example: 10.23.12.24.
-   Classless Inter-Domain Routing \(CIDR\) blocks, such as 10.23.12.24/24, where 24 indicates that the prefix of the CIDR block is 24-bit long. You can replace 24 with a value within the range of 1 to 32. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |
|ModifyMode|String|No|Append|The method of modification. Valid values:

 -   **Cover**: overwrites the whitelist.
-   **Append**: appends data to the whitelist.
-   **Delete**: deletes the whitelist.

 The default value is **Cover**. |
|SecurityIpGroupName|String|No|allowserver|The name of the IP address whitelist to be modified. The default value is **default**. |
|SecurityIpGroupAttribute|String|No|test|The attributes of an IP address whitelist. It can contain a maximum of 120 characters in length and can contain uppercase letters, lowercase letters, and digits.

 This parameter is empty by default. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|61B05CCF-EBAB-4BF3-BA67-D77256A721E2|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=ModifySecurityIps
&SecurityIps=10.23.12.24/24,10.22.22.22
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifySecurityIpsResponse>
	  <RequestId>61B05CCF-EBAB-4BF3-BA67-D77256A721E2</RequestId>
</ModifySecurityIpsResponse>
```

`JSON` format

```
{
	"RequestId": "61B05CCF-EBAB-4BF3-BA67-D77256A721E2"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

