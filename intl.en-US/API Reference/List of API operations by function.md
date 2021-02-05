# List of API operations by function

The following tables list API operations available for use in ApsaraDB for MongoDB.

## Lifecycle management

|API|Description|
|---|-----------|
|[CreateDBInstance](/intl.en-US/API Reference/Lifecycle management/CreateDBInstance.md)|Creates and clones replica set instances of ApsaraDB for MongoDB.|
|[ModifyDBInstanceSpec](/intl.en-US/API Reference/Lifecycle management/ModifyDBInstanceSpec.md)|Modifies the specifications or storage space of an ApsaraDB for MongoDB instance.|
|[DeleteDBInstance](/intl.en-US/API Reference/Lifecycle management/DeleteDBInstance.md)|Releases an ApsaraDB for MongoDB instance.|
|[CreateShardingDBInstance](/intl.en-US/API Reference/Lifecycle management/CreateShardingDBInstance.md)|Creates or clones ApsaraDB for MongoDB sharded cluster instances.|
|[CreateNode](/intl.en-US/API Reference/Lifecycle management/CreateNode.md)|Creates shards or mongos for an ApsaraDB for MongoDB sharded cluster instance.|
|[DeleteNode](/intl.en-US/API Reference/Lifecycle management/DeleteNode.md)|Deletes a shard or mongos in a sharded cluster instance of ApsaraDB for MongoDB.|
|[ModifyNodeSpec](/intl.en-US/API Reference/Lifecycle management/ModifyNodeSpec.md)|Modifies the type and storage space of a specified node in an ApsaraDB for MongoDB sharded cluster instance.|
|[DescribeInstanceAutoRenewalAttribute](/intl.en-US/API Reference/Lifecycle management/DescribeInstanceAutoRenewalAttribute.md)|Queries whether auto-renewal is enabled for an ApsaraDB for MongoDB instance.|

## Region management

|API|Description|
|---|-----------|
|[MigrateToOtherZone](/intl.en-US/API Reference/Region management/MigrateToOtherZone.md)|Migrates an ApsaraDB for MongoDB instance to another zone.|
|[DescribeRegions](/intl.en-US/API Reference/Region management/DescribeRegions.md)|Views the regions and zones that an ApsaraDB for MongoDB instance can be created.|
|[MigrateAvailableZone](/intl.en-US/API Reference/Region management/MigrateAvailableZone.md)|Changes the zone of an ApsaraDB for MongoDB instance.|

## Resource Management

|API|Description|
|---|-----------|
|[EvaluateResource](/intl.en-US/API Reference/Resource Management/EvaluateResource.md)|Checks whether sufficient resources are available in the region where you want to create or upgrade an ApsaraDB for MongoDB instance.|
|[DescribeAvailableResource](/intl.en-US/API Reference/Resource Management/DescribeAvailableResource.md)|Queries the types of instances that can be created in specified zones.|

## Connection management

|API|Description|
|---|-----------|
|[AllocatePublicNetworkAddress](/intl.en-US/API Reference/Connection Management/AllocatePublicNetworkAddress.md)|Assigns a public endpoint to an ApsaraDB for MongoDB instance.|
|[ReleasePublicNetworkAddress](/intl.en-US/API Reference/Connection Management/ReleasePublicNetworkAddress.md)|Releases the public IP address of an ApsaraDB for MongoDB instance.|
|[ModifyInstanceVpcAuthMode](/intl.en-US/API Reference/Connection Management/ModifyInstanceVpcAuthMode.md)|Enables or disables authentication for an ApsaraDB for MongoDB instance to allow access from the same VPC as the instance.|
|[DescribeShardingNetworkAddress](/intl.en-US/API Reference/Connection Management/DescribeShardingNetworkAddress.md)|Queries the connection information of sharded cluster instances of ApsaraDB for MongoDB.|
|[ModifyDBInstanceNetworkType](/intl.en-US/API Reference/Connection Management/ModifyDBInstanceNetworkType.md)|Changes the network type of an ApsaraDB for MongoDB instance.|
|[ModifyDBInstanceConnectionString](/intl.en-US/API Reference/Connection Management/ModifyDBInstanceConnectionString.md)|Modifies the connection string of an ApsaraDB for MongoDB instance.|
|[ReleaseNodePrivateNetworkAddress](/intl.en-US/API Reference/Connection Management/ReleaseNodePrivateNetworkAddress.md)|Releases the internal endpoint of the shard or Configserver node of a sharded cluster instance.|
|[AllocateNodePrivateNetworkAddress](/intl.en-US/API Reference/Connection Management/AllocateNodePrivateNetworkAddress.md)|Applies for an internal endpoint for the shard or Configserver node of an ApsaraDB for MongoDB sharded cluster instance.|

## Queries the information of an instance.

