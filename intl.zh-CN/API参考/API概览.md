# API概览

云数据库 MongoDB 版提供以下相关API接口。

## 生命周期管理

|API|描述|
|---|--|
|[CreateDBInstance](/intl.zh-CN/API参考/生命周期管理/CreateDBInstance.md)|该接口用于创建MongoDB副本集实例，同时也可用于克隆MongoDB副本集实例。|
|[ModifyDBInstanceSpec](/intl.zh-CN/API参考/生命周期管理/ModifyDBInstanceSpec.md)|调用ModifyDBInstanceSpec接口变更MongoDB单节点或副本集实例的规格或存储空间。|
|[DeleteDBInstance](/intl.zh-CN/API参考/生命周期管理/DeleteDBInstance.md)|调用DeleteDBInstance接口释放MongoDB实例。|
|[CreateShardingDBInstance](/intl.zh-CN/API参考/生命周期管理/CreateShardingDBInstance.md)|调用CreateShardingDBInstance接口创建或者克隆MongoDB分片集群实例。|
|[CreateNode](/intl.zh-CN/API参考/生命周期管理/CreateNode.md)|调用CreateNode接口为MongoDB分片集群实例增加Shard节点或Mongos节点。|
|[DeleteNode](/intl.zh-CN/API参考/生命周期管理/DeleteNode.md)|调用DeleteNode接口删除MongoDB分片集群实例中的Shard节点或Mongos节点。|
|[ModifyNodeSpec](/intl.zh-CN/API参考/生命周期管理/ModifyNodeSpec.md)|调用ModifyNodeSpec接口变更MongoDB分片集群实例中节点的规格和存储空间。|
|[DescribeInstanceAutoRenewalAttribute](/intl.zh-CN/API参考/生命周期管理/DescribeInstanceAutoRenewalAttribute.md)|调用DescribeInstanceAutoRenewalAttribute接口查询MongoDB实例是否为自动付费。|

## 区域管理

|API|描述|
|---|--|
|[MigrateToOtherZone](/intl.zh-CN/API参考/区域管理/MigrateToOtherZone.md)|调用MigrateToOtherZone接口迁移MongoDB实例到其他可用区。|
|[DescribeRegions](/intl.zh-CN/API参考/区域管理/DescribeRegions.md)|调用DescribeRegions接口查看MongoDB实例可用的地域和可用区。|
|[MigrateAvailableZone](/intl.zh-CN/API参考/区域管理/MigrateAvailableZone.md)|调用MigrateAvailableZone接口迁移MongoDB实例的可用区。|

## 资源管理

|API|描述|
|---|--|
|[EvaluateResource](/intl.zh-CN/API参考/资源管理/EvaluateResource.md)|在新购实例或对实例进行变配之前调用EvaluateResource接口评估是否有足够的资源。|
|[DescribeAvailableResource](/intl.zh-CN/API参考/资源管理/DescribeAvailableResource.md)|调用DescribeAvailableResource查询指定可用区内可创建的实例。|

## 连接管理

|API|描述|
|---|--|
|[AllocatePublicNetworkAddress](/intl.zh-CN/API参考/连接管理/AllocatePublicNetworkAddress.md)|调用AllocatePublicNetworkAddress接口为MongoDB实例申请公网连接地址。|
|[ReleasePublicNetworkAddress](/intl.zh-CN/API参考/连接管理/ReleasePublicNetworkAddress.md)|调用ReleasePublicNetworkAddress接口释放MongoDB实例的公网连接地址。|
|[ModifyInstanceVpcAuthMode](/intl.zh-CN/API参考/连接管理/ModifyInstanceVpcAuthMode.md)|调用ModifyInstanceVpcAuthMode接口开启或关闭MongoDB实例的专有网络免密访问功能。|
|[DescribeShardingNetworkAddress](/intl.zh-CN/API参考/连接管理/DescribeShardingNetworkAddress.md)|调用DescribeShardingNetworkAddress接口查询MongoDB分片集群实例的连接信息。|
|[ModifyDBInstanceNetworkType](/intl.zh-CN/API参考/连接管理/ModifyDBInstanceNetworkType.md)|调用ModifyDBInstanceNetworkType接口切换MongoDB实例的网络类型。|
|[ModifyDBInstanceConnectionString](/intl.zh-CN/API参考/连接管理/ModifyDBInstanceConnectionString.md)|调用ModifyDBInstanceConnectionString接口修改MongoDB实例的连接地址。|
|[ReleaseNodePrivateNetworkAddress](/intl.zh-CN/API参考/连接管理/ReleaseNodePrivateNetworkAddress.md)|调用ReleaseNodePrivateNetworkAddress接口释放MongoDB分片集群实例的Shard节点或ConfigServer节点的内网连接地址。|
|[AllocateNodePrivateNetworkAddress](/intl.zh-CN/API参考/连接管理/AllocateNodePrivateNetworkAddress.md)|调用AllocateNodePrivateNetworkAddress接口为MongoDB分片集群实例的Shard节点或ConfigServer节点申请内网连接地址。|

