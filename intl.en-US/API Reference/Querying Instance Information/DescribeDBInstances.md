# DescribeDBInstances

You can call this operation to query the list of ApsaraDB for MongoDB instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeDBInstances&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDBInstances|The operation that you want to perform. Set the value to **DescribeDBInstances**. |
|PageNumber|Integer|No|1|The number of the page to return. The value must be a positive integer. Default value: **1**. |
|PageSize|Integer|No|30|The number of entries to return on each page. Valid values: **30, 50, and 100**. Default value: **30**. |
|DBInstanceId|String|No|dds-bpxxxxxxxx|The ID of the instance. |
|ReplicationFactor|String|No|3|The number of nodes in a replica set instance. Valid values: **3, 5, and 7**. |
|DBInstanceDescription|String|No|Test database|The description or remarks of the instance. |
|DBInstanceStatus|String|No|ACTIVATION|The status of the instance. For more information about valid values, see [Instance states](~~63870~~). |
|DBInstanceType|String|No|replicate|The instance type. Valid values:

-   **sharding**: a sharded cluster instance
-   **replicate**: a replica set or standalone instance. This is the default value. |
|DBInstanceClass|String|No|dds.mongo.mid|The instance specifications. For more information about valid values, see [Instance types](~~57141~~). |
|Engine|String|No|MongoDB|The database engine. Valid value: **MongoDB**. |
|EngineVersion|String|No|4.0|The database version of the instance. Valid values: 3.2, 3.4, 4.0, and 4.2. |
|NetworkType|String|No|VPC|The network type of the instance. Valid values:

-   **Classic**
-   **VPC** |
|VpcId|String|No|vpc-bpxxxxxxxx|The ID of the virtual private cloud \(VPC\). |
|VSwitchId|String|No|vsw-bpxxxxxxxx|The ID of the VSwitch that is connected to the VPC. |
|ChargeType|String|No|PrePaid|The billing method of the instance. Valid values:

-   **PrePaid**: subscription
-   **PostPaid**: pay-as-you-go |
|ZoneId|String|No|cn-hangzhou-b|The ID of the zone. |
|Tag.N.Key|String|No|testdatabase|The key of the tag. Valid values of N: **1** to **20**. The tag key can be up to 64 characters in length. It cannot start with `aliyun`, `acs:`, `http://`, or `https://`.

**Note:** This parameter cannot be an empty string. |
|Tag.N.Value|String|No|apitest|The value of the tag. Valid values of N: **1** to **20**. The tag value can be up to 128 characters in length. It cannot start with `aliyun`, `acs:`, `http://`, or `https://`.

**Note:** Tag.N.Value can be an empty string. |
|RegionId|String|No|cn-hangzhou|The ID of the region where the instance is deployed. You can call the [DescribeRegions](~~61933~~) operation to query the region ID. |
|ExpireTime|String|No|2019-12-26T16:00Z|The time when the instance expires. |
|Expired|String|No|true|Specifies whether the instance has expired. Valid values:

-   **true**: The instance has expired.
-   **false**: The instance has not expired. |
|ConnectionDomain|String|No|dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com|The connection domain of the node, you can call the [DescribeDBInstanceAttribute](~~62010~~) to query.|
|ResourceGroupId|String|No|sg-bpxxxxxxxxxxxxxxxxxx|The ID of the resource group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the returned page. |
|TotalCount|Integer|1|The number of the instances in the response. |
|PageSize|Integer|30|The number of entries returned per page. |
|RequestId|String|A10B8ECB-0BA0-4EC6-93A5-C65FDEDA07CB|The ID of the request. |
|DBInstances|Array| |The list of the instances. |
|DBInstance| | | |
|ChargeType|String|PostPaid|The billing method of the instance.

