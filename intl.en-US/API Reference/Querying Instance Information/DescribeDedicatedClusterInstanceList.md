# DescribeDedicatedClusterInstanceList

You can call this operation to query instances in dedicated clusters.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeDedicatedClusterInstanceList&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDedicatedClusterInstanceList|The operation that you want to perform. Set the value to **DescribeDedicatedClusterInstanceList**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~61933~~) operation to query the most recent region list. |
|ZoneId|String|No|cn-hangzhou-h|The ID of the zone. You can call [DescribeZones](~~61933~~) to query the zone ID. |
|InstanceId|String|No|dds-t4n\*\*\*\*\*\*\*\*\*\*|The ID of the ApsaraDB for MongoDB instance.

 **Note:** Separate multiple IDs with commas \(,\). |
|InstanceStatus|String|No|1|The status of the instance. For information about the valid values of this parameter, see [Valid values of the InstanceStatus parameter for DescribeDedicatedClusterInstanceList](~~190071~~). |
|InstanceNetType|String|No|1|The network type of the instance. Valid values:

 -   0: The instance is connected over the Internet.
-   1: The instance is connected over an internal network.
-   2. The instance is deployed in a VPC.

 Default value: 1. |
|Engine|String|No|MongoDB|The database engine. Set the value to MongoDB. |
|EngineVersion|String|No|4.2|The version number of the database engine. Set the value to **4.2**. |
|ClusterId|String|No|dhg-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|The ID of the dedicated cluster to which the instance belongs.

 **Note:** Separate multiple IDs with commas \(,\). |
|DedicatedHostName|String|No|ch-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|The name of the dedicated host.

 **Note:** Separate multiple names with commas \(,\). |
|PageNumber|Integer|No|1|The number of the page to return. Valid values: any non-zero positive integer. Default value: **1**. |
|PageSize|Integer|No|30|The number of entries to return on each page. Valid values: **30**, **50**, and **100**. Default value: **30**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Instances|Array of dbInstance| |Details about the instances. |
|dbInstance| | | |
|CharacterType|String|normal|The type of the ApsaraDB for MongoDB instance. Valid value: **normal**.

 **normal**: a replica set instance. |
|ClusterId|String|dhg-2x7\*\*\*\*\*\*\*\*\*\*\*\*\*|The ID of the dedicated cluster to which the instance belongs. |
|ClusterName|String|TestCluster|The name of the dedicated cluster to which the instance belongs. |
|CreateTime|String|2020-10-09T06:12:04Z|The time when the instance was created. The time is displayed in the *yyyy*-*MM*-*dd*T*HH*:*mm*:*ss*Z format. |
|CustomId|String|123456789|The instance ID of the backend O&M platform. |
|Engine|String|MongoDB|The database engine. Valid value: **MongoDB**. |
|EngineVersion|String|4.2|The version number of the database engine. Valid value: **4.2**. |
|InstanceClass|String|mdb.shard.2x.small.s|The instance type. For more information, see **Table 1. Standalone or replica set instance types** in [Instance types](~~57141~~). |
|InstanceId|String|dds-t4n\*\*\*\*\*\*\*\*\*\*\*\*\*|The ID of the ApsaraDB for MongoDB instance. |
|InstanceName|String|TestInstance|The name of the ApsaraDB for MongoDB instance. |
|InstanceNodeList|Array of InstanceNodes| |Details about the instance nodes. |
|InstanceNodes| | | |
|DedicatedHostName|String|ch-t4n\*\*\*\*\*\*\*\*\*\*\*\*\*\*|The ID of the host to which the instances in a dedicated cluster belong. |
|InsName|String|xr-dhgi-mongo-21|The name of the shard. |
|NodeId|Integer|4068|The ID of the node. |
|NodeIp|String|192.168.0.2|The IP address of the node. |
|NodeType|String|normal|The type of the node. |
|Port|Integer|3002|The port number corresponding to the node. |
|Role|String|master|The role of the node. Valid values:

 -   **master**: a primary node.