|API|Description|
|---|-----------|
|[DescribeReplicaSetRole](/intl.en-US/API Reference/Querying Instance Information/DescribeReplicaSetRole.md)|Queries the role and connection information of an ApsaraDB for MongoDB instance.|
|[DescribeKernelReleaseNotes](/intl.en-US/API Reference/Querying Instance Information/DescribeKernelReleaseNotes.md)|Queries the release notes of the minor database versions of an ApsaraDB for MongoDB instance.|
|[DescribeAvailableEngineVersion](/intl.en-US/API Reference/Querying Instance Information/DescribeAvailableEngineVersion.md)|Queries the engine versions to which an ApsaraDB for MongoDB instance can be upgraded.|
|[DescribeDBInstances](/intl.en-US/API Reference/Querying Instance Information/DescribeDBInstances.md)|Queries the list of ApsaraDB for MongoDB instances.|
|[DescribeDBInstanceAttribute](/intl.en-US/API Reference/Querying Instance Information/DescribeDBInstanceAttribute.md)|Queries the details of an ApsaraDB for MongoDB instance.|
|[DescribeRoleZoneInfo](/intl.en-US/API Reference/Querying Instance Information/DescribeRoleZoneInfo.md)|Views the roles and zones of nodes in an ApsaraDB for MongoDB instance.|
|[DescribeActiveOperationTaskCount](/intl.en-US/API Reference/Querying Instance Information/DescribeActiveOperationTaskCount.md)|Queries the number of O&M tasks on an ApsaraDB for MongoDB instance.|
|[DescribeActiveOperationTaskType](/intl.en-US/API Reference/Querying Instance Information/DescribeActiveOperationTaskType.md)|Queries the types of O&M tasks on an ApsaraDB for MongoDB instance and the number of each type of tasks.|

## Instance management

|API|Description|
|---|-----------|
|[RestartDBInstance](/intl.en-US/API Reference/Instance management/RestartDBInstance.md)|Restarts an ApsaraDB for MongoDB instance.|
|[ModifyDBInstanceMaintainTime](/intl.en-US/API Reference/Instance management/ModifyDBInstanceMaintainTime.md)|Modifies the maintenance window of an ApsaraDB for MongoDB instance.|
|[ModifyDBInstanceDescription](/intl.en-US/API Reference/Instance management/ModifyDBInstanceDescription.md)|Changes the name of an ApsaraDB for MongoDB instance.|
|[SwitchDBInstanceHA](/intl.en-US/API Reference/Instance management/SwitchDBInstanceHA.md)|Switches between the primary and secondary nodes in an ApsaraDB for MongoDB instance.|
|[UpgradeDBInstanceEngineVersion](/intl.en-US/API Reference/Instance management/UpgradeDBInstanceEngineVersion.md)|Upgrades the database version of an ApsaraDB for MongoDB instance.|
|[DestroyInstance](/intl.en-US/API Reference/Instance management/DestroyInstance.md)|Releases an ApsaraDB for MongoDB instance.|
|[UpgradeDBInstanceKernelVersion](/intl.en-US/API Reference/Instance management/UpgradeDBInstanceKernelVersion.md)|Upgrades the minor database version of an ApsaraDB for MongoDB instance.|
|[ModifyDBInstanceNetExpireTime](/intl.en-US/API Reference/Instance management/ModifyDBInstanceNetExpireTime.md)|Extends the retention period of the classic network of an ApsaraDB for MongoDB instance.|

## Tag management

|API|Description|
|---|-----------|
|[TagResources](/intl.en-US/API Reference/Tag management/TagResources.md)|Binds tags to one or more ApsaraDB for MongoDB instances.|
|[ListTagResources](/intl.en-US/API Reference/Tag management/ListTagResources.md)|Queries the binding relationship between ApsaraDB for MongoDB instances and tags.|
|[DescribeTags](/intl.en-US/API Reference/Tag management/DescribeTags.md)|Queries all tags in a specified region.|
|[UntagResources](/intl.en-US/API Reference/Tag management/UntagResources.md)|Unbinds a tag from an instance. If the tag is not bound to another instance, the tag is deleted.|

## Account management

|API|Description|
|---|-----------|
|[DescribeAccounts](/intl.en-US/API Reference/Account management/DescribeAccounts.md)|Queries the database accounts of an ApsaraDB for MongoDB instance.|
|[ResetAccountPassword](/intl.en-US/API Reference/Account management/ResetAccountPassword.md)|Resets the password of the root account of an ApsaraDB for MongoDB instance.|
|[ModifyAccountDescription](/intl.en-US/API Reference/Account management/ModifyAccountDescription.md)|Modifies the description of the root account of an ApsaraDB for MongoDB instance.|

## Whitelists and security groups

