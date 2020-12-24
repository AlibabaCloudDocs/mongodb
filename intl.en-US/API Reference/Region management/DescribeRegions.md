# DescribeRegions

You can call this operation to view the available regions and zones of ApsaraDB for MongoDB instances.

To query available regions and zones where ApsaraDB for MongoDB instances can be created, call the [DescribeAvailableResource](~~149719~~) operation.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeRegions&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeRegions|The operation that you want to perform. Set the value to **DescribeRegions**. |
|RegionId|String|No|cn-hangzhou|The ID of the region. If you do not specify this parameter, the IDs of all supported regions are returned. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Regions|Array of DdsRegion| |Details about the regions. |
|DdsRegion| | | |
|RegionId|String|cn-qingdao|The ID of the region.

 **Note:** For more information about region names and IDs, see [Regions and zones](~~40654~~). |
|Zones|Array of Zone| |Details about the zones. |
|Zone| | | |
|VpcEnabled|Boolean|true|Indicates whether VPC is supported. |
|ZoneName|String|Hangzhou Zone H|The name of the zone. |
|RequestId|String|4E46C22C-D3B7-4DB8-9C76-63851BE68E20|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeRegions
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RequestId>4E46C22C-D3B7-4DB8-9C76-63851BE68E20</RequestId>
<Regions>
    <DdsRegion>
        <RegionId>cn-qingdao</RegionId>
    </DdsRegion>
    <DdsRegion>
        <Zones>
            <Zone>
                <ZoneName>Hangzhou Zone H</ZoneName>
                <VpcEnabled>true</VpcEnabled>
            </Zone>
        </Zones>
    </DdsRegion>
</Regions>
```

`JSON` format

```
{
	"RequestId":"4E46C22C-D3B7-4DB8-9C76-63851BE68E20",
	"Regions":{
		"DdsRegion":[
			{
				"RegionId":"cn-qingdao"
			},
			{
				"Zones":{
					"Zone":[
						{
							"ZoneName":"Hangzhou Zone H",
							"VpcEnabled":"true"
						}
					]
				}
			}
		]
	}
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

