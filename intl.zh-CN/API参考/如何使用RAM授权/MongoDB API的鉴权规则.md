# MongoDB API的鉴权规则

当子用户通过MongoDB OpenAPI进行资源访问时，MongoDB后台向RAM进行权限检查，以确保调用者拥有响应权限。

每个不同的MongoDB API会根据涉及到的资源以及API的语义来确定需要检查哪些资源的权限。具体每个API的鉴权规则见下表。

|Action|鉴权规则|
|:-----|:---|
|dds:CreateDBInstance|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:ModifyDBInstanceSpec|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:DeleteDBInstance|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:RenewDBInstance|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:CreateShardingDBInstance|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:DeleteNode|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:CreateNode|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:ModifyNodeSpec|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:DescribeDBInstances|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:RestartDBInstance|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:ModifyDBInstanceMaintainTime|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:ModifyDBInstanceDescription|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:DescribeDBInstanceAttribute|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:DescribeReplicaSetRole|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:DescribeShardingNetworkAddress|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:ModifyDBInstanceNetworkType|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:ModifyDBInstanceNetExpireTime|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:DescribeDBInstancePerformance|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:DescribeAccounts|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:ResetAccountPassword|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:DescribeSecurityIps|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:ModifySecurityIps|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:DescribeAuditRecords|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:DescribeAuditFiles|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:DescribeBackupPolicy|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:ModifyBackupPolicy|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:CreateBackup|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:RestoreDBInstance|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:DescribeBackups|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|
|dds:DescribeDBInstancePerformance|acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid|

