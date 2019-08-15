# API概览 {#doc_6758 .concept}

云数据库 MongoDB 版提供以下相关API接口。

## 如何使用RAM授权 {#section_4kp_b2u_xgw .section}

|API|描述|
|---|--|
|[使用RAM实现MongoDB资源授权](cn.zh-CN/API参考/如何使用RAM授权/使用RAM实现MongoDB资源授权.md)|使用阿里云的RAM（Resource Access Management）服务，您可以将您云账号下MongoDB资源的访问及管理权限授予RAM中子用户。|
|[RAM中可授权的MongoDB资源类型](cn.zh-CN/API参考/如何使用RAM授权/RAM中可授权的MongoDB资源类型.md)|目前，可以在RAM中进行授权的资源类型仅一种：dbinstance。在通过RAM进行授权时，资源的描述方式如下：|
|[RAM中可对MongoDB资源进行授权的Action](cn.zh-CN/API参考/如何使用RAM授权/RAM中可对MongoDB资源进行授权的Action.md)|在RAM中，可以对一个MongoDB资源进行以下Action的授权。|
|[MongoDB API的鉴权规则](cn.zh-CN/API参考/如何使用RAM授权/MongoDB API的鉴权规则.md)|当子用户通过MongoDB Open API进行资源访问时，MongoDB后台向RAM进行权限检查，以确保调用者拥有响应权限。|

## 生命周期管理 {#section_5bd_vnf_tpe .section}

|API|描述|
|---|--|
|[CreateDBInstance](cn.zh-CN/API参考/生命周期管理/CreateDBInstance.md)|该接口用于创建MongoDB副本集实例，同时也可用于克隆MongoDB副本集实例。|
|[ModifyDBInstanceSpec](cn.zh-CN/API参考/生命周期管理/ModifyDBInstanceSpec.md)|调用ModifyDBInstanceSpec接口变更MongoDB单节点或副本集实例的规格或存储空间。|
|[DeleteDBInstance](cn.zh-CN/API参考/生命周期管理/DeleteDBInstance.md)|调用DeleteDBInstance接口释放MongoDB实例。|
|[RenewDBInstance](cn.zh-CN/API参考/生命周期管理/RenewDBInstance.md)|调用RenewDBInstance接口手动续费包年包月实例。|
|[CreateShardingDBInstance](cn.zh-CN/API参考/生命周期管理/CreateShardingDBInstance.md)|调用CreateShardingDBInstance接口创建或者克隆MongoDB分片集群实例。|
|[CreateNode](cn.zh-CN/API参考/生命周期管理/CreateNode.md)|调用CreateNode接口为MongoDB分片集群实例增加Shard节点或Mongos节点。|
|[DeleteNode](cn.zh-CN/API参考/生命周期管理/DeleteNode.md)|调用DeleteNode接口删除MongoDB分片集群实例中的Shard节点或Mongos节点。|
|[ModifyNodeSpec](cn.zh-CN/API参考/生命周期管理/ModifyNodeSpec.md)|调用ModifyNodeSpec接口变更MongoDB分片集群实例中节点的规格和存储空间。|

## 实例管理 {#section_fhf_yjx_6b1 .section}