|API|Description|
|---|-----------|
|[DescribeSecurityGroupConfiguration](/intl.en-US/API Reference/IP Whitelist and Security Groups/DescribeSecurityGroupConfiguration.md)|Queries the ECS security groups associated with an ApsaraDB for MongoDB instance.|
|[ModifySecurityGroupConfiguration](/intl.en-US/API Reference/IP Whitelist and Security Groups/ModifySecurityGroupConfiguration.md)|Modifies the ECS security group that is bound to the ApsaraDB for MongoDB instance.|
|[DescribeSecurityIps](/intl.en-US/API Reference/IP Whitelist and Security Groups/DescribeSecurityIps.md)|Queries the IP address whitelist of an ApsaraDB for MongoDB instance.|
|[ModifySecurityIps](/intl.en-US/API Reference/IP Whitelist and Security Groups/ModifySecurityIps.md)|Modifies the IP address whitelist of an ApsaraDB for MongoDB instance.|

## Keys

|API|Description|
|---|-----------|
|[CheckCloudResourceAuthorized](/intl.en-US/API Reference/Encription Keys/CheckCloudResourceAuthorized.md)|Checks whether KMS keys are authorized to ApsaraDB for MongoDB instances.|
|[DescribeUserEncryptionKeyList](/intl.en-US/API Reference/Encription Keys/DescribeUserEncryptionKeyList.md)|Queries the list of custom keys for an ApsaraDB for MongoDB instance.|
|[DescribeDBInstanceEncryptionKey](/intl.en-US/API Reference/Encription Keys/DescribeDBInstanceEncryptionKey.md)|Queries the details of a key for an ApsaraDB for MongoDB instance.|
|[DescribeDBInstanceTDEInfo](/intl.en-US/API Reference/Encription Keys/DescribeDBInstanceTDEInfo.md)|Queries whether TDE is enabled for an ApsaraDB for MongoDB instance.|
|[ModifyDBInstanceTDE](/intl.en-US/API Reference/Encription Keys/ModifyDBInstanceTDE.md)|Modifies the transparent data encryption \(TDE\) status of an ApsaraDB for MongoDB instance.|

## SSL encryption

|API|Description|
|---|-----------|
|[ModifyDBInstanceSSL](/intl.en-US/API Reference/SSL encryption/ModifyDBInstanceSSL.md)|Modifies the SSL configuration of an ApsaraDB for MongoDB instance.|
|[DescribeDBInstanceSSL](/intl.en-US/API Reference/SSL encryption/DescribeDBInstanceSSL.md)|Queries the SSL settings of an ApsaraDB for MongoDB instance.|

## Audit logs

|API|Description|
|---|-----------|
|[DescribeAuditRecords](/intl.en-US/API Reference/Audit Logs/DescribeAuditRecords.md)|Queries the audit log of an ApsaraDB for MongoDB instance.|
|[DescribeAuditFiles]()|Queries the audit log files of an ApsaraDB for MongoDB instance.|
|[DescribeAuditPolicy](/intl.en-US/API Reference/Audit Logs/DescribeAuditPolicy.md)|Queries whether the audit log feature is enabled for an ApsaraDB for MongoDB instance.|
|[ModifyAuditLogFilter](/intl.en-US/API Reference/Audit Logs/ModifyAuditLogFilter.md)|Modifies the type of audit log entries that you want to collect for an ApsaraDB for MongoDB instance.|
|[DescribeAuditLogFilter](/intl.en-US/API Reference/Audit Logs/DescribeAuditLogFilter.md)|Queries the types of entries in the audit log collected for an ApsaraDB for MongoDB instance.|
|[ModifyAuditPolicy](/intl.en-US/API Reference/Audit Logs/ModifyAuditPolicy.md)|Enables or disables the audit log feature or set the log retention period for an ApsaraDB for MongoDB instance.|

## Log management

|API|Description|
|---|-----------|
|[DescribeSlowLogRecords](/intl.en-US/API Reference/Log management/DescribeSlowLogRecords.md)|Queries entries in the slow query log of an ApsaraDB for MongoDB instance.|
|[DescribeErrorLogRecords](/intl.en-US/API Reference/Log management/DescribeErrorLogRecords.md)|Queries the error log of an ApsaraDB for MongoDB instance.|
|[DescribeRunningLogRecords](/intl.en-US/API Reference/Log management/DescribeRunningLogRecords.md)|Queries the operational log of an ApsaraDB for MongoDB instance.|
|[DescribeMongoDBLogConfig](/intl.en-US/API Reference/Log management/DescribeMongoDBLogConfig.md)|You can call DescribeMongoDBLogConfig to view the log service configuration of ApsaraDB for MongoDB.|

## Performance monitoring management

