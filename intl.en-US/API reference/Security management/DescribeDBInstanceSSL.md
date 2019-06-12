# DescribeDBInstanceSSL {#doc_api_Dds_DescribeDBInstanceSSL .reference}

You can call this operation to query the SSL settings of a MongoDB instance.

Ensure that the instance meets the following conditions when you call this operation:

-   The instance is in the running state.
-   The instance type is replica set.
-   The database version of the instance is 3.4 or 4.0.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeDBInstanceSSL) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDBInstanceSSL|The operation that you want to perform. Set the value to **DescribeDBInstanceSSL**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|SSLExpiredTime|String|2020-03-11T02:28:25Z|The expiration time of the SSL certificate. The time is in the *yyyy-MM-dd*T*HH:mm:ss*Z format.

 |
|RequestId|String|36BB1BC2-789C-4BBA-A519-C5B388E4B0D4|The ID of the request.

 |
|SSLStatus|String|Open|The status of the SSL function.

 -   **Open**
-   **Closed**

 |
|CertCommonName|String|dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com|The name of the SSL certificate.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeDBInstanceSSL
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeDBInstanceSSLResponse>
  <SSLExpiredTime>2020-03-11T02:28:25Z</SSLExpiredTime>
  <RequestId>36BB1BC2-789C-4BBA-A519-C5B388E4B0D4</RequestId>
  <SSLStatus>Open</SSLStatus>
  <CertCommonName>dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com</CertCommonName>
</DescribeDBInstanceSSLResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"SSLExpiredTime":"2020-03-11T02:28:25Z",
	"RequestId":"36BB1BC2-789C-4BBA-A519-C5B388E4B0D4",
	"SSLStatus":"Open",
	"CertCommonName":"dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

