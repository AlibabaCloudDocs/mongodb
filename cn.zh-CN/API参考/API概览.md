# API概览 {#doc_6758 .concept}

云数据库 MongoDB 版提供以下相关API接口。

## 生命周期管理 {#section_ilq_owy_oh7 .section}

|API|描述|
|---|--|
|[CreateDBInstance](~~61763~~)|该接口用于创建MongoDB副本集实例，同时也可用于克隆MongoDB副本集实例。|
|[ModifyDBInstanceSpec](~~61816~~)|调用ModifyDBInstanceSpec接口变更MongoDB单节点或副本集实例的规格或存储空间。|
|[DeleteDBInstance](~~61826~~)|调用DeleteDBInstance接口释放MongoDB实例。|
|[RenewDBInstance](~~61830~~)|调用RenewDBInstance接口手动续费包年包月实例。|
|[CreateShardingDBInstance](~~61884~~)|调用CreateShardingDBInstance接口创建或者克隆MongoDB分片集群实例。|
|[CreateNode](~~61911~~)|调用CreateNode接口为MongoDB分片集群实例增加Shard节点或Mongos节点。|
|[DeleteNode](~~61922~~)|调用DeleteNode接口删除MongoDB分片集群实例中的Shard节点或Mongos节点。|
|[ModifyNodeSpec](~~61923~~)|调用ModifyNodeSpec接口变更MongoDB分片集群实例中节点的规格和存储空间。|

## 实例管理 {#section_amp_zqd_rwo .section}

|API|描述|
|---|--|
|[ModifyDBInstanceDescription](~~62009~~)|调用ModifyDBInstanceDescription接口修改MongoDB实例名称。|
|[DescribeRegions](~~61933~~)|调用DescribeRegions接口查看MongoDB实例可用的地域和可用区。|
|[RestartDBInstance](~~62006~~)|调用RestartDBInstance接口重启MongoDB实例。|
|[DescribeReplicaSetRole](~~62134~~)|调用DescribeReplicaSetRole接口查询MongoDB实例中的角色信息及连接信息。|
|[DescribeShardingNetworkAddress](~~62135~~)|调用DescribeShardingNetworkAddress接口查询MongoDB分片集群实例的连接信息。|
|[ModifyDBInstanceNetworkType](~~62138~~)|调用ModifyDBInstanceNetworkType接口切换MongoDB实例的网络类型。|
|[ModifyDBInstanceNetExpireTime](~~94536~~)|调用ModifyDBInstanceNetExpireTime接口延长MongoDB实例的经典网络保留时长。|
|[SwitchDBInstanceHA](~~66887~~)|调用SwitchDBInstanceHA接口切换MongoDB实例中的主备节点。|
|[AllocatePublicNetworkAddress](~~67602~~)|调用AllocatePublicNetworkAddress接口为MongoDB实例申请公网连接地址。|
|[ReleasePublicNetworkAddress](~~67604~~)|调用ReleasePublicNetworkAddress接口释放MongoDB实例的公网连接地址。|
|[UpgradeDBInstanceEngineVersion](~~67608~~)|调用UpgradeDBInstanceEngineVersion接口升级MongoDB实例的数据库版本。|
|[ModifyDBInstanceConnectionString](~~90263~~)|调用ModifyDBInstanceConnectionString接口修改MongoDB实例的连接地址。|
|[UpgradeDBInstanceKernelVersion](~~89819~~)|调用UpgradeDBInstanceKernelVersion接口升级MongoDB实例的数据库小版本。|
|[DescribeKernelReleaseNotes](~~89852~~)|调用DescribeKernelReleaseNotes接口查询MongoDB实例的小版本发布日志。|
|[DestroyInstance](~~85501~~)|调用DestroyInstance接口销毁MongoDB实例。|
|[DescribeDBInstances](~~61939~~)|调用DescribeDBInstances接口查询MongoDB实例列表。|
|[ModifyDBInstanceMaintainTime](~~62008~~)|调用ModifyDBInstanceMaintainTime接口修改MongoDB实例的可维护时间。|
|[DescribeDBInstanceAttribute](~~62010~~)|调用DescribeDBInstanceAttribute接口查询MongoDB实例详情。|
|[MigrateAvailableZone](~~116036~~)|调用MigrateAvailableZone接口迁移MongoDB实例的可用区。|
|[ModifyInstanceVpcAuthMode](~~116099~~)|调用ModifyInstanceVpcAuthMode接口开启或关闭MongoDB实例的专有网络免密访问功能。|

