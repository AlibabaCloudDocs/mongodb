# DescribeRegions {#doc_api_Dds_DescribeRegions .reference}

You can call this operation to view the available regions and zones of a MongoDB instance.

Before calling [CreateDBInstance](~~61763~~) or [CreateShardingDBInstance](~~61884~~) to create an instance, you must call this operation to query the available regions and zones.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeRegions) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeRegions|The operation that you want to perform. Set the value to **DescribeRegions**.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Regions| | |The list of regions.

 |
|└RegionId|String|cn-qingdao|The ID of the region.

 **Note:** For more information about region names and IDs, see [Region and zone](~~40654~~).

 |
|└Zones| | |The list of zones.

 |
|└VpcEnabled|Boolean|true|Indicates whether VPC is supported.

 |
|└ZoneId|String|cn-hangzhou-b|The ID of the zone.

 |
|RequestId|String|4E46C22C-D3B7-4DB8-9C76-63851BE68E20|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeRegions
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeRegionsResponse>
  <RequestId>4E46C22C-D3B7-4DB8-9C76-63851BE68E20</RequestId> 
  <Regions> 
    <DdsRegion> 
      <RegionId>cn-hangzhou</RegionId> 
      <Zones> 
        <Zone>
          <VpcEnabled>true</VpcEnabled>
          <ZoneId>cn-hangzhou-e</ZoneId>
        </Zone>
        <Zone>
          <VpcEnabled>true</VpcEnabled>
          <ZoneId>cn-hangzhou-b</ZoneId>
        </Zone>
        <Zone>
          <VpcEnabled>true</VpcEnabled>
          <ZoneId>cn-hangzhou-d</ZoneId>
        </Zone>
        <Zone>
          <VpcEnabled>true</VpcEnabled>
          <ZoneId>cn-hangzhou-f</ZoneId>
        </Zone>
        <Zone>
          <VpcEnabled>true</VpcEnabled>
          <ZoneId>cn-hangzhou-MAZ5(b,e,f)</ZoneId>
        </Zone>
        <Zone>
          <VpcEnabled>true</VpcEnabled>
          <ZoneId>cn-hangzhou-g</ZoneId>
        </Zone>
      </Zones> 
    </DdsRegion>
  </Regions> 
</DescribeRegionsResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"4E46C22C-D3B7-4DB8-9C76-63851BE68E20",
	"Regions":{
		"DdsRegion":[
			{
				"RegionId":"cn-hangzhou",
				"Zones":{
					"Zone":[
						{
							"VpcEnabled":true,
							"ZoneId":"cn-hangzhou-i"
						},
						{
							"VpcEnabled":true,
							"ZoneId":"cn-hangzhou-b"
						},
						{
							"VpcEnabled":true,
							"ZoneId":"cn-hangzhou-d"
						},
						{
							"VpcEnabled":true,
							"ZoneId":"cn-hangzhou-f"
						},
						{
							"VpcEnabled":true,
							"ZoneId":"cn-hangzhou-MAZ5(b,e,f)"
						},
						{
							"VpcEnabled":true,
							"ZoneId":"cn-hangzhou-g"
						}
					]
				}
			}
		]
	}
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

