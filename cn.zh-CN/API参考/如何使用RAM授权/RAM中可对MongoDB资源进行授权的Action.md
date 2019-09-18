# RAM中可对MongoDB资源进行授权的Action {#concept_61756_zh .concept}

在RAM中，可以对一个MongoDB资源进行以下Action的授权。

|Action|Action|
|:-----|:-----|
|CreateDBInstance|ModifyDBInstanceSpec|
|DeleteDBInstance|RenewDBInstance|
|CreateShardingDBInstance|DeleteNode|
|ModifyNodeSpec|CreateNode|
|RestartDBInstance|ModifyDBInstanceMaintainTime|
|ModifyDBInstanceDescription|DescribeDBInstanceAttribute|
|DescribeReplicaSetRole|DescribeShardingNetworkAddress|
|ModifyDBInstanceNetworkType|ModifyDBInstanceNetExpireTime|
|DescribeAccounts|ResetAccountPassword|
|DescribeSecurityIps|ModifySecurityIps|
|DescribeAuditRecords|DescribeAuditFiles|
|DescribeBackupPolicy|ModifyBackupPolicy|
|CreateBackup|DescribeBackups|
|RestoreDBInstance|DescribeDBInstancePerformance|
|DescribeDBInstances|-|

其中DescribeDBInstances，授权时必须对该用户全部实例授权。不需要鉴权的接口为[DescribeRegions](intl.zh-CN/API参考/实例管理/DescribeRegions.md#)。