## 账号管理 {#section_eoz_ozd_ukv .section}

|API|描述|
|---|--|
|[DescribeAccounts](~~62153~~)|调用DescribeAccounts接口查询MongoDB实例的数据库账号信息。|
|[ResetAccountPassword](~~62152~~)|调用ResetAccountPassword接口重置MongoDB实例中root账号的密码。|
|[ModifyAccountDescription](~~62154~~)|调用ModifyAccountDescription接口修改MongoDB实例中root账号的备注信息。|

## 安全管理 {#section_icg_7tm_iko .section}

|API|描述|
|---|--|
|[DescribeAuditPolicy](~~89021~~)|调用DescribeAuditPolicy接口查询MongoDB实例的审计日志是否开启。|
|[DescribeAuditRecords](~~62158~~)|调用DescribeAuditRecords接口查询MongoDB实例的审计日志。|
|[DescribeAuditFiles](~~62162~~)|调用DescribeAuditFiles接口查询MongoDB实例的审计日志文件。|
|[DescribeAuditLogFilter](~~89090~~)|调用DescribeAuditLogFilter接口查询MongoDB实例审计日志采集的日志类型。|
|[ModifyAuditLogFilter](~~89033~~)|调用ModifyAuditLogFilter接口修改MongoDB实例审计日志的采集类型。|
|[DescribeSecurityIps](~~62156~~)|调用DescribeSecurityIps接口查询MongoDB实例的IP白名单。|
|[ModifySecurityIps](~~62157~~)|调用ModifySecurityIps接口修改MongoDB实例的IP白名单。|
|[ModifyDBInstanceSSL](~~89255~~)|调用ModifyDBInstanceSSL接口修改MongoDB实例的SSL配置。|
|[DescribeDBInstanceSSL](~~89268~~)|调用DescribeDBInstanceSSL接口查询MongoDB实例的SSL设置详情。|

## 日志管理 {#section_ow6_eq5_p45 .section}

|API|描述|
|---|--|
|[DescribeSlowLogRecords](~~108227~~)|调用DescribeSlowLogRecords接口查询MongoDB实例运行出现的慢操作日志明细。|
|[DescribeRunningLogRecords](~~108229~~)|调用DescribeRunningLogRecords接口查询MongoDB实例的运行日志。|
|[DescribeErrorLogRecords](~~108228~~)|调用DescribeErrorLogRecords接口查询MongoDB实例的错误日志。|

## 性能监控管理 {#section_auk_u8g_l9c .section}

|API|描述|
|---|--|
|[DescribeDBInstancePerformance](~~62175~~)|调用DescribeDBInstancePerformance接口查询MongoDB实例性能数据。|

## 参数管理 {#section_7he_c0i_rhj .section}

|API|描述|
|---|--|
|[DescribeParameterModificationHistory](~~67614~~)|调用DescribeParameterModificationHistory接口查询MongoDB实例参数的修改记录。|
|[DescribeParameters](~~67611~~)|调用DescribeParameters接口查询MongoDB实例的参数配置信息。|
|[DescribeParameterTemplates](~~67618~~)|调用DescribeParameterTemplates接口查询MongoDB实例默认的参数模板列表。|
|[ModifyParameters](~~67612~~)|调用ModifyParameters接口修改MongoDB实例的参数。|

## 索引推荐 {#section_pnk_t4w_hp9 .section}

|API|描述|
|---|--|
|[CreateRecommendationTask](~~95527~~)|调用CreateRecommendationTask接口为MongoDB实例创建索引分析任务。|
|[DescribeAvailableTimeRange](~~95534~~)|调用DescribeAvailableTimeRange接口查询MongoDB实例索引分析报告的分析时间段和生成状态。|
|[DescribeIndexRecommendation](~~95517~~)|调用DescribeIndexRecommendation接口查询MongoDB实例的索引推荐详情。|

## 备份与恢复 {#section_3ia_tbf_a0c .section}

|API|描述|
|---|--|
|[DescribeBackupPolicy](~~62168~~)|调用DescribeBackupPolicy接口查询MongoDB实例的备份策略。|
|[ModifyBackupPolicy](~~62169~~)|调用ModifyBackupPolicy接口修改MongoDB实例的备份策略。|
|[CreateBackup](~~62171~~)|调用CreateBackup接口手动备份MongoDB实例。|
|[DescribeBackups](~~62172~~)|调用DescribeBackups接口查询MongoDB实例的备份列表。|
|[RestoreDBInstance](~~62173~~)|调用RestoreDBInstance接口恢复数据至当前MongoDB实例。|

