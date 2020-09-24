# DescribeReplicaSetRole

You can call this operation to query the role and connection information of a MongoDB instance.

This operation is applicable to replica set instances and sharded cluster instances. DescribeReplicaSetRole cannot be performed on standalone instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeReplicaSetRole&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeReplicaSetRole|The operation that you want to perform. Set the value to **DescribeReplicaSetRole**. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance. |
|RegionId|String|No|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~61933~~) to query. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|DB4A0595-FCA9-437F-B2BB-25DBFC009D3E|The ID of the request. |
|DBInstanceId|String|dds-bpxxxxxxxx|The ID of the instance. |
|ReplicaSets| | |The role list of the replica set. |
|ReplicaSet| | | |
|ConnectionDomain|String|dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com|The connection address of the node. |
|ConnectionPort|String|3717|The port of the node. |
|ExpiredTime|String|1209582|The remaining duration of the classic network address. Unit: seconds. |
|NetworkType|String|VPC|The network type. Valid values:

-   **VPC**
-   **Classic**
-   **Public** |
|ReplicaSetRole|String|Primary|The role of the node in the replica set.

-   **Primary**
-   **Secondary** |
|RoleId|String|651xxxxx|The role ID of the node. |

## Examples

Sample requests

```

http(s)://mongodb.aliyuncs.com/? Action=DescribeReplicaSetRole
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

```
<DescribeReplicaSetRoleResponse>
  <RequestId>7762D0FF-F34D-4DAF-9D06-6C1C28CC98CD</RequestId> 
  <DBInstanceId>dds-bpxxxxxxxx</DBInstanceId>
  <ReplicaSets>
    <ReplicaSet>
      <NetworkType>Classic</NetworkType>
      <ConnectionPort>3717</ConnectionPort>
      <ReplicaSetRole>Primary</ReplicaSetRole>
      <ConnectionDomain>dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com</ConnectionDomain>
      <ExpiredTime>12xxxxx</ExpiredTime>
      <RoleId>55xxxxx</RoleId>
    </ReplicaSet>
    <ReplicaSet>
      <NetworkType>Classic</NetworkType>
      <ConnectionPort>3717</ConnectionPort>
      <ReplicaSetRole>Secondary</ReplicaSetRole>
      <ConnectionDomain>dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com</ConnectionDomain>
      <ExpiredTime>12xxxxx</ExpiredTime>
      <RoleId>55xxxxx</RoleId>
    </ReplicaSet>
    <ReplicaSet>
      <NetworkType>VPC</NetworkType>
      <ConnectionPort>3717</ConnectionPort>
      <ReplicaSetRole>Primary</ReplicaSetRole>
      <ConnectionDomain>dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com</ConnectionDomain>
      <RoleId>55xxxxx</RoleId>
    </ReplicaSet>
    <ReplicaSet>
      <NetworkType>VPC</NetworkType>
      <ConnectionPort>3717</ConnectionPort>
      <ReplicaSetRole>Secondary</ReplicaSetRole>
      <ConnectionDomain>dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com</ConnectionDomain>
      <RoleId>55xxxxx</RoleId>
    </ReplicaSet>
  </ReplicaSets>
</DescribeReplicaSetRoleResponse>

```

`JSON` format

```
{
	"ReplicaSets":{
		"ReplicaSet":[
			{
				"NetworkType":"Classic",
				"ConnectionPort":"3717",
				"ReplicaSetRole":"Primary",
				"ConnectionDomain":"dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com",
				"ExpiredTime":"12xxxxx",
				"RoleId":"55xxxxx"
			},
			{
				"NetworkType":"Classic",
				"ConnectionPort":"3717",
				"ReplicaSetRole":"Secondary",
				"ConnectionDomain":"dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com",
				"ExpiredTime":"12xxxxx",
				"RoleId":"55xxxxx"
			},
			{
				"NetworkType":"VPC",
				"ConnectionPort":"3717",
				"ReplicaSetRole":"Primary",
				"ConnectionDomain":"dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com",
				"RoleId":"55xxxxx"
			},
			{
				"NetworkType":"VPC",
				"ConnectionPort":"3717",
				"ReplicaSetRole":"Secondary",
				"ConnectionDomain":"dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com",
				"RoleId":"55xxxxx"
			}
		]
	},
	"DBInstanceId":"dds-bpxxxxxxxx",
	"RequestId":"7762D0FF-F34D-4DAF-9D06-6C1C28CC98CD"
}
```

## Error codes

[View error codes](https://error-center.aliyun.com/status/product/Dds)