|API|描述|
|---|--|
|[ModifyDBInstanceDescription](cn.zh-CN/API参考/实例管理/ModifyDBInstanceDescription.md)|调用ModifyDBInstanceDescription接口修改MongoDB实例名称。|
|[DescribeRegions](cn.zh-CN/API参考/实例管理/DescribeRegions.md)|调用DescribeRegions接口查看MongoDB实例可用的地域和可用区。|
|[RestartDBInstance](cn.zh-CN/API参考/实例管理/RestartDBInstance.md)|调用RestartDBInstance接口重启MongoDB实例。|
|[DescribeReplicaSetRole](cn.zh-CN/API参考/实例管理/DescribeReplicaSetRole.md)|调用DescribeReplicaSetRole接口查询MongoDB实例中的角色信息及连接信息。|
|[DescribeShardingNetworkAddress](cn.zh-CN/API参考/实例管理/DescribeShardingNetworkAddress.md)|调用DescribeShardingNetworkAddress接口查询MongoDB分片集群实例的连接信息。|
|[ModifyDBInstanceNetworkType](cn.zh-CN/API参考/实例管理/ModifyDBInstanceNetworkType.md)|调用ModifyDBInstanceNetworkType接口切换MongoDB实例的网络类型。|
|[ModifyDBInstanceNetExpireTime](cn.zh-CN/API参考/实例管理/ModifyDBInstanceNetExpireTime.md)|调用ModifyDBInstanceNetExpireTime接口延长MongoDB实例的经典网络保留时长。|
|[SwitchDBInstanceHA](cn.zh-CN/API参考/实例管理/SwitchDBInstanceHA.md)|调用SwitchDBInstanceHA接口切换MongoDB实例中的主备节点。|
|[AllocatePublicNetworkAddress](cn.zh-CN/API参考/实例管理/AllocatePublicNetworkAddress.md)|调用AllocatePublicNetworkAddress接口为MongoDB实例申请公网连接地址。|
|[ReleasePublicNetworkAddress](cn.zh-CN/API参考/实例管理/ReleasePublicNetworkAddress.md)|调用ReleasePublicNetworkAddress接口释放MongoDB实例的公网连接地址。|
|[UpgradeDBInstanceEngineVersion](cn.zh-CN/API参考/实例管理/UpgradeDBInstanceEngineVersion.md)|调用UpgradeDBInstanceEngineVersion接口升级MongoDB实例的数据库版本。|
|[ModifyDBInstanceConnectionString](cn.zh-CN/API参考/实例管理/ModifyDBInstanceConnectionString.md)|调用ModifyDBInstanceConnectionString接口修改MongoDB实例的连接地址。|
|[UpgradeDBInstanceKernelVersion](cn.zh-CN/API参考/实例管理/UpgradeDBInstanceKernelVersion.md)|调用UpgradeDBInstanceKernelVersion接口升级MongoDB实例的数据库小版本。|
|[DescribeKernelReleaseNotes](cn.zh-CN/API参考/实例管理/DescribeKernelReleaseNotes.md)|调用DescribeKernelReleaseNotes接口查询MongoDB实例的小版本发布日志。|
|[DestroyInstance](cn.zh-CN/API参考/实例管理/DestroyInstance.md)|调用DestroyInstance接口销毁MongoDB实例。|
|[DescribeDBInstances](cn.zh-CN/API参考/实例管理/DescribeDBInstances.md)|调用DescribeDBInstances接口查询MongoDB实例列表。|
|[ModifyDBInstanceMaintainTime](cn.zh-CN/API参考/实例管理/ModifyDBInstanceMaintainTime.md)|调用ModifyDBInstanceMaintainTime接口修改MongoDB实例的可维护时间。|
|[DescribeDBInstanceAttribute](cn.zh-CN/API参考/实例管理/DescribeDBInstanceAttribute.md)|调用DescribeDBInstanceAttribute接口查询MongoDB实例详情。|
|[MigrateAvailableZone](cn.zh-CN/API参考/实例管理/MigrateAvailableZone.md)|调用MigrateAvailableZone接口迁移MongoDB实例的可用区。|
|[ModifyInstanceVpcAuthMode](cn.zh-CN/API参考/实例管理/ModifyInstanceVpcAuthMode.md)|调用ModifyInstanceVpcAuthMode接口开启或关闭MongoDB实例的专有网络免密访问功能。|

## 账号管理 {#section_s3h_nvv_7la .section}

|API|描述|
|---|--|
|[DescribeAccounts](cn.zh-CN/API参考/账号管理/DescribeAccounts.md)|调用DescribeAccounts接口查询MongoDB实例的数据库账号信息。|
|[ResetAccountPassword](cn.zh-CN/API参考/账号管理/ResetAccountPassword.md)|调用ResetAccountPassword接口重置MongoDB实例中root账号的密码。|
|[ModifyAccountDescription](cn.zh-CN/API参考/账号管理/ModifyAccountDescription.md)|调用ModifyAccountDescription接口修改MongoDB实例中root账号的备注信息。|

## 安全管理 {#section_jkc_fpl_qjk .section}

|API|描述|
|---|--|
|[DescribeAuditPolicy](cn.zh-CN/API参考/安全管理/DescribeAuditPolicy.md)|调用DescribeAuditPolicy接口查询MongoDB实例的审计日志是否开启。|
|[DescribeAuditRecords](cn.zh-CN/API参考/安全管理/DescribeAuditRecords.md)|调用DescribeAuditRecords接口查询MongoDB实例的审计日志。|
|[DescribeAuditFiles](cn.zh-CN/API参考/安全管理/DescribeAuditFiles.md)|调用DescribeAuditFiles接口查询MongoDB实例的审计日志文件。|
|[DescribeAuditLogFilter](cn.zh-CN/API参考/安全管理/DescribeAuditLogFilter.md)|调用DescribeAuditLogFilter接口查询MongoDB实例审计日志采集的日志类型。|
|[ModifyAuditLogFilter](cn.zh-CN/API参考/安全管理/ModifyAuditLogFilter.md)|调用ModifyAuditLogFilter接口修改MongoDB实例审计日志的采集类型。|
|[DescribeSecurityIps](cn.zh-CN/API参考/安全管理/DescribeSecurityIps.md)|调用DescribeSecurityIps接口查询MongoDB实例的IP白名单。|
|[ModifySecurityIps](cn.zh-CN/API参考/安全管理/ModifySecurityIps.md)|调用ModifySecurityIps接口修改MongoDB实例的IP白名单。|
|[ModifyDBInstanceSSL](cn.zh-CN/API参考/安全管理/ModifyDBInstanceSSL.md)|调用ModifyDBInstanceSSL接口修改MongoDB实例的SSL配置。|
|[DescribeDBInstanceSSL](cn.zh-CN/API参考/安全管理/DescribeDBInstanceSSL.md)|调用DescribeDBInstanceSSL接口查询MongoDB实例的SSL设置详情。|

