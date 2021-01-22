# Details of the DBInstances parameter in the DescribePrice operation

This topic describes the detailed parameters of the DBInstances parameter that is used in the DescribePrice operation. You can call the DescribePrice operation to query the fees incurred when you create, upgrade, or renew an ApsaraDB for MongoDB instance.

|Parameter|Type|Required|Description|Example|
|---------|----|--------|-----------|-------|
|DBInstanceId|String|No|The ID of the instance. You can call the [DescribeDBInstances](~~61939~~) operation to query the list of one or more ApsaraDB for MongoDB instances. This parameter is required when the **OrderType** parameter is set to **UPGRADE** or **RENEW**.|dds-bp1xxxxxxxxxxxxx|
|RegionId|String|Yes|The region ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query available regions.|cn-hangzhou|
|ZoneId|String|Yes|The zone ID of the instance. You can call the [DescribeRegions](~~61933~~) operation to query available zones.|cn-hangzhou-h|
|Engine|String|Yes|The database engine that the instance runs. Set the value to **MongoDB**.|MongoDB|
|EngineVersion|String|Yes|The version of the database engine. Valid values:-   **3.4**
-   **4.0**
-   **4.2**

|4.2|
|DBInstanceClass|String|No|The instance type. For more information, see [Instance types](~~57141~~).|dds.mongo.mid|
|DBInstanceStorage|String|Yes|The storage capacity of the instance. Unit: GB.|20|
|ReplicationFactor|String|No|The number of nodes in the instance. Valid values:-   **1**
-   **3**
-   **5**
-   **7**

|3|
|NetworkType|String|No|The network type of the instance. Valid values:-   **VPC**
-   **Classic**

Default value: **Classic**.

|VPC|
|VPCId|String|No|The ID of the VPC. This parameter is required when the **NetworkType** parameter is set to **VPC**.|vpc-bp1xxxxxxxxxxxxxx|
|VSwitchId|String|No|The ID of the vSwitch. This parameter is required when the **NetworkType** parameter is set to **VPC**.|vsw-bp1xxxxxxxxxxxxxx|
|ChargeType|String|No|The billing method of the instance. Valid values:-   **PostPaid**: pay-as-you-go
-   **PrePaid**: subscription

|PostPaid|
|AutoPay|String|No|Specifies whether to enable auto-renewal for the instance. Valid values:-   **True**: enables auto-renewal for the instance.
-   **False**: disables auto-renewal for the instance.

|True|
|Period|String|No|The subscription period of the instance. Unit: months. This parameter is required when the **ChargeType** parameter is set to **PrePaid**.|1|
|configServers|JSON|No|The specifications of the Configserver nodes in a sharded cluster instance. Subparameters:-   **nodeClass**: the instance type of the Configserver nodes.
-   **nodeStorage**: the storage capacity of the Configserver nodes.

Set the value to `[{"nodeClass":"dds.cs.mid","nodeStorage":"20"}]`.|\[\{"nodeClass":"dds.cs.mid","nodeStorage":"20"\}\]|
|mongos|JSON|No|The specifications of the mongos nodes in a sharded cluster instance. For more information, see [Instance types](~~57141~~). Subparameter:-   **nodeClass**: the instance types of the mongos nodes.

|\[\{"nodeClass":"dds.mongos.mid"\},\{"nodeClass":"dds.mongos.mid"\}\]|
|shards|JSON|No|The specifications of the shard nodes in a sharded cluster instance. For more information, see [Instance types](~~57141~~). Subparameters:-   **nodeClass**: the instance types of the shard nodes.
-   **nodeStorage**: the storage capacity of the shard nodes.
-   **ReadonlyReplicas**: the number of read-only nodes. Valid values: **0**, **1**, **2**, **3**, **4**, and **5**.

|\[\{"nodeClass":"dds.shard.mid","ReadonlyReplicas":"1","nodeStorage":"10"\},\{"nodeClass":"dds.shard.mid","ReadonlyReplicas":"1","nodeStorage":"10"\}\]|

