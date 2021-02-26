---
keyword: [数据库迁移, mongodb迁移, 阿里云数据库同步, 数据库同步, 数据库同步工具]
---

# MongoDB数据迁移和同步方案概览

云数据库MongoDB提供了多种数据迁移和同步方案，可满足不同业务场景下MongoDB数据库的数据迁移和同步需求。

## 影响

如果您的数据库小版本过期或者不在维护列表内，当执行[实例版本升级](/intl.zh-CN/用户指南/实例管理/数据库升级/升级数据库版本.md)、[数据迁移](/intl.zh-CN/用户指南/数据迁移和同步/MongoDB数据迁移和同步方案概览.md)、[变更实例配置](/intl.zh-CN/用户指南/实例管理/变更实例配置/变更配置方案概览.md)、[从备份点创建实例](/intl.zh-CN/用户指南/数据恢复/从备份点创建实例.md)、[按时间点新建实例](/intl.zh-CN/用户指南/数据恢复/按时间点新建实例.md)或[MongoDB单库恢复](/intl.zh-CN/用户指南/数据恢复/MongoDB单库恢复.md)等操作时，为保证提供更出色的性能和稳定性，系统会默认将您的数据库小版本升级至最新版。

## MongoDB数据迁移方案介绍

通过[数据传输服务（DTS）](数据传输服务（DTS）t17063.dita#concept_26592_zh)，您可以实现MongoDB数据库的全量数据迁移和增量数据迁移，在不影响业务的情况下平滑地将MongoDB数据库迁移上云。

云数据库MongoDB支持使用官方的mongodump和mongorestore工具全量迁移数据库。

另外，云数据库MongoDB还支持通过物理备份文件和逻辑备份文件两种途径，将云上数据迁移到本地数据库。

|迁移场景|源库架构|文档链接|
|:---|:---|:---|
|将自建或本地数据库迁移上云|单节点|[使用DTS迁移单节点架构的自建MongoDB数据库上云](/intl.zh-CN/快速入门/数据迁移/使用DTS迁移单节点架构的自建MongoDB数据库上云.md)|
|[使用MongoDB工具将自建数据库迁移至单节点实例](/intl.zh-CN/快速入门/数据迁移/使用MongoDB工具将自建数据库迁移至单节点实例.md)|
|副本集|[使用DTS迁移副本集架构的自建MongoDB数据库上云](/intl.zh-CN/快速入门/数据迁移/使用DTS迁移副本集架构的自建MongoDB数据库上云.md)|
|[使用MongoDB工具将自建数据库迁移至副本集实例](/intl.zh-CN/快速入门/数据迁移/使用MongoDB工具将自建数据库迁移至副本集实例.md)|
|分片集群|[使用DTS迁移分片集群架构的自建MongoDB数据库上云](/intl.zh-CN/快速入门/数据迁移/使用DTS迁移分片集群架构的自建MongoDB数据库上云.md)|
|[使用MongoDB工具将自建数据库迁移至分片集群实例](/intl.zh-CN/快速入门/数据迁移/使用MongoDB工具迁移自建数据库上云.md)|
|第三方云迁移至阿里云|不涉及|[使用MongoDB工具将Amazon DynamoDB迁移至阿里云](/intl.zh-CN/用户指南/数据迁移和同步/第三方云迁移到阿里云/使用MongoDB工具将Amazon DynamoDB迁移至阿里云.md)|
|副本集或分片集群|-   [使用MongoDB工具将MongoDB Atlas迁移至阿里云](/intl.zh-CN/用户指南/数据迁移和同步/第三方云迁移到阿里云/使用MongoDB工具将MongoDB Atlas迁移至阿里云.md)
-   [使用DTS将MongoDB Atlas数据库迁移至阿里云](/intl.zh-CN/用户指南/数据迁移和同步/第三方云迁移到阿里云/使用DTS将MongoDB Atlas数据库迁移至阿里云.md) |
|云数据库MongoDB实例间的迁移|副本集|[从MongoDB副本集实例迁移至分片集群实例](/intl.zh-CN/用户指南/数据迁移和同步/MongoDB实例间迁移/从MongoDB副本集实例迁移至分片集群实例.md)|
|单节点|[从MongoDB单节点实例迁移至副本集或分片集群实例](/intl.zh-CN/用户指南/数据迁移和同步/MongoDB实例间迁移/从MongoDB单节点实例迁移至副本集或分片集群实例.md)|
|单节点或副本集|[跨阿里云账号迁移MongoDB实例](/intl.zh-CN/用户指南/数据迁移和同步/MongoDB实例间迁移/跨阿里云账号迁移MongoDB实例.md)|
|将云数据库MongoDB迁移至自建或本地MongoDB数据库|副本集|[逻辑备份恢复至自建数据库](/intl.zh-CN/用户指南/数据恢复/逻辑备份恢复至自建数据库.md)|
|[将MongoDB物理备份文件恢复至自建数据库](/intl.zh-CN/用户指南/数据恢复/物理备份恢复至自建数据库/将MongoDB物理备份文件恢复至自建数据库.md)|

## MongoDB数据同步方案介绍

您可以阿里云自研的MongoShake工具，实现MongoDB数据库间的数据同步。

|同步场景|同步工具|文档链接|
|:---|:---|:---|
|同步至已有实例|MongoShake|[使用MongoShake实现MongoDB副本集间的单向同步](/intl.zh-CN/用户指南/数据迁移和同步/数据同步/使用MongoShake实现MongoDB副本集间的单向同步.md)|