-   **PrePaid**: subscription
-   **PostPaid**: pay-as-you-go |
|CreationTime|String|2018-09-25T06:33:07Z|The time when the instance was created. Specify the time in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC. |
|DBInstanceClass|String|dds.mongo.mid|The instance type. |
|DBInstanceDescription|String|Test database|The description or remarks of the instance. |
|DBInstanceId|String|dds-bpxxxxxxxx|The ID of the instance. |
|DBInstanceStatus|String|Running|The status of the instance. For more information, see [Instance states](~~63870~~). |
|DBInstanceStorage|Integer|20|The storage space of the instance. |
|DBInstanceType|String|sharding|The instance type.

-   **sharding**: a sharded cluster instance
-   **replicate**: a replica set instance |
|DestroyTime|String|2019-03-05T11:26:02Z|The time when the instance is released. Specify the time in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC.

**Note:**

-   Subscription instances are released seven days after expiration. After an instance is released, its data is deleted and cannot be restored.
-   Pay-as-you-go instances will be locked when the payment is overdue for more than 24 hours. The instance will be released when it is overdue for more than seven days. The data of released instances will be deleted and cannot be recovered. |
|Engine|String|MongoDB|The database engine. |
|EngineVersion|String|4.0|The version of the database. |
|ExpireTime|String|2019-11-25T16:00Z|The time when the instance expires. Specify the time in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC. |
|KindCode|String|1|The type of the instance. Valid values:-   **0**: a physical machine
-   **1**: an Elastic Compute Service \(ECS\) instance
-   **2**: a Docker cluster instance
-   **18**: a Kubernetes cluster instance |
|LastDowngradeTime|String|2019-03-08|The time when the instance was last downgraded. |
|LockMode|String|Unlock|Indicates whether the instance is locked.

-   **Unlock**: The instance is not locked.
-   **ManualLock**: The instance has been manually locked.
-   **LockByExpiration**: The instance has been locked upon expiration.
-   **LockByRestoration:** The instance has been locked for a rollback.
-   **LockByDiskQuota:** The instance has been automatically locked because its storage space is exhausted.
-   **Released:** The instance has been released. You cannot unlock a released instance. After an instance is released, you can only use a backup to restore the data of the instance to a new instance. This process requires a long time. |
|MongosList|Array| |The list of mongos.

**Note:** This parameter is returned if the instance is a sharded cluster instance. |
|MongosAttribute| | | |
|NodeClass|String|dds.mongos.mid|The instance type of the mongos. |
|NodeDescription|String|Test mongos|The description of the mongos. |
|NodeId|String|s-bpxxxxxxxx|The ID of the mongos. |
|NetworkType|String|VPC|The network type of the instance.

-   **Classic**
-   **VPC** |
|RegionId|String|cn-hangzhou|The ID of the region where the instance is deployed. |
|ReplicationFactor|String|3|The number of the nodes in the instance.

**Note:** This parameter is returned if the instance is a replica set instance. |
|ResourceGroupId|String|rg-axxxxxxxx|The ID of the resource group. |
|ShardList|Array| |The list of shards.

**Note:** This parameter is returned if the instance is a sharded cluster instance. |
|ShardAttribute| | | |
|NodeClass|String|dds.shard.mid|The instance type of the shard. |
|NodeDescription|String|Test shard node|The description of the shard. |
|NodeId|String|d-bpxxxxxxxx|The ID of the shard. |
|NodeStorage|Integer|20|The storage space of the shard. Unit: GB. |
|Tags|Array| |The list of resource tags. |
|Tag| | | |
|Key|String|test|The key of the tag. |
|Value|String|api|The value of the tag. |
|VpcAuthMode|String|Close|Indicates whether password-free access within the VPC is enabled. Valid values:

-   **Open**: Password-free access is enabled.
-   **Close**: Password-free access is disabled. |
|ZoneId|String|cn-hangzhou-b|The ID of the zone to which the instance belongs. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeDBInstances
&<Common request parameters>
```

Sample success responses

`XML` format

```
<PageNumber>1</PageNumber>
<TotalCount>1</TotalCount>
<PageSize>30</PageSize>
<RequestId>D1FF92B8-3714-4182-BA0B-D04F917F0463</RequestId>
<DBInstances>
    <DBInstance>
        <ChargeType>PostPaid</ChargeType>
        <LockMode>Unlock</LockMode>
        <DBInstanceClass>dds.mongo.logic</DBInstanceClass>
        <ResourceGroupId>rg-acxxxxxxxx</ResourceGroupId>
        <DBInstanceId>dds-bpxxxxxxxx</DBInstanceId>
        <ZoneId>cn-hangzhou-i</ZoneId>
        <MongosList>
            <MongosAttribute>
                <NodeId>s-bpxxxxxxxx</NodeId>
                <NodeClass>dds.mongos.mid</NodeClass>
            </MongosAttribute>
            <MongosAttribute>
                <NodeId>s-bpxxxxxxxx</NodeId>
                <NodeClass>dds.mongos.mid</NodeClass>
            </MongosAttribute>
        </MongosList>
        <DBInstanceDescription>testdata</DBInstanceDescription>
        <Engine>MongoDB</Engine>
        <CreationTime>2019-11-23T03:08:01Z</CreationTime>
        <Tags>
        </Tags>
        <NetworkType>VPC</NetworkType>
        <ExpireTime>2999-09-08T16:00Z</ExpireTime>
        <DBInstanceType>sharding</DBInstanceType>
        <RegionId>cn-hangzhou</RegionId>
        <ShardList>
            <ShardAttribute>
                <NodeId>d-bpxxxxxxxx</NodeId>
                <NodeClass>dds.shard.standard</NodeClass>
                <NodeStorage>10</NodeStorage>
            </ShardAttribute>
            <ShardAttribute>
                <NodeId>d-bpxxxxxxxx</NodeId>
                <NodeClass>dds.shard.standard</NodeClass>
                <NodeStorage>10</NodeStorage>
            </ShardAttribute>
        </ShardList>
        <EngineVersion>4.2</EngineVersion>
        <DBInstanceStatus>Running</DBInstanceStatus>
    </DBInstance>
</DBInstances>
```

`JSON` format

```
{
    "PageNumber": 1,
    "TotalCount": 1,
    "PageSize": 30,
    "RequestId": "D1FF92B8-3714-4182-BA0B-D04F917F0463",
    "DBInstances": {
        "DBInstance": [
            {
                "ChargeType": "PostPaid",
                "LockMode": "Unlock",
                "DBInstanceClass": "dds.mongo.logic",
                "ResourceGroupId": "rg-acxxxxxxxx",
                "DBInstanceId": "dds-bpxxxxxxxx",
                "ZoneId": "cn-hangzhou-i",
                "MongosList": {
                    "MongosAttribute": [
                        {
                            "NodeId": "s-bpxxxxxxxx",
                            "NodeClass": "dds.mongos.mid"
                        },
                        {
                            "NodeId": "s-bpxxxxxxxx",
                            "NodeClass": "dds.mongos.mid"
                        }
                    ]
                },
                "DBInstanceDescription": "testdata",
                "Engine": "MongoDB",
                "CreationTime": "2019-11-23T03:08:01Z",
                "Tags": {
                    "Tag": []
                },
                "NetworkType": "VPC",
                "ExpireTime": "2999-09-08T16:00Z",
                "DBInstanceType": "sharding",
                "RegionId": "cn-hangzhou",
                "ShardList": {
                    "ShardAttribute": [
                        {
                            "NodeId": "d-bpxxxxxxxx",
                            "NodeClass": "dds.shard.standard",
                            "NodeStorage": 10
                        },
                        {
                            "NodeId": "d-bpxxxxxxxx",
                            "NodeClass": "dds.shard.standard",
                            "NodeStorage": 10
                        }
                    ]
                },
                "EngineVersion": "4.2",
                "DBInstanceStatus": "Running"
            }
        ]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