-   **slave**: a secondary node. |
|ZoneId|String|cn-hangzhou-h|The zone ID of the instance. |
|InstanceStatus|String|1|The status of the instance. For information about the valid values of this parameter, see [Valid values of the InstanceStatus parameter for DescribeDedicatedClusterInstanceList](~~190071~~). |
|MaintainEndTime|String|22:00Z|The end time of the maintenance window. The time is in the *HH:mmZ* format. The time is displayed in UTC. |
|MaintainStartTime|String|18:00Z|The start time of the maintenance window. The time is in the *HH:mm*Z format. The time is displayed in UTC. |
|Region|String|China \(Hangzhou\)|The region where the instance is deployed. |
|RegionId|String|cn-hangzhou|The ID of the region where the instance is deployed. |
|StorageType|String|CLOUD\_ESSD|The type of the storage. |
|VpcId|String|vpc-bpxxxxxxxx|The ID of the VPC. |
|VswitchId|String|vsw-bpxxxxxxxx|The vSwitch ID of the VPC. |
|ZoneId|String|cn-hangzhou-h|The zone ID of the instance. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|25|The number of entries returned per page. |
|RequestId|String|A10B8ECB-0BA0-4EC6-93A5-C65FDEDA07CB|The ID of the request. |
|TotalCount|Integer|1|The number of instances in the response. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeDedicatedClusterInstanceList
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<Instances>
    <dbInstance>
        <StorageType>CLOUD_ESSD</StorageType>
        <EngineVersion>4.2</EngineVersion>
        <ZoneId>cn-hangzhou-h</ZoneId>
        <InstanceId>dds-t4n*************</InstanceId>
        <ClusterId>dhg-2x7*************</ClusterId>
        <CreateTime>2020-10-09T06:12:04Z</CreateTime>
        <InstanceClass>mdb.shard.2x.small.s</InstanceClass>
        <CharacterType>normal</CharacterType>
        <VswitchId>vsw-bpxxxxxxxx</VswitchId>
        <InstanceName>TestInstance</InstanceName>
        <MaintainEndTime>22:00Z</MaintainEndTime>
        <VpcId>vpc-bpxxxxxxxx</VpcId>
        <InstanceStatus>1</InstanceStatus>
        <CustomId>123456789</CustomId>
        <ClusterName>TestCluster</ClusterName>
        <Region>China (Hangzhou)</Region>
        <RegionId>cn-hangzhou</RegionId>
        <Engine>MongoDB</Engine>
        <MaintainStartTime>18:00Z</MaintainStartTime>
    </dbInstance>
    <dbInstance>
        <InstanceNodeList>
            <InstanceNodes>
                <Role>master</Role>
                <ZoneId>cn-hangzhou-h</ZoneId>
                <DedicatedHostName>ch-t4n**************</DedicatedHostName>
                <Port>3002</Port>
                <NodeType>normal</NodeType>
                <NodeId>4068</NodeId>
                <NodeIp>192.168.0.2</NodeIp>
                <InsName>xr-dhgi-mongo-21</InsName>
            </InstanceNodes>
        </InstanceNodeList>
    </dbInstance>
</Instances>
<TotalCount>1</TotalCount>
<PageSize>25</PageSize>
<RequestId>A10B8ECB-0BA0-4EC6-93A5-C65FDEDA07CB</RequestId>
<PageNumber>1</PageNumber>
```

`JSON` format

```
{
    "Instances":{
        "dbInstance":[
            {
                "StorageType":"CLOUD_ESSD",
                "EngineVersion":"4.2",
                "ZoneId":"cn-hangzhou-h",
                "InstanceId":"dds-t4n*************",
                "ClusterId":"dhg-2x7*************",
                "CreateTime":"2020-10-09T06:12:04Z",
                "InstanceClass":"mdb.shard.2x.small.s",
                "CharacterType":"normal",
                "VswitchId":"vsw-bpxxxxxxxx",
                "InstanceName":"TestInstance",
                "MaintainEndTime":"22:00Z",
                "VpcId":"vpc-bpxxxxxxxx",
                "InstanceStatus":"1",
                "CustomId":"123456789",
                "ClusterName":"TestCluster",
                "Region":"China (Hangzhou)",
                "RegionId":"cn-hangzhou",
                "Engine":"MongoDB",
                "MaintainStartTime":"18:00Z"
            },{
                "InstanceNodeList":{
                    "InstanceNodes":[
                        {
                            "Role":"master",
                            "ZoneId":"cn-hangzhou-h",
                            "DedicatedHostName":"ch-t4n**************",
                            "Port":"3002",
                            "NodeType":"normal",
                            "NodeId":"4068",
                            "NodeIp":"192.168.0.2",
                            "InsName":"xr-dhgi-mongo-21"
                        }
                    ]
                }
            }
        ]
    },
    "TotalCount":"1",
    "PageSize":"25",
    "RequestId":"A10B8ECB-0BA0-4EC6-93A5-C65FDEDA07CB",
    "PageNumber":"1"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