## 查询实例信息

|API|描述|
|---|--|
|[DescribeReplicaSetRole](/intl.zh-CN/API参考/查询实例信息/DescribeReplicaSetRole.md)|调用DescribeReplicaSetRole接口查询MongoDB实例中的角色信息及连接信息。|
|[DescribeKernelReleaseNotes](/intl.zh-CN/API参考/查询实例信息/DescribeKernelReleaseNotes.md)|调用DescribeKernelReleaseNotes接口查询MongoDB实例的小版本发布日志。|
|[DescribeAvailableEngineVersion](/intl.zh-CN/API参考/查询实例信息/DescribeAvailableEngineVersion.md)|调用DescribeAvailableEngineVersion接口查询MongoDB实例可升级的版本。|
|[DescribeDBInstances](/intl.zh-CN/API参考/查询实例信息/DescribeDBInstances.md)|调用DescribeDBInstances接口查询MongoDB实例列表。|
|[DescribeDBInstanceAttribute](/intl.zh-CN/API参考/查询实例信息/DescribeDBInstanceAttribute.md)|调用DescribeDBInstanceAttribute接口查询MongoDB实例详情。|
|[DescribeRoleZoneInfo](/intl.zh-CN/API参考/查询实例信息/DescribeRoleZoneInfo.md)|调用DescribeRoleZoneInfo接口查询MongoDB实例的各节点的角色和所属的可用区。|
|[DescribeActiveOperationTaskCount](/intl.zh-CN/API参考/查询实例信息/DescribeActiveOperationTaskCount.md)|调用DescribeActiveOperationTaskCount接口查询MongoDB实例的运维任务数量。|
|[DescribeActiveOperationTaskType](/intl.zh-CN/API参考/查询实例信息/DescribeActiveOperationTaskType.md)|调用DescribeActiveOperationTaskType接口查询MongoDB实例的运维任务类型以及各类型的任务数量。|

## 实例管理

|API|描述|
|---|--|
|[RestartDBInstance](/intl.zh-CN/API参考/实例管理/RestartDBInstance.md)|调用RestartDBInstance接口重启MongoDB实例。|
|[ModifyDBInstanceMaintainTime](/intl.zh-CN/API参考/实例管理/ModifyDBInstanceMaintainTime.md)|调用ModifyDBInstanceMaintainTime接口修改MongoDB实例的可维护时间。|
|[ModifyDBInstanceDescription](/intl.zh-CN/API参考/实例管理/ModifyDBInstanceDescription.md)|调用ModifyDBInstanceDescription接口修改MongoDB实例名称。|
|[SwitchDBInstanceHA](/intl.zh-CN/API参考/实例管理/SwitchDBInstanceHA.md)|调用SwitchDBInstanceHA接口切换MongoDB实例中的主备节点。|
|[UpgradeDBInstanceEngineVersion](/intl.zh-CN/API参考/实例管理/UpgradeDBInstanceEngineVersion.md)|调用UpgradeDBInstanceEngineVersion接口升级MongoDB实例的数据库版本。|
|[DestroyInstance](/intl.zh-CN/API参考/实例管理/DestroyInstance.md)|调用DestroyInstance接口销毁MongoDB实例。|
|[UpgradeDBInstanceKernelVersion](/intl.zh-CN/API参考/实例管理/UpgradeDBInstanceKernelVersion.md)|调用UpgradeDBInstanceKernelVersion接口升级MongoDB实例的数据库小版本。|
|[ModifyDBInstanceNetExpireTime](/intl.zh-CN/API参考/实例管理/ModifyDBInstanceNetExpireTime.md)|调用ModifyDBInstanceNetExpireTime接口延长MongoDB实例的经典网络保留时长。|

