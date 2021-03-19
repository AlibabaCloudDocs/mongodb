# DescribeDBInstances

You can call this operation to query the list of one or more MongoDB instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeDBInstances&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDBInstances|The operation that you want to perform. Set the value to **DescribeDBInstances**. |
|PageNumber|Integer|No|1|The number of the page to return. The value must be an integer that is larger than 0. Default value: **1**. |
|PageSize|Integer|No|30|The number of records on each page. Valid values: **30, 50, and 100**. Default value: **30**. |
|DBInstanceId|String|No|dds-bpxxxxxxxx|The ID of the instance. |
|ReplicationFactor|String|No|3|The number of nodes in a replica set instance. Valid values: **3, 5, and 7**. |
|DBInstanceDescription|String|No|testdatabase|The description of the instance. |
|DBInstanceStatus|String|No|ACTIVATION|The state of the instance. For more information about valid values, see [Instance states](~~63870~~). |
|DBInstanceType|String|No|replicate|The category of the instance. Valid values:

 -   **sharding**: sharded cluster instance
-   **replicate**: replica set or standalone instance |
|DBInstanceClass|String|No|dds.mongo.mid|The instance type. For more information about valid values, see [Instance types](~~57141~~). |
|Engine|String|No|MongoDB|The database engine of the instance. Valid value: **MongoDB**. |
|EngineVersion|String|No|4.0|The version of the database engine. Valid values: **3.2**, **3.4**, **4.0**, and **4.2**. |
|NetworkType|String|No|VPC|The network type of the instance. Valid values:

 -   **Classic**
-   **VPC** |
|VpcId|String|No|vpc-bpxxxxxxxx|The VPC ID of the instance. |
|VSwitchId|String|No|vsw-bpxxxxxxxx|The vSwitch ID of the instance. |
|ChargeType|String|No|PrePaid|The billing method of the instance. Valid values:

 -   **PrePaid**: subscription
-   **PostPaid**: pay-as-you-go |
|ZoneId|String|No|cn-hangzhou-b|The zone ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the most recent zone list. |
|Tag.N.Key|String|No|testdatabase|The tag key of the instance. Valid values of N: **1** to **20**. The tag key can be up to 64 characters in length. It cannot start with `aliyun`, `acs:`, `http://`, or `https://`.

 **Note:** The Tag.N.Key parameter cannot be an empty string. |
|Tag.N.Value|String|No|apitest|The tag value of the instance. Valid values of N: **1** to **20**. The tag value can be up to 128 characters in length. It cannot start with `aliyun`, `acs:`, `http://`, or `https://`.

 **Note:** The Tag.N.Value parameter can be an empty string. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query the region ID of the instance. |
|ExpireTime|String|No|2019-12-26T16:00Z|The time when the instance expires. |
|Expired|String|No|true|Specifies whether the instance is expired. Valid values:

 -   **true**
-   **false** |
|ConnectionDomain|String|No|dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com|The endpoint of the node. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the endpoint of the node. |
|ResourceGroupId|String|No|rg-axxxxxxxx|The ID of the resource group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the returned page. |
|TotalCount|Integer|1|The number of the instances in the query results. |
|PageSize|Integer|30|The number of entries returned per page. |
|RequestId|String|A10B8ECB-0BA0-4EC6-93A5-C65FDEDA07CB|The ID of the request. |
|DBInstances|Array of DBInstance| |Details about the instances. |
|DBInstance| | | |
|ChargeType|String|PostPaid|The billing method of the instance.

 -   **PrePaid**: subscription
-   **PostPaid**: pay-as-you-go |
|CreationTime|String|2018-09-25T06:33:07Z|The time when the instance was created. The time is in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|DBInstanceClass|String|dds.mongo.mid|The instance type. |
|DBInstanceDescription|String|testdatabase|The description of the instance. |
|DBInstanceId|String|dds-bpxxxxxxxx|The ID of the instance. |
|DBInstanceStatus|String|Running|The state of the instance. For more information about valid values, see [Instance states](~~63870~~). |
|DBInstanceStorage|Integer|20|The storage capacity of the instance. |
|DBInstanceType|String|sharding|The category of the instance.

 -   **sharding**: sharded cluster instance
