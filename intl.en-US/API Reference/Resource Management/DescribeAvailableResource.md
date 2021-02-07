# DescribeAvailableResource

You can call this operation to query the types of ApsaraDB for Redis instances that can be created in a specified zone.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeAvailableResource&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAvailableResource|The operation that you want to perform. Set the value to **DescribeAvailableResource**. |
|RegionId|String|Yes|cn-hangzhou|The region ID. You can call the [DescribeRegions](~~61933~~) operation to view the region IDs. |
|ZoneId|String|No|cn-hangzhou-h|The zone ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to view the zone IDs. |
|InstanceChargeType|String|No|PrePaid|The billing method. Valid values:

 -   PrePaid: subscription.
-   PostPaid: pay-as-you-go.

 **Note:** Default value: PrePaid. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|344EE51D-8850-4935-B68B-58A8F4DCE3BD|The ID of the request. |
|SupportedDBTypes|Array of SupportedDBType| |An array that consists of the information of the database type supported. |
|SupportedDBType| | | |
|AvailableZones|Array of AvailableZone| |An array that consists of the information of the zones. |
|AvailableZone| | | |
|RegionId|String|cn-hangzhou|The ID of the region. |
|SupportedEngineVersions|Array of SupportedEngineVersion| |An array that consists of the information of the storage engine versions in the zone. |
|SupportedEngineVersion| | | |
|SupportedEngines|Array of SupportedEngine| |An array that consists of the information of the storage engines in the zone. |
|SupportedEngine| | | |
|Engine|String|WiredTiger|The storage engine of the instance. |
|SupportedNodeTypes|Array of SupportedNodeType| |An array that consists of the information of the instance types supported. |
|SupportedNodeType| | | |
|AvailableResources|Array of AvailableResource| |An array that consists of the information of the available resources. |
|AvailableResource| | | |
|InstanceClass|String|dds.mongo.2xlarge|The instance type. |
|InstanceClassRemark|String|8 vCPUs, 32 GiB \(maximum connections: 8000 IOPS: 14000\)|The specifications of the instance. |
|NetworkTypes|String|VPC|The network type of the instance. Valid values: |
|NodeType|String|3|The number of nodes in the instance. |
|Version|String|4.0|The database engine version of the instance. |
|ZoneId|String|cn-hangzhou-h|The zone ID of the instance. |
|DbType|String|sharding|The database engine of the instance. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeAvailableResource
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` fomat

```
<RequestId>E2463135-7FB3-4941-A232-31CF1793A6E0</RequestId>
<SupportedDBTypes>
    <SupportedDBType>
        <DbType>normal</DbType>
        <AvailableZones>
            <AvailableZone>
                <ZoneId>cn-hangzhou-h</ZoneId>
                <RegionId>cn-hangzhou</RegionId>
                <SupportedEngineVersions>
                    <SupportedEngineVersion>
                        <Version>4.2</Version>
                        <SupportedEngines>
                            <SupportedEngine>
                                <SupportedNodeTypes>
                                    <SupportedNodeType>
                                        <NetworkTypes>VPC</NetworkTypes>
                                        <NetworkTypes>Classic</NetworkTypes>
                                        <NodeType>3</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.medium</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.standard</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xmonopolize</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.mid</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.xlarge</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                    <SupportedNodeType>
                                        <NetworkTypes>Classic</NetworkTypes>
                                        <NetworkTypes>VPC</NetworkTypes>
                                        <NodeType>5</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.medium</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.standard</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xmonopolize</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.mid</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.xlarge</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                    <SupportedNodeType>
                                        <NetworkTypes/>
                                        <NodeType>7</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.medium</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.standard</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xmonopolize</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.mid</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.xlarge</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                </SupportedNodeTypes>
                            </SupportedEngine>
                        </SupportedEngines>
                    </SupportedEngineVersion>
                    <SupportedEngineVersion>
                        <Version>4.0</Version>
                        <SupportedEngines>
                            <SupportedEngine>
                                <SupportedNodeTypes>
                                    <SupportedNodeType>
                                        <NetworkTypes>VPC</NetworkTypes>
                                        <NetworkTypes>Classic</NetworkTypes>
                                        <NodeType>3</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.medium</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.standard</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xmonopolize</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.mid</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.xlarge</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                    <SupportedNodeType>
                                        <NetworkTypes>Classic</NetworkTypes>
                                        <NetworkTypes>VPC</NetworkTypes>
                                        <NodeType>5</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.medium</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.standard</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xmonopolize</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.mid</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.xlarge</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                    <SupportedNodeType>
                                        <NetworkTypes/>
                                        <NodeType>7</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.medium</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.standard</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xmonopolize</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.mid</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.xlarge</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                    <SupportedNodeType>
                                        <NetworkTypes>VPC</NetworkTypes>
                                        <NodeType>1</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 4 GiB memory (maximum connections: 4000 IOPS: 30*Storage capacity (GB) and must be less than 20000)</InstanceClassRemark>
                                                <InstanceClass>dds.sn2.medium.1</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 16 GiB memory (maximum connections: 8000 IOPS: 30*Storage capacity (GB) and must be less than 20000)</InstanceClassRemark>
                                                <InstanceClass>dds.sn2.xlarge.1</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 16 GiB memory (maximum connections: 8000 IOPS: 30*Storage capacity (GB) and must be less than 20000)</InstanceClassRemark>
                                                <InstanceClass>dds.sn4.xlarge.1</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 8 GiB memory (maximum connections: 6000 IOPS: 30*Storage capacity (GB) and must be less than 20000)</InstanceClassRemark>
                                                <InstanceClass>dds.sn4.large.1</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 8 GiB memory (maximum connections: 6000 IOPS: 30*Storage capacity (GB) and must be less than 20000)</InstanceClassRemark>
                                                <InstanceClass>dds.sn2.large.1</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                </SupportedNodeTypes>
                            </SupportedEngine>
                        </SupportedEngines>
                    </SupportedEngineVersion>
                    <SupportedEngineVersion>
                        <Version>3.4</Version>
                        <SupportedEngines>
                            <SupportedEngine>
                                <SupportedNodeTypes>
                                    <SupportedNodeType>
                                        <NetworkTypes>VPC</NetworkTypes>
                                        <NetworkTypes>Classic</NetworkTypes>
                                        <NodeType>3</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.medium</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.standard</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xmonopolize</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.mid</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.xlarge</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                    <SupportedNodeType>
                                        <NetworkTypes/>
                                        <NodeType>5</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.medium</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.standard</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xmonopolize</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.mid</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.xlarge</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                    <SupportedNodeType>
                                        <NetworkTypes/>
                                        <NodeType>7</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.medium</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.standard</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.2xmonopolize</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)</InstanceClassRemark>
                                                <InstanceClass>mongo.x8.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.mid</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongo.xlarge</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                    <SupportedNodeType>
                                        <NetworkTypes>VPC</NetworkTypes>
                                        <NodeType>1</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 4 GiB memory (maximum connections: 4000 IOPS: 30*Storage capacity (GB) and must be less than 20000)</InstanceClassRemark>
                                                <InstanceClass>dds.sn2.medium.1</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 16 GiB memory (maximum connections: 8000 IOPS: 30*Storage capacity (GB) and must be less than 20000)</InstanceClassRemark>
                                                <InstanceClass>dds.sn2.xlarge.1</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 16 GiB memory (maximum connections: 8000 IOPS: 30*Storage capacity (GB) and must be less than 20000)</InstanceClassRemark>
                                                <InstanceClass>dds.sn4.xlarge.1</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 8 GiB memory (maximum connections: 6000 IOPS: 30*Storage capacity (GB) and must be less than 20000)</InstanceClassRemark>
                                                <InstanceClass>dds.sn4.large.1</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 8 GiB memory (maximum connections: 6000 IOPS: 30*Storage capacity (GB) and must be less than 20000)</InstanceClassRemark>
                                                <InstanceClass>dds.sn2.large.1</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                </SupportedNodeTypes>
                            </SupportedEngine>
                        </SupportedEngines>
                    </SupportedEngineVersion>
                </SupportedEngineVersions>
            </AvailableZone>
        </AvailableZones>
    </SupportedDBType>
    <SupportedDBType>
        <DbType>sharding</DbType>
        <AvailableZones>
            <AvailableZone>
                <ZoneId>cn-hangzhou-h</ZoneId>
                <RegionId>cn-hangzhou</RegionId>
                <SupportedEngineVersions>
                    <SupportedEngineVersion>
                        <Version>4.2</Version>
                        <SupportedEngines>
                            <SupportedEngine>
                                <SupportedNodeTypes>
                                    <SupportedNodeType>
                                        <NodeType>mongos</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB memory (maximum connections: 1000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.mid</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 64 GiB memory (maximum connections: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 8 GiB memory (maximum connections: 4000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 32 GiB (maximum connections: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 4 GiB memory (maximum connections: 2000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.standard</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 16 GiB (maximum connections: 8000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.xlarge</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                    <SupportedNodeType>
                                        <NodeType>shard</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 128 GiB memory (dedicated) (IOPS: 36000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.sn8.8xlarge.3</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 64 GiB memory (IOPS: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 64 GiB memory (dedicated) (IOPS: 18000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.sn8.4xlarge.3</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 8 GiB memory (IOPS: 4000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 16 GiB (IOPS: 8000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 32 GiB memory (dedicated) (IOPS: 9000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.sn8.2xlarge.3</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB (IOPS: 1000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.mid</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 32 GiB (IOPS: 14000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>32 vCPUs, 256 GiB memory (dedicated) (IOPS: 72000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.sn8.16xlarge.3</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 16 GiB memory (dedicated) (IOPS: 4500)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.sn8.xlarge.3</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 4 GiB memory (IOPS: 2000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.standard</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                    <SupportedNodeType>
                                        <NodeType>configserver</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB memory</InstanceClassRemark>
                                                <InstanceClass>dds.cs.mid</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                </SupportedNodeTypes>
                            </SupportedEngine>
                        </SupportedEngines>
                    </SupportedEngineVersion>
                    <SupportedEngineVersion>
                        <Version>4.0</Version>
                        <SupportedEngines>
                            <SupportedEngine>
                                <SupportedNodeTypes>
                                    <SupportedNodeType>
                                        <NodeType>mongos</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB memory (maximum connections: 1000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.mid</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 64 GiB memory (maximum connections: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 8 GiB memory (maximum connections: 4000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 32 GiB (maximum connections: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 4 GiB memory (maximum connections: 2000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.standard</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 16 GiB (maximum connections: 8000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.xlarge</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                    <SupportedNodeType>
                                        <NodeType>shard</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 128 GiB memory (dedicated) (IOPS: 36000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.sn8.8xlarge.3</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 64 GiB memory (IOPS: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 64 GiB memory (dedicated) (IOPS: 18000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.sn8.4xlarge.3</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 8 GiB memory (IOPS: 4000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 16 GiB (IOPS: 8000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 32 GiB memory (dedicated) (IOPS: 9000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.sn8.2xlarge.3</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB (IOPS: 1000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.mid</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 32 GiB (IOPS: 14000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>32 vCPUs, 256 GiB memory (dedicated) (IOPS: 72000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.sn8.16xlarge.3</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 16 GiB memory (dedicated) (IOPS: 4500)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.sn8.xlarge.3</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 4 GiB memory (IOPS: 2000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.standard</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                    <SupportedNodeType>
                                        <NodeType>configserver</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB memory</InstanceClassRemark>
                                                <InstanceClass>dds.cs.mid</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                </SupportedNodeTypes>
                            </SupportedEngine>
                        </SupportedEngines>
                    </SupportedEngineVersion>
                    <SupportedEngineVersion>
                        <Version>3.4</Version>
                        <SupportedEngines>
                            <SupportedEngine>
                                <SupportedNodeTypes>
                                    <SupportedNodeType>
                                        <NodeType>mongos</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB memory (maximum connections: 1000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.mid</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 64 GiB memory (maximum connections: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 8 GiB memory (maximum connections: 4000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 32 GiB (maximum connections: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 4 GiB memory (maximum connections: 2000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.standard</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 16 GiB (maximum connections: 8000)</InstanceClassRemark>
                                                <InstanceClass>dds.mongos.xlarge</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                    <SupportedNodeType>
                                        <NodeType>shard</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 128 GiB memory (dedicated) (IOPS: 36000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.sn8.8xlarge.3</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>16 vCPUs, 64 GiB memory (IOPS: 16000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.4xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 64 GiB memory (dedicated) (IOPS: 18000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.sn8.4xlarge.3</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 8 GiB memory (IOPS: 4000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.large</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 16 GiB (IOPS: 8000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>4 vCPUs, 32 GiB memory (dedicated) (IOPS: 9000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.sn8.2xlarge.3</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB (IOPS: 1000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.mid</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>8 vCPUs, 32 GiB (IOPS: 14000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.2xlarge</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>32 vCPUs, 256 GiB memory (dedicated) (IOPS: 72000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.sn8.16xlarge.3</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 16 GiB memory (dedicated) (IOPS: 4500)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.sn8.xlarge.3</InstanceClass>
                                            </AvailableResource>
                                            <AvailableResource>
                                                <InstanceClassRemark>2 vCPUs, 4 GiB memory (IOPS: 2000)</InstanceClassRemark>
                                                <InstanceClass>dds.shard.standard</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                    <SupportedNodeType>
                                        <NodeType>configserver</NodeType>
                                        <AvailableResources>
                                            <AvailableResource>
                                                <InstanceClassRemark>1 vCPUs, 2 GiB memory</InstanceClassRemark>
                                                <InstanceClass>dds.cs.mid</InstanceClass>
                                            </AvailableResource>
                                        </AvailableResources>
                                    </SupportedNodeType>
                                </SupportedNodeTypes>
                            </SupportedEngine>
                        </SupportedEngines>
                    </SupportedEngineVersion>
                </SupportedEngineVersions>
            </AvailableZone>
        </AvailableZones>
    </SupportedDBType>
</SupportedDBTypes>
```

`JSON` format

```
{
	"RequestId": "E2463135-7FB3-4941-A232-31CF1793A6E0",
	"SupportedDBTypes": {
		"SupportedDBType": [
			{
				"DbType": "normal",
				"AvailableZones": {
					"AvailableZone": [
						{
							"ZoneId": "cn-hangzhou-h",
							"RegionId": "cn-hangzhou",
							"SupportedEngineVersions": {
								"SupportedEngineVersion": [
									{
										"Version": "4.2",
										"SupportedEngines": {
											"SupportedEngine": [
												{
													"SupportedNodeTypes": {
														"SupportedNodeType": [
															{
																"NetworkTypes": [
																	"VPC",
																	"Classic"
																],
																"NodeType": "3",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)",
																			"InstanceClass": "dds.mongo.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)",
																			"InstanceClass": "mongo.x8.medium"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)",
																			"InstanceClass": "mongo.x8.large"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)",
																			"InstanceClass": "mongo.x8.xlarge"
																		},
																		{
																			"InstanceClassRemark": "32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)",
																			"InstanceClass": "mongo.x8.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)",
																			"InstanceClass": "dds.mongo.large"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)",
																			"InstanceClass": "dds.mongo.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)",
																			"InstanceClass": "dds.mongo.standard"
																		},
																		{
																			"InstanceClassRemark": "60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)",
																			"InstanceClass": "dds.mongo.2xmonopolize"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)",
																			"InstanceClass": "mongo.x8.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)",
																			"InstanceClass": "dds.mongo.mid"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)",
																			"InstanceClass": "dds.mongo.xlarge"
																		}
																	]
																}
															},
															{
																"NetworkTypes": [
																	"Classic",
																	"VPC"
																],
																"NodeType": "5",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)",
																			"InstanceClass": "dds.mongo.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)",
																			"InstanceClass": "mongo.x8.medium"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)",
																			"InstanceClass": "mongo.x8.large"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)",
																			"InstanceClass": "mongo.x8.xlarge"
																		},
																		{
																			"InstanceClassRemark": "32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)",
																			"InstanceClass": "mongo.x8.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)",
																			"InstanceClass": "dds.mongo.large"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)",
																			"InstanceClass": "dds.mongo.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)",
																			"InstanceClass": "dds.mongo.standard"
																		},
																		{
																			"InstanceClassRemark": "60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)",
																			"InstanceClass": "dds.mongo.2xmonopolize"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)",
																			"InstanceClass": "mongo.x8.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)",
																			"InstanceClass": "dds.mongo.mid"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)",
																			"InstanceClass": "dds.mongo.xlarge"
																		}
																	]
																}
															},
															{
																"NetworkTypes": null,
																"NodeType": "7",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)",
																			"InstanceClass": "dds.mongo.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)",
																			"InstanceClass": "mongo.x8.medium"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)",
																			"InstanceClass": "mongo.x8.large"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)",
																			"InstanceClass": "mongo.x8.xlarge"
																		},
																		{
																			"InstanceClassRemark": "32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)",
																			"InstanceClass": "mongo.x8.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)",
																			"InstanceClass": "dds.mongo.large"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)",
																			"InstanceClass": "dds.mongo.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)",
																			"InstanceClass": "dds.mongo.standard"
																		},
																		{
																			"InstanceClassRemark": "60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)",
																			"InstanceClass": "dds.mongo.2xmonopolize"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)",
																			"InstanceClass": "mongo.x8.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)",
																			"InstanceClass": "dds.mongo.mid"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)",
																			"InstanceClass": "dds.mongo.xlarge"
																		}
																	]
																}
															}
														]
													}
												}
											]
										}
									},
									{
										"Version": "4.0",
										"SupportedEngines": {
											"SupportedEngine": [
												{
													"SupportedNodeTypes": {
														"SupportedNodeType": [
															{
																"NetworkTypes": [
																	"VPC",
																	"Classic"
																],
																"NodeType": "3",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)",
																			"InstanceClass": "dds.mongo.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)",
																			"InstanceClass": "mongo.x8.medium"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)",
																			"InstanceClass": "mongo.x8.large"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)",
																			"InstanceClass": "mongo.x8.xlarge"
																		},
																		{
																			"InstanceClassRemark": "32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)",
																			"InstanceClass": "mongo.x8.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)",
																			"InstanceClass": "dds.mongo.large"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)",
																			"InstanceClass": "dds.mongo.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)",
																			"InstanceClass": "dds.mongo.standard"
																		},
																		{
																			"InstanceClassRemark": "60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)",
																			"InstanceClass": "dds.mongo.2xmonopolize"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)",
																			"InstanceClass": "mongo.x8.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)",
																			"InstanceClass": "dds.mongo.mid"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)",
																			"InstanceClass": "dds.mongo.xlarge"
																		}
																	]
																}
															},
															{
																"NetworkTypes": [
																	"Classic",
																	"VPC"
																],
																"NodeType": "5",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)",
																			"InstanceClass": "dds.mongo.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)",
																			"InstanceClass": "mongo.x8.medium"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)",
																			"InstanceClass": "mongo.x8.large"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)",
																			"InstanceClass": "mongo.x8.xlarge"
																		},
																		{
																			"InstanceClassRemark": "32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)",
																			"InstanceClass": "mongo.x8.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)",
																			"InstanceClass": "dds.mongo.large"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)",
																			"InstanceClass": "dds.mongo.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)",
																			"InstanceClass": "dds.mongo.standard"
																		},
																		{
																			"InstanceClassRemark": "60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)",
																			"InstanceClass": "dds.mongo.2xmonopolize"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)",
																			"InstanceClass": "mongo.x8.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)",
																			"InstanceClass": "dds.mongo.mid"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)",
																			"InstanceClass": "dds.mongo.xlarge"
																		}
																	]
																}
															},
															{
																"NetworkTypes": null,
																"NodeType": "7",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)",
																			"InstanceClass": "dds.mongo.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)",
																			"InstanceClass": "mongo.x8.medium"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)",
																			"InstanceClass": "mongo.x8.large"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)",
																			"InstanceClass": "mongo.x8.xlarge"
																		},
																		{
																			"InstanceClassRemark": "32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)",
																			"InstanceClass": "mongo.x8.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)",
																			"InstanceClass": "dds.mongo.large"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)",
																			"InstanceClass": "dds.mongo.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)",
																			"InstanceClass": "dds.mongo.standard"
																		},
																		{
																			"InstanceClassRemark": "60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)",
																			"InstanceClass": "dds.mongo.2xmonopolize"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)",
																			"InstanceClass": "mongo.x8.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)",
																			"InstanceClass": "dds.mongo.mid"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)",
																			"InstanceClass": "dds.mongo.xlarge"
																		}
																	]
																}
															},
															{
																"NetworkTypes": [
																	"VPC"
																],
																"NodeType": "1",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "2 vCPUs, 4 GiB memory (maximum connections: 4000 IOPS: 30*Storage capacity (GB) and must be less than 20000)",
																			"InstanceClass": "dds.sn2.medium.1"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 16 GiB memory (maximum connections: 8000 IOPS: 30*Storage capacity (GB) and must be less than 20000)",
																			"InstanceClass": "dds.sn2.xlarge.1"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 16 GiB memory (maximum connections: 8000 IOPS: 30*Storage capacity (GB) and must be less than 20000)",
																			"InstanceClass": "dds.sn4.xlarge.1"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 8 GiB memory (maximum connections: 6000 IOPS: 30*Storage capacity (GB) and must be less than 20000)",
																			"InstanceClass": "dds.sn4.large.1"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 8 GiB memory (maximum connections: 6000 IOPS: 30*Storage capacity (GB) and must be less than 20000)",
																			"InstanceClass": "dds.sn2.large.1"
																		}
																	]
																}
															}
														]
													}
												}
											]
										}
									},
									{
										"Version": "3.4",
										"SupportedEngines": {
											"SupportedEngine": [
												{
													"SupportedNodeTypes": {
														"SupportedNodeType": [
															{
																"NetworkTypes": [
																	"VPC",
																	"Classic"
																],
																"NodeType": "3",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)",
																			"InstanceClass": "dds.mongo.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)",
																			"InstanceClass": "mongo.x8.medium"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)",
																			"InstanceClass": "mongo.x8.large"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)",
																			"InstanceClass": "mongo.x8.xlarge"
																		},
																		{
																			"InstanceClassRemark": "32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)",
																			"InstanceClass": "mongo.x8.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)",
																			"InstanceClass": "dds.mongo.large"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)",
																			"InstanceClass": "dds.mongo.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)",
																			"InstanceClass": "dds.mongo.standard"
																		},
																		{
																			"InstanceClassRemark": "60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)",
																			"InstanceClass": "dds.mongo.2xmonopolize"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)",
																			"InstanceClass": "mongo.x8.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)",
																			"InstanceClass": "dds.mongo.mid"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)",
																			"InstanceClass": "dds.mongo.xlarge"
																		}
																	]
																}
															},
															{
																"NetworkTypes": null,
																"NodeType": "5",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)",
																			"InstanceClass": "dds.mongo.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)",
																			"InstanceClass": "mongo.x8.medium"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)",
																			"InstanceClass": "mongo.x8.large"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)",
																			"InstanceClass": "mongo.x8.xlarge"
																		},
																		{
																			"InstanceClassRemark": "32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)",
																			"InstanceClass": "mongo.x8.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)",
																			"InstanceClass": "dds.mongo.large"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)",
																			"InstanceClass": "dds.mongo.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)",
																			"InstanceClass": "dds.mongo.standard"
																		},
																		{
																			"InstanceClassRemark": "60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)",
																			"InstanceClass": "dds.mongo.2xmonopolize"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)",
																			"InstanceClass": "mongo.x8.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)",
																			"InstanceClass": "dds.mongo.mid"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)",
																			"InstanceClass": "dds.mongo.xlarge"
																		}
																	]
																}
															},
															{
																"NetworkTypes": null,
																"NodeType": "7",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "8 vCPUs, 32 GiB (maximum connections: 8000 IOPS: 14000)",
																			"InstanceClass": "dds.mongo.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 16 GiB memory (dedicated) (maximum connections: 2500 IOPS: 4500)",
																			"InstanceClass": "mongo.x8.medium"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 32 GiB memory (dedicated) (maximum connections: 5000 IOPS: 9000)",
																			"InstanceClass": "mongo.x8.large"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 64 GiB memory (dedicated) (maximum connections: 10000 IOPS: 18000)",
																			"InstanceClass": "mongo.x8.xlarge"
																		},
																		{
																			"InstanceClassRemark": "32 vCPUs, 256 GiB memory (dedicated) (maximum connections: 40000 IOPS: 72000)",
																			"InstanceClass": "mongo.x8.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 8 GiB memory (maximum connections: 2000 IOPS: 4000)",
																			"InstanceClass": "dds.mongo.large"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 64 GiB memory (maximum connections: 16000 IOPS: 16000)",
																			"InstanceClass": "dds.mongo.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 4 GiB memory (maximum connections: 1000 IOPS: 2000)",
																			"InstanceClass": "dds.mongo.standard"
																		},
																		{
																			"InstanceClassRemark": "60 vCPUs, 440 GiB memory (dedicated) (maximum connections: 100000 IOPS: 100000)",
																			"InstanceClass": "dds.mongo.2xmonopolize"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 128 GiB memory (dedicated) (maximum connections: 20000 IOPS: 36000)",
																			"InstanceClass": "mongo.x8.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory (maximum connections: 500 IOPS: 1000)",
																			"InstanceClass": "dds.mongo.mid"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 16 GiB (maximum connections: 4000 IOPS: 8000)",
																			"InstanceClass": "dds.mongo.xlarge"
																		}
																	]
																}
															},
															{
																"NetworkTypes": [
																	"VPC"
																],
																"NodeType": "1",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "2 vCPUs, 4 GiB memory (maximum connections: 4000 IOPS: 30*Storage capacity (GB) and must be less than 20000)",
																			"InstanceClass": "dds.sn2.medium.1"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 16 GiB memory (maximum connections: 8000 IOPS: 30*Storage capacity (GB) and must be less than 20000)",
																			"InstanceClass": "dds.sn2.xlarge.1"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 16 GiB memory (maximum connections: 8000 IOPS: 30*Storage capacity (GB) and must be less than 20000)",
																			"InstanceClass": "dds.sn4.xlarge.1"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 8 GiB memory (maximum connections: 6000 IOPS: 30*Storage capacity (GB) and must be less than 20000)",
																			"InstanceClass": "dds.sn4.large.1"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 8 GiB memory (maximum connections: 6000 IOPS: 30*Storage capacity (GB) and must be less than 20000)",
																			"InstanceClass": "dds.sn2.large.1"
																		}
																	]
																}
															}
														]
													}
												}
											]
										}
									}
								]
							}
						}
					]
				}
			},
			{
				"DbType": "sharding",
				"AvailableZones": {
					"AvailableZone": [
						{
							"ZoneId": "cn-hangzhou-h",
							"RegionId": "cn-hangzhou",
							"SupportedEngineVersions": {
								"SupportedEngineVersion": [
									{
										"Version": "4.2",
										"SupportedEngines": {
											"SupportedEngine": [
												{
													"SupportedNodeTypes": {
														"SupportedNodeType": [
															{
																"NodeType": "mongos",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory (maximum connections: 1000)",
																			"InstanceClass": "dds.mongos.mid"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 64 GiB memory (maximum connections: 16000)",
																			"InstanceClass": "dds.mongos.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 8 GiB memory (maximum connections: 4000)",
																			"InstanceClass": "dds.mongos.large"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 32 GiB (maximum connections: 16000)",
																			"InstanceClass": "dds.mongos.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 4 GiB memory (maximum connections: 2000)",
																			"InstanceClass": "dds.mongos.standard"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 16 GiB (maximum connections: 8000)",
																			"InstanceClass": "dds.mongos.xlarge"
																		}
																	]
																}
															},
															{
																"NodeType": "shard",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "16 vCPUs, 128 GiB memory (dedicated) (IOPS: 36000)",
																			"InstanceClass": "dds.shard.sn8.8xlarge.3"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 64 GiB memory (IOPS: 16000)",
																			"InstanceClass": "dds.shard.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 64 GiB memory (dedicated) (IOPS: 18000)",
																			"InstanceClass": "dds.shard.sn8.4xlarge.3"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 8 GiB memory (IOPS: 4000)",
																			"InstanceClass": "dds.shard.large"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 16 GiB (IOPS: 8000)",
																			"InstanceClass": "dds.shard.xlarge"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 32 GiB memory (dedicated) (IOPS: 9000)",
																			"InstanceClass": "dds.shard.sn8.2xlarge.3"
																		},
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory (IOPS: 1000)",
																			"InstanceClass": "dds.shard.mid"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 32 GiB (IOPS: 14000)",
																			"InstanceClass": "dds.shard.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "32 vCPUs, 256 GiB memory (dedicated) (IOPS: 72000)",
																			"InstanceClass": "dds.shard.sn8.16xlarge.3"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 16 GiB memory (dedicated) (IOPS: 4500)",
																			"InstanceClass": "dds.shard.sn8.xlarge.3"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 4 GiB memory (IOPS: 2000)",
																			"InstanceClass": "dds.shard.standard"
																		}
																	]
																}
															},
															{
																"NodeType": "configserver",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory",
																			"InstanceClass": "dds.cs.mid"
																		}
																	]
																}
															}
														]
													}
												}
											]
										}
									},
									{
										"Version": "4.0",
										"SupportedEngines": {
											"SupportedEngine": [
												{
													"SupportedNodeTypes": {
														"SupportedNodeType": [
															{
																"NodeType": "mongos",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory (maximum connections: 1000)",
																			"InstanceClass": "dds.mongos.mid"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 64 GiB memory (maximum connections: 16000)",
																			"InstanceClass": "dds.mongos.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 8 GiB memory (maximum connections: 4000)",
																			"InstanceClass": "dds.mongos.large"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 32 GiB (maximum connections: 16000)",
																			"InstanceClass": "dds.mongos.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 4 GiB memory (maximum connections: 2000)",
																			"InstanceClass": "dds.mongos.standard"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 16 GiB (maximum connections: 8000)",
																			"InstanceClass": "dds.mongos.xlarge"
																		}
																	]
																}
															},
															{
																"NodeType": "shard",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "16 vCPUs, 128 GiB memory (dedicated) (IOPS: 36000)",
																			"InstanceClass": "dds.shard.sn8.8xlarge.3"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 64 GiB memory (IOPS: 16000)",
																			"InstanceClass": "dds.shard.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 64 GiB memory (dedicated) (IOPS: 18000)",
																			"InstanceClass": "dds.shard.sn8.4xlarge.3"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 8 GiB memory (IOPS: 4000)",
																			"InstanceClass": "dds.shard.large"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 16 GiB (IOPS: 8000)",
																			"InstanceClass": "dds.shard.xlarge"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 32 GiB memory (dedicated) (IOPS: 9000)",
																			"InstanceClass": "dds.shard.sn8.2xlarge.3"
																		},
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory (IOPS: 1000)",
																			"InstanceClass": "dds.shard.mid"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 32 GiB (IOPS: 14000)",
																			"InstanceClass": "dds.shard.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "32 vCPUs, 256 GiB memory (dedicated) (IOPS: 72000)",
																			"InstanceClass": "dds.shard.sn8.16xlarge.3"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 16 GiB memory (dedicated) (IOPS: 4500)",
																			"InstanceClass": "dds.shard.sn8.xlarge.3"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 4 GiB memory (IOPS: 2000)",
																			"InstanceClass": "dds.shard.standard"
																		}
																	]
																}
															},
															{
																"NodeType": "configserver",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory",
																			"InstanceClass": "dds.cs.mid"
																		}
																	]
																}
															}
														]
													}
												}
											]
										}
									},
									{
										"Version": "3.4",
										"SupportedEngines": {
											"SupportedEngine": [
												{
													"SupportedNodeTypes": {
														"SupportedNodeType": [
															{
																"NodeType": "mongos",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory (maximum connections: 1000)",
																			"InstanceClass": "dds.mongos.mid"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 64 GiB memory (maximum connections: 16000)",
																			"InstanceClass": "dds.mongos.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 8 GiB memory (maximum connections: 4000)",
																			"InstanceClass": "dds.mongos.large"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 32 GiB (maximum connections: 16000)",
																			"InstanceClass": "dds.mongos.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 4 GiB memory (maximum connections: 2000)",
																			"InstanceClass": "dds.mongos.standard"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 16 GiB (maximum connections: 8000)",
																			"InstanceClass": "dds.mongos.xlarge"
																		}
																	]
																}
															},
															{
																"NodeType": "shard",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "16 vCPUs, 128 GiB memory (dedicated) (IOPS: 36000)",
																			"InstanceClass": "dds.shard.sn8.8xlarge.3"
																		},
																		{
																			"InstanceClassRemark": "16 vCPUs, 64 GiB memory (IOPS: 16000)",
																			"InstanceClass": "dds.shard.4xlarge"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 64 GiB memory (dedicated) (IOPS: 18000)",
																			"InstanceClass": "dds.shard.sn8.4xlarge.3"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 8 GiB memory (IOPS: 4000)",
																			"InstanceClass": "dds.shard.large"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 16 GiB (IOPS: 8000)",
																			"InstanceClass": "dds.shard.xlarge"
																		},
																		{
																			"InstanceClassRemark": "4 vCPUs, 32 GiB memory (dedicated) (IOPS: 9000)",
																			"InstanceClass": "dds.shard.sn8.2xlarge.3"
																		},
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory (IOPS: 1000)",
																			"InstanceClass": "dds.shard.mid"
																		},
																		{
																			"InstanceClassRemark": "8 vCPUs, 32 GiB (IOPS: 14000)",
																			"InstanceClass": "dds.shard.2xlarge"
																		},
																		{
																			"InstanceClassRemark": "32 vCPUs, 256 GiB memory (dedicated) (IOPS: 72000)",
																			"InstanceClass": "dds.shard.sn8.16xlarge.3"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 16 GiB memory (dedicated) (IOPS: 4500)",
																			"InstanceClass": "dds.shard.sn8.xlarge.3"
																		},
																		{
																			"InstanceClassRemark": "2 vCPUs, 4 GiB memory (IOPS: 2000)",
																			"InstanceClass": "dds.shard.standard"
																		}
																	]
																}
															},
															{
																"NodeType": "configserver",
																"AvailableResources": {
																	"AvailableResource": [
																		{
																			"InstanceClassRemark": "1 vCPUs, 2 GiB memory",
																			"InstanceClass": "dds.cs.mid"
																		}
																	]
																}
															}
														]
													}
												}
											]
										}
									}
								]
							}
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