## 标签管理

|API|描述|
|---|--|
|[TagResources](/intl.zh-CN/API参考/标签管理/TagResources.md)|调用TagResources接口为一个或多个MongoDB实例绑定标签。|
|[ListTagResources](/intl.zh-CN/API参考/标签管理/ListTagResources.md)|调用ListTagResources接口查询MongoDB实例和标签的绑定关系。|
|[DescribeTags](/intl.zh-CN/API参考/标签管理/DescribeTags.md)|调用DescribeTags接口查询目标地域中所有的标签信息。|
|[UntagResources](/intl.zh-CN/API参考/标签管理/UntagResources.md)|调用UntagResources接口将标签从实例中解绑，如果该标签没有绑定到其他实例，则该标签会被删除。|

## 账号管理

|API|描述|
|---|--|
|[DescribeAccounts](/intl.zh-CN/API参考/账号管理/DescribeAccounts.md)|调用DescribeAccounts接口查询MongoDB实例的数据库账号信息。|
|[ResetAccountPassword](/intl.zh-CN/API参考/账号管理/ResetAccountPassword.md)|调用ResetAccountPassword接口重置MongoDB实例中root账号的密码。|
|[ModifyAccountDescription](/intl.zh-CN/API参考/账号管理/ModifyAccountDescription.md)|调用ModifyAccountDescription接口修改MongoDB实例中root账号的备注信息。|

## 白名单和安全组

|API|描述|
|---|--|
|[DescribeSecurityGroupConfiguration](/intl.zh-CN/API参考/白名单和安全组/DescribeSecurityGroupConfiguration.md)|调用DescribeSecurityGroupConfiguration接口查询MongoDB实例绑定的ECS安全组信息。|
|[ModifySecurityGroupConfiguration](/intl.zh-CN/API参考/白名单和安全组/ModifySecurityGroupConfiguration.md)|调用ModifySecurityGroupConfiguration更改MongoDB实例已绑定的ECS安全组。|
|[DescribeSecurityIps](/intl.zh-CN/API参考/白名单和安全组/DescribeSecurityIps.md)|调用DescribeSecurityIps接口查询MongoDB实例的IP白名单。|
|[ModifySecurityIps](/intl.zh-CN/API参考/白名单和安全组/ModifySecurityIps.md)|调用ModifySecurityIps接口修改MongoDB实例的IP白名单。|

## 密钥

|API|描述|
|---|--|
|[CheckCloudResourceAuthorized](/intl.zh-CN/API参考/密钥/CheckCloudResourceAuthorized.md)|调用CheckCloudResourceAuthorized接口查询KMS密钥是否已授权给MongoDB实例。|
|[DescribeUserEncryptionKeyList](/intl.zh-CN/API参考/密钥/DescribeUserEncryptionKeyList.md)|调用DescribeUserEncryptionKeyList查询实例的自定义密钥列表。|
|[DescribeDBInstanceEncryptionKey](/intl.zh-CN/API参考/密钥/DescribeDBInstanceEncryptionKey.md)|调用DescribeDBInstanceEncryptionKey查询MongoDB实例的某个密钥的详情。|
|[DescribeDBInstanceTDEInfo](/intl.zh-CN/API参考/密钥/DescribeDBInstanceTDEInfo.md)|调用DescribeDBInstanceTDEInfo接口查询MongoDB实例的透明数据加密TDE（Transparent Data Encryption）是否开启。|
|[ModifyDBInstanceTDE](/intl.zh-CN/API参考/密钥/ModifyDBInstanceTDE.md)|调用ModifyDBInstanceTDE接口修改MongoDB实例的透明数据加密TDE（Transparent Data Encryption）状态。|

