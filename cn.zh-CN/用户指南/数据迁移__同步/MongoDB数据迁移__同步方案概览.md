# MongoDB数据迁移/同步方案概览 {#concept_ujv_lml_cgb .concept}

云数据库MongoDB提供了多种数据迁移/同步方案，可满足不同业务场景下MongoDB数据库的数据迁移/同步需求。

## MongoDB数据迁移方案介绍 {#section_s1y_xz2_qgb .section}

通过使用阿里云[数据传输服务（DTS）](https://help.aliyun.com/document_detail/26592.html)工具，您可以实现MongoDB数据库的全量数据迁移和增量数据迁移，其中增量数据迁移可以在不影响业务的情况下平滑地将MongoDB数据库迁移上云。

云数据库MongoDB支持使用官方的mongodump 和mongorestore工具全量迁移数据库。

另外，云数据库MongoDB还支持通过物理备份文件和逻辑备份文件两种途径，将云上数据迁移到本地数据库。

|迁移场景|源库架构|文档链接|
|:---|:---|:---|
|将自建/本地数据库迁移上云|单节点|[使用DTS迁移单节点架构的自建MongoDB数据库上云](../../../../cn.zh-CN/单节点快速入门/数据迁移/使用DTS迁移单节点架构的自建MongoDB数据库上云.md#)|
|[使用MongoDB工具迁移单节点架构的MongoDB自建数据库上云](../../../../cn.zh-CN/单节点快速入门/数据迁移/使用MongoDB工具迁移自建数据库上云.md#)|
|副本集|[使用DTS迁移副本集架构的自建MongoDB数据库上云](../../../../cn.zh-CN/副本集快速入门/数据迁移/使用DTS迁移副本集架构的自建MongoDB数据库上云.md#)|
|[使用MongoDB工具迁移副本集架构的MongoDB自建数据库上云](../../../../cn.zh-CN/副本集快速入门/数据迁移/使用MongoDB工具迁移自建数据库上云.md#)|
|分片集群|[使用DTS迁移分片集群架构的自建MongoDB数据库上云](../../../../cn.zh-CN/分片集群快速入门/数据迁移/使用DTS迁移分片集群架构的自建MongoDB数据库上云.md#)|
|[使用MongoDB工具迁移分片集群架构的MongoDB自建数据库上云](../../../../cn.zh-CN/分片集群快速入门/数据迁移/使用MongoDB工具迁移自建数据库上云.md#)|
|第三方云迁移至阿里云|不涉及|[Amazon DynamoDB数据库迁移至阿里云](cn.zh-CN/用户指南/数据迁移__同步/第三方云迁移到阿里云/Amazon DynamoDB数据库迁移至阿里云.md#)|
|副本集/分片集群|[Atlas MongoDB数据库迁移至阿里云](cn.zh-CN/用户指南/数据迁移__同步/第三方云迁移到阿里云/Atlas MongoDB数据库迁移至阿里云.md#)|
|单节点/副本集|[华为云文档数据库迁移至阿里云MongoDB](cn.zh-CN/用户指南/数据迁移__同步/第三方云迁移到阿里云/从华为云文档数据库迁移至阿里云.md#)|
|副本集|[使用DTS将腾讯云MongoDB增量迁移至阿里云](cn.zh-CN/用户指南/数据迁移__同步/第三方云迁移到阿里云/使用DTS将腾讯云MongoDB增量迁移至阿里云.md#)|
|[使用DTS将腾讯云MongoDB全量迁移至阿里云](cn.zh-CN/用户指南/数据迁移__同步/第三方云迁移到阿里云/使用DTS将腾讯云MongoDB全量迁移至阿里云.md#)|
|[使用MongoDB工具将腾讯云MongoDB迁移至阿里云](cn.zh-CN/用户指南/数据迁移__同步/第三方云迁移到阿里云/使用MongoDB工具将腾讯云MongoDB迁移至阿里云.md#)|
|云数据库MongoDB实例间的迁移|副本集|[副本集实例迁移至分片集群实例](cn.zh-CN/用户指南/数据迁移__同步/MongoDB实例间迁移/从MongoDB副本集实例迁移至分片集群实例.md#)|
|单节点|[单节点实例迁移至副本集或分片集群实例](cn.zh-CN/用户指南/数据迁移__同步/MongoDB实例间迁移/从MongoDB单节点实例迁移至副本集或分片集群实例.md#)|
|单节点/副本集|[跨阿里云账号迁移MongoDB实例](cn.zh-CN/用户指南/数据迁移__同步/MongoDB实例间迁移/跨阿里云账号迁移MongoDB实例.md#)|
|将云数据库MongoDB迁移至自建/本地MongoDB数据库|副本集|[将逻辑备份迁移/恢复至本地MongoDB数据库](cn.zh-CN/用户指南/数据恢复/逻辑备份恢复至自建数据库.md#)|
|副本集|[将物理备份迁移/恢复至本地MongoDB数据库](cn.zh-CN/用户指南/数据恢复/物理备份恢复至自建数据库/将MongoDB物理备份文件恢复至自建数据库.md#)|

## MongoDB数据同步方案介绍 {#section_7fj_sq3_ccw .section}

您可以使用云上灾备功能或阿里云自研的MongoShake工具，实现MongoDB数据库间的数据同步。

|同步场景|同步工具|文档链接|
|:---|:---|:---|
|同步至新实例|不涉及|[创建云上灾备实例](cn.zh-CN/用户指南/云上灾备和多活/创建云上灾备实例.md#) **说明：** 更多信息，请参见[云上灾备和多活架构](cn.zh-CN/用户指南/云上灾备和多活/云上灾备和多活架构.md#)。

 |
|同步至已有实例|MongoShake|[使用MongoShake实现MongoDB副本集间的单向数据同步](cn.zh-CN/用户指南/数据迁移__同步/数据同步/使用MongoShake实现MongoDB副本集间的单向同步.md#)|

