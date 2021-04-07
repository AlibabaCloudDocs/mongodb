# 解决因磁盘空间耗尽导致的锁定或无法写入问题

当MongoDB实例的磁盘空间被耗尽后，实例的状态将转变为锁定中，处于该状态的实例将无法写入或删除数据。本文将介绍如何排查因磁盘空间耗尽导致的无法写入问题。

## 故障表现

-   部署的应用程序突然无法将数据写入数据库，但是可以正常读取数据。
-   管理人员通过Mongo Shell连接数据库进行排查时，测试写入一条数据，返回错误信息：`not authorized on xxxx to execute command`，例如：

    ```
    db.customer.insert({"name":"zhangsan"})
    WriteCommandError({
            "operationTime" : Timestamp(1563437183, 1),
            "ok" : 0,
            "errmsg" : "not authorized on db1 to execute command { insert: \"customer\", ordered: true, lsid: { id: UUID(\"8d43461c-5c51-49ef-b9b3-9xxxxxxxxf\") }, $clusterTime: { clusterTime: Timestamp(1563437183, 1), signature: { hash: BinData(0, 0C3FAAE747xxxxxx), keyId: 668293399xxxxxx } }, $db: \"db1\" }",
            "code" : 13,
            "codeName" : "Unauthorized",
            "$clusterTime" : {
                    "clusterTime" : Timestamp(1563437183, 1),
                    "signature" : {
                            "hash" : BinData(0,"DD+q50dPTuIQKTzytT5SiTPYX4Q="),
                            "keyId" : NumberLong("66xxxxxxxx")
                    }
            }
    })
    ```

-   管理人员通过MongoDB控制台，查看到实例的状态处于**锁定中**。

    **说明：** 由于分片集群架构的特殊性，当分片集群实例磁盘空间被占满后，实例不会显示为**锁定中**。


## 检查磁盘空间是否被耗尽

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。

2.  在页面左上角，选择实例所在的资源组和地域。

3.  根据实例类型，在左侧导航栏单击**副本集实例列表**或**分片集群实例列表**。

4.  找到目标实例，单击实例ID。

5.  根据实例类型，选择下述步骤进行操作。

    **说明：** 磁盘空间使用率的数据采集粒度为5分钟。

    -   单节点或副本集实例

        在**基本信息**页面，确认实例状态及磁盘空间的使用率信息。本案例中，实例状态为**锁定中**，同时查看到实例的磁盘空间使用率超过了100%，由此可判断磁盘空间被耗尽。

        ![查看磁盘空间使用率](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4774797951/p51781.png)

    -   分片集群实例
        1.  单击左侧导航栏的**监控信息**。
        2.  在**监控信息**页面顶部，筛选所需查看的Shard节点。

            ![选择Shard节点](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4774797951/p51878.png)

            **说明：** 以`d`开头的节点ID为Shard节点，以`s`开头的节点ID为Mongos节点。

        3.  查看磁盘空间使用率。本案例中，查看到Shard节点的磁盘空间的使用率超过了100%，由此可判断磁盘空间被耗尽。

            ![查看磁盘空间使用率](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4774797951/p51879.png)


## 解决方法

-   通过[t6706.md\#](/intl.zh-CN/用户指南/实例管理/变更实例配置/变更配置方案概览.md)来提升实例的磁盘空间。

    **说明：** 不同的实例规格对应的最大磁盘空间有所不同，详情请参见[实例规格表](/intl.zh-CN/产品简介/实例规格表.md)。

-   副本集实例的最高规格中，可配置的最大磁盘空间为3,000GB。如果您的业务预期会超过此限制，建议使用[分片集群实例](/intl.zh-CN/产品简介/系统架构/分片集群架构.md)，通过扩展Shard节点的方式横向扩展磁盘空间，最高可扩展至96,000GB。

    **说明：** 源实例的数据可通过DTS迁移至新的分片集群实例，详情请参见[从MongoDB副本集实例迁移至分片集群实例](/intl.zh-CN/用户指南/数据迁移和同步/MongoDB实例间迁移/从MongoDB副本集实例迁移至分片集群实例.md)。


## 优化建议

如果您的实例使用`db.collection.remove`命令删除了大量数据或没有整理过碎片，您可以[整理物理空间碎片以提升磁盘利用率](/intl.zh-CN/最佳实践/性能/整理物理空间碎片以提升磁盘利用率.md)。

