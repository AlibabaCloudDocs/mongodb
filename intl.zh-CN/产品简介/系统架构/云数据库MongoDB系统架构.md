# 云数据库MongoDB系统架构 {#concept_lyt_gc5_xgb .concept}

## 系统架构图 {#section_akh_kc5_xgb .section}

![MongoDB系统架构](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132916/156704221539713_zh-CN.png)

## 主要组件说明 {#section_lzk_jc5_xgb .section}

-   HA控制系统

    高可用探测模块，用于探测MongoDB实例的运行状况。如果判断主节点实例不可用，则切换主备节点操作并通知用户，保障MongoDB实例的高可用。

-   日志收集系统

    收集MongoDB运行情况的日志信息，包括实例慢操作记录日志、审计日志等。

-   监控系统

    收集MongoDB实例的性能监控信息，包括基础指标、磁盘容量、网络请求以及操作次数等核心信息。

-   在线迁移系统

    当实例所运行的物理机出现故障，在线迁移系统会根据备份系统中的备份文件进行实例重新搭建，保证业务不受影响。

-   备份系统

    针对MongoDB实例进行备份处理，将生成的备份文件存储至OSS（Object Storage Service）中。目前MongoDB备份系统支持用户自定义备份策略的自动备份和手动备份，保存7天内的备份文件。

-   任务控制

    MongoDB实例支持多种管理控制任务，如创建实例、变更配置以及备份实例等。任务系统会根据您下发的操作指令，进行灵活控制并进行任务跟踪及出错管理。