## SSL加密

|API|描述|
|---|--|
|[ModifyDBInstanceSSL](/intl.zh-CN/API参考/SSL加密/ModifyDBInstanceSSL.md)|调用ModifyDBInstanceSSL接口修改MongoDB实例的SSL配置。|
|[DescribeDBInstanceSSL](/intl.zh-CN/API参考/SSL加密/DescribeDBInstanceSSL.md)|调用DescribeDBInstanceSSL接口查询MongoDB实例的SSL设置详情。|

## 审计日志

|API|描述|
|---|--|
|[DescribeAuditRecords](/intl.zh-CN/API参考/审计日志/DescribeAuditRecords.md)|调用DescribeAuditRecords接口查询MongoDB实例的审计日志。|
|[DescribeAuditFiles](/intl.zh-CN/API参考/审计日志/DescribeAuditFiles.md)|调用DescribeAuditFiles接口查询MongoDB实例的审计日志文件。|
|[DescribeAuditPolicy](/intl.zh-CN/API参考/审计日志/DescribeAuditPolicy.md)|调用DescribeAuditPolicy接口查询MongoDB实例的审计日志是否开启。|
|[ModifyAuditLogFilter](/intl.zh-CN/API参考/审计日志/ModifyAuditLogFilter.md)|调用ModifyAuditLogFilter接口修改MongoDB实例审计日志的采集类型。|
|[DescribeAuditLogFilter](/intl.zh-CN/API参考/审计日志/DescribeAuditLogFilter.md)|调用DescribeAuditLogFilter接口查询MongoDB实例审计日志采集的日志类型。|
|[ModifyAuditPolicy](/intl.zh-CN/API参考/审计日志/ModifyAuditPolicy.md)|调用ModifyAuditPolicy接口设置MongoDB实例的审计日志开关或日志存储时长。|

## 日志管理

|API|描述|
|---|--|
|[DescribeSlowLogRecords](/intl.zh-CN/API参考/日志管理/DescribeSlowLogRecords.md)|调用DescribeSlowLogRecords接口查询MongoDB实例运行出现的慢操作日志明细。|
|[DescribeErrorLogRecords](/intl.zh-CN/API参考/日志管理/DescribeErrorLogRecords.md)|调用DescribeErrorLogRecords接口查询MongoDB实例的错误日志。|
|[DescribeRunningLogRecords](/intl.zh-CN/API参考/日志管理/DescribeRunningLogRecords.md)|调用DescribeRunningLogRecords接口查询MongoDB实例的运行日志。|
|[DescribeMongoDBLogConfig](/intl.zh-CN/API参考/日志管理/DescribeMongoDBLogConfig.md)|调用DescribeMongoDBLogConfig查看MongoDB日志服务的配置。|

## 性能监控管理

|API|描述|
|---|--|
|[DescribeDBInstancePerformance](/intl.zh-CN/API参考/性能监控管理/DescribeDBInstancePerformance.md)|调用DescribeDBInstancePerformance接口查询MongoDB实例性能数据。|
|[ModifyDBInstanceMonitor](/intl.zh-CN/API参考/性能监控管理/ModifyDBInstanceMonitor.md)|调用ModifyDBInstanceMonitor接口设置MongoDB实例的监控采集粒度。|
|[DescribeDBInstanceMonitor](/intl.zh-CN/API参考/性能监控管理/DescribeDBInstanceMonitor.md)|调用DescribeDBInstanceMonitor接口查询MongoDB实例的监控采集粒度。|

## 参数管理

|API|描述|
|---|--|
|[DescribeParameterModificationHistory](/intl.zh-CN/API参考/参数管理/DescribeParameterModificationHistory.md)|调用DescribeParameterModificationHistory接口查询MongoDB实例参数的修改记录。|
|[DescribeParameters](/intl.zh-CN/API参考/参数管理/DescribeParameters.md)|调用DescribeParameters接口查询MongoDB实例的参数配置信息。|
|[DescribeParameterTemplates](/intl.zh-CN/API参考/参数管理/DescribeParameterTemplates.md)|调用DescribeParameterTemplates接口查询MongoDB实例默认的参数模板列表。|
|[ModifyParameters](/intl.zh-CN/API参考/参数管理/ModifyParameters.md)|调用ModifyParameters接口修改MongoDB实例的参数。|

