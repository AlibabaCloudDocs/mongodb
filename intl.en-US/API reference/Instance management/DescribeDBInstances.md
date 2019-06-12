# DescribeDBInstances {#doc_api_Dds_DescribeDBInstances .reference}

You can call this operation to query the list of MongoDB instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeDBInstances) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDBInstances|The operation that you want to perform. Set the value to **DescribeDBInstances**.

 |
|PageNumber|Integer|No|1|The number of the page. Valid values: any non-zero positive integer. Default value: **1**.

 |
|PageSize|Integer|No|30|The number of records on each page. Valid values: **30, 50, and 100**. Default value: **30**.

 |
|DBInstanceId|String|No|dds-bpxxxxxxxx|The ID of the instance.

 |
|ReplicationFactor|String|No|3|The number of nodes in a replica set instance. Valid values: **3, 5, and 7**.

 |
|DBInstanceDescription|String|No|Test database|The description or remarks of the instance.

 |
|DBInstanceStatus|String|No|ACTIVATION|The status information of the instance. For more information about valid values, see [Instance states](~~63870~~).

 |
|DBInstanceType|String|No|Replicate|The instance type. Valid values:

 -   **sharding**: sharded cluster instances.
-   **replicate**: replica set or standalone instances. This is the default value.

 |
|DBInstanceClass|String|No|dds.mongo.mid|The instance type. For more information about valid values, see [Instance types](~~57141~~).

 |
|Engine|String|No|MongoDB|The database engine. Valid value: **MongoDB**.

 |
|EngineVersion|String|No|4.0|The database version of the instance.

 |
|NetworkType|String|No|VPC|The network type of the instances. Valid values:

 -   **Classic**
-   **VPC**

 |
|VpcId|String|No|vpc-bpxxxxxxxx|The ID of the VPC.

 |
|VSwitchId|String|No|vsw-bpxxxxxxxx|The VSwitch ID of the VPC.

 |
|ChargeType|String|No|PrePaid|The billing method of the instance. Valid values:

 -   **PrePaid**: monthly or yearly subscription.
-   **PostPaid**: pay-as-you-go.

 |
|ZoneId|String|No|cn-hangzhou-b|The zone ID.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |
|Tag.N.Key|String|No|testdatabase|The key of the tag. Valid values of N: **1** to **20**. It can be up to 64 characters in length. It cannot begin with aliyun, acs:, http://, or https://.

 **Note:** It cannot be an empty string.

 |
|Tag.N.Value|String|No|apitest|The value of the tag. Valid values of N: **1** to **20**. It can be a maximum of 128 characters in length. It cannot start with aliyun, acs:, http://, or https://.

 **Note:** Tag.N.Value can be an empty string.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The number of the page.

 |
|TotalCount|Integer|1|The number of the instances in the query results.

 |
|PageSize|Integer|30|The number of records to display on each page.

 |
|RequestId|String|A10B8ECB-0BA0-4EC6-93A5-C65FDEDA07CB|The ID of the request.

 |
|DBInstances| | |The list of the instances.

 |
|└ChargeType|String|PostPaid|The billing method of the instance.

 -   **PrePaid**: monthly or yearly subscription.
-   **PostPaid**: pay-as-you-go.

 |
|└CreationTime|String|2018-09-25T06:33:07Z|The creation time of the instance. The time is in the *yyyy-MM-dd*T*HH: mm: ss*Z format.

 |
|└DBInstanceClass|String|dds.mongo.mid|The instance type

 |
|└DBInstanceDescription|String|Test database|The description or remarks of the instance.

 |
|└DBInstanceId|String|dds-bpxxxxxxxx|The ID of the instance.

 |
|└DBInstanceStatus|String|Running|The state of the instance. For more information, see [Instance states](~~63870~~).

 |
|└DBInstanceStorage|Integer|20|The storage space of the instance.

 |
|└DBInstanceType|String|sharding|The instance type.

 -   **sharding**: sharded cluster instances.
-   **replicate**: replica set instances.

 |
|└DestroyTime|String|2019-03-05T11:26:02Z|The release time of the instance. The time is in the *yyyy-MM-dd*T*HH:mm:ss*Z format.

 **Note:** 

-   Subscription instances will be released seven days after expiration. The data of released instances will be deleted and cannot be recovered.
-   Pay-as-you-go instances will be locked when the payment is overdue for more than 24 hours. The instance will be released when it is overdue for more than seven days. The data of released instances will be deleted and cannot be recovered.

 |
|└Engine|String|MongoDB|The database engine.

 |
|└EngineVersion|String|4.0|The version of the database.

 |
|└ExpireTime|String|2019-11-25T16:00Z|The expiration time of the instance.

 |
|└LastDowngradeTime|String|2019-03-08|The last time the instance was downgraded.

 |
|└LockMode|String|Unlock|The lock status of the instance.

 -   **Unlock**: The instance is not locked.
