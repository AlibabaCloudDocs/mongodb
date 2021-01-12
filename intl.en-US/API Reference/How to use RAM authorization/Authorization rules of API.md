# Authorization rules of API

When a subaccount accesses resources through ApsaraDB for MongoDB API, the ApsaraDB for MongoDB background performs a permission verification on RAM to make sure that the caller has relevant permissions.

Each ApsaraDB for MongoDB API determines the resource permissions that need to be checked based on the involved resources and the API semantics. The authorization rules for each API are shown in the following table.

|Operation name|Authentication rule|
|:-------------|:------------------|
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

