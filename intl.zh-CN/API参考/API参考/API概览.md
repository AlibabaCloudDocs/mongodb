# API概览 {#reference_gwx_tss_l2b .reference}

## 生命周期管理 {#section_xrj_kts_l2b .section}

|API|描述|
|---|--|
|[CreateDBInstance](intl.zh-CN/API参考/API参考/生命周期管理/CreateDBInstance.md#)|创建副本集实例|
|[ModifyDBInstanceSpec](intl.zh-CN/API参考/API参考/生命周期管理/ModifyDBInstanceSpec.md#)ModifyDBInstanceSpec|变配副本集实例|
|[DeleteDBInstance](intl.zh-CN/API参考/API参考/生命周期管理/DeleteDBInstance.md#)|释放实例|
|[RenewDBInstance](intl.zh-CN/API参考/API参考/生命周期管理/RenewDBInstance.md#)|续费副本集实例|
|[CreateShardingDBInstance](intl.zh-CN/API参考/API参考/生命周期管理/CreateShardingDBInstance.md#)|创建分片集群实例|
|[CreateNode](intl.zh-CN/API参考/API参考/生命周期管理/CreateNode.md#)|新增集群实例组件|
|[DeleteNode](intl.zh-CN/API参考/API参考/生命周期管理/DeleteNode.md#)|删除集群实例组件|
|[ModifyNodeSpec](intl.zh-CN/API参考/API参考/生命周期管理/ModifyNodeSpec.md#)|集群实例变配|

## 实例管理 {#section_ndz_lts_l2b .section}

|API|描述|
|---|--|
|[DescribeRegions](intl.zh-CN/API参考/API参考/实例管理/DescribeRegions.md#)|查询可用地域列表|
|[DescribeDBInstances](intl.zh-CN/API参考/API参考/实例管理/DescribeDBInstances.md#)|查询实例列表|
|[RestartDBInstance](intl.zh-CN/API参考/API参考/实例管理/RestartDBInstance.md#)|重启实例|
|[ModifyDBInstanceMaintainTime](intl.zh-CN/API参考/API参考/实例管理/ModifyDBInstanceMaintainTime.md#)|修改实例可维护时间|
|[ModifyDBInstanceDescription](intl.zh-CN/API参考/API参考/实例管理/ModifyDBInstanceDescription.md#)|修改实例备注|
|[DescribeDBInstanceAttribute](intl.zh-CN/API参考/API参考/实例管理/DescribeDBInstanceAttribute.md#)|查询实例详情|
|[DescribeReplicaSetRole](intl.zh-CN/API参考/API参考/实例管理/DescribeReplicaSetRole.md#)|查询复制集角色及连接信息|
|[DescribeShardingNetworkAddress](intl.zh-CN/API参考/API参考/实例管理/DescribeShardingNetworkAddress.md#)|查询分片集群连接信息|
|[ModifyDBInstanceNetworkType](intl.zh-CN/API参考/API参考/实例管理/ModifyDBInstanceNetworkType.md#)|切换实例类型|
|[ModifyDBInstanceNetExpireTime](intl.zh-CN/API参考/API参考/实例管理/ModifyDBInstanceNetExpireTime.md#)|延长经典网络保留时长|
|[SwitchDBInstanceHA](intl.zh-CN/API参考/API参考/实例管理/SwitchDBInstanceHA.md#)|MongoDB实例主备切换|
|[AllocatePublicNetworkAddress](intl.zh-CN/API参考/API参考/实例管理/AllocatePublicNetworkAddress.md#)|申请公网连接地址|
|[ReleasePublicNetworkAddress](intl.zh-CN/API参考/API参考/实例管理/ReleasePublicNetworkAddress.md#)|释放公网连接地址|
|[ModifyDBInstanceConnectionString](intl.zh-CN/API参考/API参考/实例管理/ModifyDBInstanceConnectionString.md#)|修改实例连接地址|
|[UpgradeDBInstanceEngineVersion](intl.zh-CN/API参考/API参考/实例管理/UpgradeDBInstanceEngineVersion.md#)|升级引擎版本|
|[UpgradeDBInstanceKernelVersion](intl.zh-CN/API参考/API参考/实例管理/UpgradeDBInstanceKernelVersion.md#)|升级数据库小版本|
|[DescribeKernelReleaseNotes](intl.zh-CN/API参考/API参考/实例管理/DescribeKernelReleaseNotes.md#)|查询数据库小版本发布日志|
|[DestroyInstance](intl.zh-CN/API参考/API参考/实例管理/DestroyInstance.md#)|销毁MongoDB实例|

## 账号管理 {#section_ggn_rts_l2b .section}

|API|描述|
|---|--|
|[DescribeAccounts](intl.zh-CN/API参考/API参考/账号管理/DescribeAccounts.md#)|查询账号|
|[ResetAccountPassword](intl.zh-CN/API参考/API参考/账号管理/ResetAccountPassword.md#)|重置密码|
|[ModifyAccountDescription](intl.zh-CN/API参考/API参考/账号管理/ModifyAccountDescription.md#)|修改账户备注|

## 数据库安全管理 {#section_r1v_sts_l2b .section}

|API|描述|
|---|--|
|[DescribeSecurityIps](intl.zh-CN/API参考/API参考/安全管理/DescribeSecurityIps.md#)|查询实例访问白名单|
|[ModifySecurityIps](https://help.aliyun.com/document_detail/62157.html)|修改实例访问白名单|
|[DescribeAuditRecords](https://help.aliyun.com/document_detail/62158.html)|查询审计日志|
|[DescribeAuditFiles](https://help.aliyun.com/document_detail/62162.html)|查询审计日志文件|
|DescribeAuditPolicy|查询审计日志开通状态及日志保存时间|
|DescribeAuditLogFilter|查询审计日志的采集类型|
|ModifyAuditLogFilter|设置审计日志的采集类型|
|ModifyDBInstanceSSL|为实例设置SSL加密|
|DescribeDBInstanceSSL|查询实例的SSL设置详情|

## 备份与恢复 {#section_kdg_5ts_l2b .section}

|API|描述|
|---|--|
|[DescribeBackupPolicy](intl.zh-CN/API参考/API参考/备份与恢复/DescribeBackupPolicy.md#)|查看备份策略|
|[ModifyBackupPolicy](intl.zh-CN/API参考/API参考/备份与恢复/ModifyBackupPolicy.md#)|修改备份策略|
|[CreateBackup](intl.zh-CN/API参考/API参考/备份与恢复/CreateBackup.md#)|创建备份|
|[DescribeBackups](intl.zh-CN/API参考/API参考/备份与恢复/DescribeBackups.md#)|查看备份列表|
|[RestoreDBInstance](intl.zh-CN/API参考/API参考/备份与恢复/RestoreDBInstance.md#)|数据恢复|

## 监控报警管理 {#section_qjs_vts_l2b .section}

|API|描述|
|---|--|
|[DescribeDBInstancePerformance](https://help.aliyun.com/document_detail/62175.html)|查询实例性能数据|

## 参数管理 {#section_l21_xts_l2b .section}

|API|描述|
|---|--|
|[DescribeParameters](intl.zh-CN/API参考/API参考/参数管理/DescribeParameters.md#)|查询参数信息|
|[ModifyParameters](intl.zh-CN/API参考/API参考/参数管理/ModifyParameters.md#)|修改参数信息|
|[DescribeParameterModificationHistory](intl.zh-CN/API参考/API参考/参数管理/DescribeParameterModificationHistory.md#)|查询参数历史修改信息|
|[DescribeParameterTemplates](intl.zh-CN/API参考/API参考/参数管理/DescribeParameterTemplates.md#)|查看参数模板列表|

