# DescribeReplicaSetRole {#doc_api_Dds_DescribeReplicaSetRole .reference}

You can call this operation to query the role and connection information of a MongoDB instance.

This operation is applicable to replica set instances and sharded cluster instances. DescribeReplicaSetRole cannot be performed on standalone instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Dds&api=DescribeReplicaSetRole) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeReplicaSetRole|The operation that you want to perform. Set the value to **DescribeReplicaSetRole**.

 |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

 |
|AccessKeyId|String|No|LTAIgbTGpxxxxxx|The AccessKey ID provided to you by Alibaba Cloud.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|DB4A0595-FCA9-437F-B2BB-25DBFC009D3E|The ID of the request.

 |
|DBInstanceId|String|dds-bpxxxxxxxx|The ID of the instance.

 |
|ReplicaSets| | |The role list of the replica set.

 |
|└ConnectionDomain|String|dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com|The connection address of the node.

 |
|└ConnectionPort|String|3717|The port of the node.

 |
|└ExpiredTime|String|1209582|The remaining duration of the classic network address. Unit: seconds.

 |
|└NetworkType|String|VPC|The network type. Valid values:

 -   **VPC**
-   **Classic**
-   **Public**

 |
|└ReplicaSetRole|String|Primary|The role of the node in the replica set.

 -   **Primary**
-   **Secondary**

 |
|└RoleId|String|651xxxxx|The role ID of the node.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://mongodb.aliyuncs.com/? Action=DescribeReplicaSetRole
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
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

``` {#json_return_success_demo}
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

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Dds)