|API|Description|
|---|-----------|
|[DescribeDBInstancePerformance](/intl.en-US/API Reference/Performance monitoring management/DescribeDBInstancePerformance.md)|Queries the performance data of an ApsaraDB for MongoDB instance.|
|[ModifyDBInstanceMonitor](/intl.en-US/API Reference/Performance monitoring management/ModifyDBInstanceMonitor.md)|Sets the monitoring granularity for an ApsaraDB for MongoDB instance.|
|[DescribeDBInstanceMonitor](/intl.en-US/API Reference/Performance monitoring management/DescribeDBInstanceMonitor.md)|Sets the monitoring granularity for an ApsaraDB for MongoDB instance.|

## Parameter management

|API|Description|
|---|-----------|
|[DescribeParameterModificationHistory](/intl.en-US/API Reference/Parameter management/DescribeParameterModificationHistory.md)|Queries the modification records of ApsaraDB for MongoDB instance parameters.|
|[DescribeParameters](/intl.en-US/API Reference/Parameter management/DescribeParameters.md)|Queries parameter configurations of an ApsaraDB for MongoDB instance.|
|[DescribeParameterTemplates](/intl.en-US/API Reference/Parameter management/DescribeParameterTemplates.md)|Queries the list of default parameter templates for ApsaraDB for MongoDB instances.|
|[ModifyParameters](/intl.en-US/API Reference/Parameter management/ModifyParameters.md)|Modifies the parameters of an AsparaDB for MongoDB instance.|

## Index recommendation

|API|Description|
|---|-----------|
|[DescribeIndexRecommendation]()|Queries the index recommendation details of an AsparaDB for MongoDB instance.|
|[CreateRecommendationTask](/intl.en-US/API Reference/Index recommendations/CreateRecommendationTask.md)|Creates index analysis tasks for an AsparaDB for MongoDB instance.|
|[DescribeAvailableTimeRange](/intl.en-US/API Reference/Index recommendations/DescribeAvailableTimeRange.md)|Queries the analysis period and generation status of the index analysis report on an ApsaraDB for MongoDB instance.|

## Backup and restoration

|API|Description|
|---|-----------|
|[DescribeBackupPolicy](/intl.en-US/API Reference/Backup and recovery/DescribeBackupPolicy.md)|Queries the backup policy of an ApsaraDB for MongoDB instance.|
|[ModifyBackupPolicy](/intl.en-US/API Reference/Backup and recovery/ModifyBackupPolicy.md)|Modifies the backup policy of an ApsaraDB for MongoDB instance.|
|[CreateBackup](/intl.en-US/API Reference/Backup and recovery/CreateBackup.md)|Manually backs up MongoDB instances.|
|[DescribeBackups](/intl.en-US/API Reference/Backup and recovery/DescribeBackups.md)|Queries the backups of an ApsaraDB for MongoDB instance.|
|[RestoreDBInstance](/intl.en-US/API Reference/Backup and recovery/RestoreDBInstance.md)|Restores data to the current ApsaraDB for MongoDB instance.|
|[DescribeBackupDBs](/intl.en-US/API Reference/Backup and recovery/DescribeBackupDBs.md)|Queries the databases at the specified time or the databases in a specified backup set before you restore a database for an ApsaraDB for MongoDB instance.|
|[CheckRecoveryCondition](/intl.en-US/API Reference/Backup and recovery/CheckRecoveryCondition.md)|Checks whether an ApsaraDB for MongoDB instance meets the data restoration conditions.|

## Renewal management

|API|Description|
|---|-----------|
|[DescribePrice](/intl.en-US/API Reference/Renewal management/DescribePrice.md)|Queries the fees incurred by creating, upgrading, or renewing ApsaraDB for MongoDB instances.|
|[ModifyInstanceAutoRenewalAttribute](/intl.en-US/API Reference/Renewal management/ModifyInstanceAutoRenewalAttribute.md)|Enables or disables auto-renewal for an ApsaraDB for MongoDB instance.|
|[TransformToPrePaid](/intl.en-US/API Reference/Renewal management/TransformToPrePaid.md)|Changes the billing method of an ApsaraDB for MongoDB instance from pay-as-you-go to subscription.|
|[RenewDBInstance](/intl.en-US/API Reference/Renewal management/RenewDBInstance.md)|Manually renews a subscription instance.|
|[DescribeRenewalPrice](/intl.en-US/API Reference/Renewal management/DescribeRenewalPrice.md)|Queries the monthly renewal price of an ApsaraDB for MongoDB instance.|

## Appendixes

|API|Description|
|---|-----------|
|[Error codes](/intl.en-US/API Reference/Appendix/Error codes.md)|Error codes|
|[Instance specifications](/intl.en-US/API Reference/Appendix/Instance specifications.md)|Instance specifications|
|[Instance states](/intl.en-US/API Reference/Appendix/Instance states.md)|Instance states|
|[Performance metrics](/intl.en-US/API Reference/Appendix/Performance metrics.md)|Performance metrics|