-   **replicate**: replica set instance |
|DestroyTime|String|2019-03-05T11:26:02Z|The time when the instance was released. The time is in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time must be in UTC.

 **Note:**

-   Subscription instances are released seven days after expiration. After an instance is released, its data is deleted and cannot be restored.
-   Pay-as-you-go instances are locked after the payment is overdue for more than 24 hours. The instance is released after it is overdue for more than seven days. The data of released instances is deleted and cannot be restored. |
|Engine|String|MongoDB|The database engine of the instance. |
|EngineVersion|String|4.0|The version of the database engine. |
|ExpireTime|String|2019-11-25T16:00Z|The time when the instance expires. The time is in the *yyyy-MM-dd*T*HH:mm*Z format. The time is displayed in UTC. |
|KindCode|String|1|The kind code of the instance. Valid values:

 -   **0**: physical machine
-   **1**: Elastic Compute Service \(ECS\)
-   **2**: Docker cluster
-   **18**: Kubernetes cluster |
|LastDowngradeTime|String|2019-03-08|The last time when the instance was downgraded. |
|LockMode|String|Unlock|Indicates whether the instance is locked.

 -   **Unlock**: The instance is not locked.
-   **ManualLock**: The instance is manually locked.
-   **LockByExpiration**: The instance is locked upon expiration.
-   **LockByRestoration**: The instance is locked for a rollback.
-   **LockByDiskQuota**: The instance is automatically locked because the storage space is exhausted.
-   **Released**: The instance is released. You cannot unlock an instance that has been released. After an instance is released, you can only use a backup to restore the data of the instance to a new instance. This process requires a long period of time. |
|MongosList|Array of MongosAttribute| |Details about the mongos nodes.

 **Note:** This parameter is returned if the instance is a sharded cluster instance. |
|MongosAttribute| | | |
|NodeClass|String|dds.mongos.mid|The specifications of the mongos node. |
|NodeDescription|String|testmongos|The description of the mongos node. |
|NodeId|String|s-bpxxxxxxxx|The ID of the mongos node. |
|NetworkType|String|VPC|The network type of the instance. Valid values:

 -   **Classic**
-   **VPC** |
|RegionId|String|cn-hangzhou|The region ID of the instance. |
|ReplicationFactor|String|3|The number of the nodes in the instance.

 **Note:** This parameter is returned if the instance is a replica set instance. |
|ResourceGroupId|String|rg-axxxxxxxx|The ID of the resource group. |
|ShardList|Array of ShardAttribute| |Details about the shard nodes.

 **Note:** This parameter is returned if the instance is a sharded cluster instance. |
|ShardAttribute| | | |
|NodeClass|String|dds.shard.mid|The specifications of the shard node. |
|NodeDescription|String|testshardnode|The description of the shard node. |
|NodeId|String|d-bpxxxxxxxx|The ID of the shard node. |
|NodeStorage|Integer|20|The storage capacity of the shard node. Unit: GB. |
|ReadonlyReplicas|Integer|1|The number of read-only nodes in the shard node. Valid values: **0** to **5**.

 **Note:** This parameter is available only for ApsaraDB for MongoDB instances that are purchased on the Alibaba Cloud China site. |
|Tags|Array of Tag| |Details about the resource tags. |
|Tag| | | |
|Key|String|test|The tag key of the resource. |
|Value|String|api|The tag value of the resource. |
|VpcAuthMode|String|Close|Indicates whether password-free access within the VPC is enabled. Valid values:

 -   **Open**: Password-free access is enabled.
-   **Close**: Password-free access is disabled. |
|ZoneId|String|cn-hangzhou-b|The zone ID of the instance. |

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