## 索引推荐

|API|描述|
|---|--|
|[DescribeIndexRecommendation](/intl.zh-CN/API参考/索引推荐/DescribeIndexRecommendation.md)|调用DescribeIndexRecommendation接口查询MongoDB实例的索引推荐详情。|
|[CreateRecommendationTask](/intl.zh-CN/API参考/索引推荐/CreateRecommendationTask.md)|调用CreateRecommendationTask接口为MongoDB实例创建索引分析任务。|
|[DescribeAvailableTimeRange](/intl.zh-CN/API参考/索引推荐/DescribeAvailableTimeRange.md)|调用DescribeAvailableTimeRange接口查询MongoDB实例索引分析报告的分析时间段和生成状态。|

## 备份与恢复

|API|描述|
|---|--|
|[DescribeBackupPolicy](/intl.zh-CN/API参考/备份与恢复/DescribeBackupPolicy.md)|调用DescribeBackupPolicy接口查询MongoDB实例的备份策略。|
|[ModifyBackupPolicy](/intl.zh-CN/API参考/备份与恢复/ModifyBackupPolicy.md)|调用ModifyBackupPolicy接口修改MongoDB实例的备份策略。|
|[CreateBackup](/intl.zh-CN/API参考/备份与恢复/CreateBackup.md)|调用CreateBackup接口手动备份MongoDB实例。|
|[DescribeBackups](/intl.zh-CN/API参考/备份与恢复/DescribeBackups.md)|调用DescribeBackups接口查询MongoDB实例的备份列表。|
|[RestoreDBInstance](/intl.zh-CN/API参考/备份与恢复/RestoreDBInstance.md)|调用RestoreDBInstance接口恢复数据至当前MongoDB实例。|
|[DescribeBackupDBs](/intl.zh-CN/API参考/备份与恢复/DescribeBackupDBs.md)|在为MongoDB实例执行单库恢复前，您可以调用本接口查询指定的时间点或备份集内包含的数据库。|
|[CheckRecoveryCondition](/intl.zh-CN/API参考/备份与恢复/CheckRecoveryCondition.md)|调用CheckRecoveryCondition接口检查MongoDB实例是否满足数据恢复的条件。|

## 续费管理

|API|描述|
|---|--|
|[DescribePrice](/intl.zh-CN/API参考/续费管理/DescribePrice.md)|调用DescribePrice查询创建MongoDB实例、升级配置或续费操作产生的费用。|
|[ModifyInstanceAutoRenewalAttribute](/intl.zh-CN/API参考/续费管理/ModifyInstanceAutoRenewalAttribute.md)|调用ModifyInstanceAutoRenewalAttribute接口设置MongoDB实例的自动续费功能。|
|[TransformToPrePaid](/intl.zh-CN/API参考/续费管理/TransformToPrePaid.md)|调用TransformToPrePaid接口将按量付费的MongoDB实例转换为包年包月（预付费）实例。|
|[RenewDBInstance](/intl.zh-CN/API参考/续费管理/RenewDBInstance.md)|调用RenewDBInstance接口手动续费包年包月的MongoDB实例。|
|[DescribeRenewalPrice](/intl.zh-CN/API参考/续费管理/DescribeRenewalPrice.md)|调用DescribeRenewalPrice接口查询指定MongoDB实例续费一个月的价格。|

## 附表

|API|描述|
|---|--|
|[错误码表](/intl.zh-CN/API参考/附表/错误码表.md)|错误码表|
|[实例规格表](/intl.zh-CN/API参考/附表/实例规格表.md)|实例规格表|
|[实例状态表](/intl.zh-CN/API参考/附表/实例状态表.md)|实例状态表|
|[性能监控表](/intl.zh-CN/API参考/附表/性能监控表.md)|性能监控表|

