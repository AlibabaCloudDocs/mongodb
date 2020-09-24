# DescribeSecurityIps

You can call this operation to query the IP address whitelist of a MongoDB instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeSecurityIps&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeSecurityIps|The operation that you want to perform. Set the value to**DescribeSecurityIps**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the region ID of the instance. |

## Response parameters

|Prameter|Type|Sample response|Description|
|--------|----|---------------|-----------|
|SecurityIpGroups|Array| |The IP address whitelists. |
|SecurityIpGroup| | | |
|SecurityIpGroupAttribute|String|hidden|The attribute of the IP address whitelist. This value is empty by default. |
|SecurityIpGroupName|String|default|The name of the whitelist. |
|SecurityIpList|String|47.xxx.xxx.xx,100.xxx.xxx.0/24|The IP addresses in the whitelist. |
|SecurityIps|String|47.xxx.xxx.xx,100.xxx.xxx.0/24|The IP addresses in the default whitelist. |
|RequestId|String|FC724D23-2962-479E-ABB1-606C935AE7FD|The ID of the request. |

## Examples

Sample requests

```

http(s)://mongodb.aliyuncs.com/? Action=DescribeSecurityIps
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Sample success response

`XML` format

```
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

`JSON` format

```
{
    "SecurityIpGroups": {
        "SecurityIpGroup": [
            {
                "SecurityIpList": "114.xxx.xxx.xx",
                "SecurityIpGroupAttribute": "",
                "SecurityIpGroupName": "allowserver"
            },
            {
                "SecurityIpList": "47.xxx.xxx.xx,100.xxx.xxx.0/24",
                "SecurityIpGroupAttribute": "",
                "SecurityIpGroupName": "default"
            }
        ]
    },
    "SecurityIps": "47.xxx.xxx.xx,100.xxx.xxx.0/24",
    "RequestId": "FC724D23-2962-479E-ABB1-606C935AE7FD"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