-   **ManualLock**: The instance has been manually locked.
-   **LockByExpiration**: The instance has been locked because it has expired.
-   **LockByRestoration**: The instance has been locked before rollback.
-   **LockByDiskQuota**: The instance has been locked because its capacity is full.
-   **Released**: The instance has been released. When the instance is in the released state, it cannot be unlocked. If you want to restore the instance, you can only use backup data to create a new instance. Creating an instance from backup data takes a long time.

 |
|└MongosList| | |The list of mongos.

 **Note:** This parameter is returned when the instance is a sharded cluster instance.

 |
|└NodeClass|String|dds.mongos.mid|The specifications of the mongos.

 |
|└NodeDescription|String|Test mongos|The description of the mongos.

 |
|└NodeId|String|s-bpxxxxxxxx|The ID of the mongos.

 |
|└NetworkType|String|VPC|The network type of the instance.

 -   **Classic**
-   **VPC**

 |
|└RegionId|String|cn-hangzhou|The ID of the region to which the instance belongs.

 |
|└ReplicationFactor|String|3|The number of the nodes in the instance.

 **Note:** This parameter is returned when the instance is a replica set instance.

 |
|└ResourceGroupId|String|rg-axxxxxxxx|The ID of the resource group.

 |
|└ShardList| | |The list of shards.

 **Note:** This parameter is returned when the instance is a sharded cluster instance.

 |
|└NodeClass|String|dds.shard.mid|The instance type of the shard.

 |
|└NodeDescription|String|Test shard node|The description of the shard.

 |
|└NodeId|String|d-bpxxxxxxxx|The ID of the shard.

 |
|└NodeStorage|Integer|20|The storage space of the shard. Unit: GB.

 |
|└Tags| | |The resource tag information list.

 |
|└Key|String|test|The tag key of the resource.

 |
|└Value|String|api|The tag value of the resource.

 |
|└ZoneId|String|cn-hangzhou-b|The ID of the zone to which the instance belongs.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeDBInstances
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeDBInstancesResponse>
  <PageNumber>1</PageNumber>
  <TotalCount>1</TotalCount>
  <PageSize>30</PageSize>
  <RequestId>5E182ACD-6283-48BE-B2E6-0890BC123F8B</RequestId>
  <DBInstances>
    <DBInstance>
      <ChargeType>PostPaid</ChargeType> 
      <LockMode>Unlock</LockMode> 
      <DBInstanceClass>dds.mongo.logic</DBInstanceClass> 
      <DBInstanceId>dds-bpxxxxxxxx</DBInstanceId> 
      <ZoneId>cn-hangzhou-b</ZoneId>
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
      <Engine>MongoDB</Engine>
      <CreationTime>2019-03-07T06:06:00Z</CreationTime>
      <NetworkType>Classic</NetworkType>
      <ExpireTime>2999-09-08T16:00Z</ExpireTime>
      <RegionId>cn-hangzhou</RegionId>
      <DBInstanceType>sharding</DBInstanceType>
      <ShardList>
        <ShardAttribute>
          <NodeId>d-bpxxxxxxxx</NodeId>
          <NodeClass>dds.shard.standard</NodeClass>
          <NodeStorage>20</NodeStorage>
        </ShardAttribute>
        <ShardAttribute>
          <NodeId>d-bpxxxxxxxx</NodeId>
          <NodeClass>dds.shard.mid</NodeClass>
          <NodeStorage>10</NodeStorage>
        </ShardAttribute>
      </ShardList>
      <EngineVersion>3.4</EngineVersion>
      <DBInstanceStatus>Running</DBInstanceStatus>
    </DBInstance>
  </DBInstances>
</DescribeDBInstancesResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":30,
	"RequestId":"5E182ACD-6283-48BE-B2E6-0890BC123F8B",
	"DBInstances":{
		"DBInstance":[
			{
				"ChargeType":"PostPaid",
				"LockMode":"Unlock",
				"DBInstanceClass":"dds.mongo.logic",
				"DBInstanceId":"dds-bpxxxxxxxx",
				"ZoneId":"cn-hangzhou-b",
				"MongosList":{
					"MongosAttribute":[
						{
							"NodeId":"s-bpxxxxxxxx",
							"NodeClass":"dds.mongos.mid"
						},
						{
							"NodeId":"s-bpxxxxxxxx",
							"NodeClass":"dds.mongos.mid"
						}
					]
				},
				"Engine":"MongoDB",
				"CreationTime":"2019-03-07T06:06:00Z",
				"NetworkType":"Classic",
				"ExpireTime":"2999-09-08T16:00Z",
				"RegionId":"cn-hangzhou",
				"DBInstanceType":"sharding",
				"ShardList":{
					"ShardAttribute":[
						{
							"NodeId":"d-bpxxxxxxxx",
							"NodeClass":"dds.shard.standard",
							"NodeStorage":20
						},
						{
							"NodeId":"d-bpxxxxxxxx",
							"NodeClass":"dds.shard.mid",
							"NodeStorage":10
						}
					]
				},
				"EngineVersion":"3.4",
				"DBInstanceStatus":"Running"
			}
		]
	}
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