## 日志管理 {#section_90h_4lw_ich .section}

|API|描述|
|---|--|
|[DescribeSlowLogRecords](cn.zh-CN/API参考/日志管理/DescribeSlowLogRecords.md)|调用DescribeSlowLogRecords接口查询MongoDB实例运行出现的慢操作日志明细。|
|[DescribeRunningLogRecords](cn.zh-CN/API参考/日志管理/DescribeRunningLogRecords.md)|调用DescribeRunningLogRecords接口查询MongoDB实例的运行日志。|
|[DescribeErrorLogRecords](cn.zh-CN/API参考/日志管理/DescribeErrorLogRecords.md)|调用DescribeErrorLogRecords接口查询MongoDB实例的错误日志。|

## 性能监控管理 {#section_7tm_per_ow4 .section}

|API|描述|
|---|--|
|[DescribeDBInstancePerformance](cn.zh-CN/API参考/性能监控管理/DescribeDBInstancePerformance.md)|调用DescribeDBInstancePerformance接口查询MongoDB实例性能数据。|

## 参数管理 {#section_khs_swi_ix9 .section}

|API|描述|
|---|--|
|[DescribeParameterModificationHistory](cn.zh-CN/API参考/参数管理/DescribeParameterModificationHistory.md)|调用DescribeParameterModificationHistory接口查询MongoDB实例参数的修改记录。|
|[DescribeParameters](cn.zh-CN/API参考/参数管理/DescribeParameters.md)|调用DescribeParameters接口查询MongoDB实例的参数配置信息。|
|[DescribeParameterTemplates](cn.zh-CN/API参考/参数管理/DescribeParameterTemplates.md)|调用DescribeParameterTemplates接口查询MongoDB实例默认的参数模板列表。|
|[ModifyParameters](cn.zh-CN/API参考/参数管理/ModifyParameters.md)|调用ModifyParameters接口修改MongoDB实例的参数。|

## 索引推荐 {#section_jyg_kkc_fcw .section}

|API|描述|
|---|--|
|[CreateRecommendationTask](cn.zh-CN/API参考/索引推荐/CreateRecommendationTask.md)|调用CreateRecommendationTask接口为MongoDB实例创建索引分析任务。|
|[DescribeAvailableTimeRange](cn.zh-CN/API参考/索引推荐/DescribeAvailableTimeRange.md)|调用DescribeAvailableTimeRange接口查询MongoDB实例索引分析报告的分析时间段和生成状态。|
|[DescribeIndexRecommendation](cn.zh-CN/API参考/索引推荐/DescribeIndexRecommendation.md)|调用DescribeIndexRecommendation接口查询MongoDB实例的索引推荐详情。|

## 备份与恢复 {#section_5mg_yfx_jwv .section}

|API|描述|
|---|--|
|[DescribeBackupPolicy](cn.zh-CN/API参考/备份与恢复/DescribeBackupPolicy.md)|调用DescribeBackupPolicy接口查询MongoDB实例的备份策略。|
|[ModifyBackupPolicy](cn.zh-CN/API参考/备份与恢复/ModifyBackupPolicy.md)|调用ModifyBackupPolicy接口修改MongoDB实例的备份策略。|
|[CreateBackup](cn.zh-CN/API参考/备份与恢复/CreateBackup.md)|调用CreateBackup接口手动备份MongoDB实例。|
|[DescribeBackups](cn.zh-CN/API参考/备份与恢复/DescribeBackups.md)|调用DescribeBackups接口查询MongoDB实例的备份列表。|
|[RestoreDBInstance](cn.zh-CN/API参考/备份与恢复/RestoreDBInstance.md)|调用RestoreDBInstance接口恢复数据至当前MongoDB实例。|

## 附表 {#section_zdl_jhc_sww .section}

|API|描述|
|---|--|
|[错误码表](cn.zh-CN/API参考/附表/错误码表.md)|错误码表|
|[实例规格表](cn.zh-CN/API参考/附表/实例规格表.md)|参见：实例规格表。|
|[实例状态表](cn.zh-CN/API参考/附表/实例状态表.md)|实例状态表|
|[性能监控表](cn.zh-CN/API参考/附表/性能监控表.md)|性能监控表|

