# 如何查询及限制连接数

您可以通过DMS或Mongo Shell登录MongoDB数据库，本文介绍如何查询连接使用情况以及设置连接池的连接数。

## 查询当前连接数

根据您购买的MongoDB实例规格不同，最大连接数也不同，详情请参见[实例规格](/cn.zh-CN/产品简介/实例规格表.md)。

**说明：** 最大连接数是指实例中每个节点的最大连接数，例如您购买了1核2G规格的三节点副本集实例，那么该实例的Primary节点和Secondary节点的最大连接数均为500，Hidden节点由于其架构特殊性，不对外提供服务。

通过Mongo Shell连接实例，详情请参见[连接实例](/cn.zh-CN/用户指南/连接实例/连接实例.md)，然后执行命令`db.serverStatus().connections`。

```
mgset-123456:PRIMARY> db.serverStatus().connections
{
        "current" : 1,
        "available" : 999,
        "internal_current" : 10,
        "internal_available" : 990,
        "totalCreated" : 632
}             
```

**说明：** 您需要关注以下参数及对应的值。

-   "current" ：当前已经建立的连接数。
-   "available" ：当前可用的连接数。

## 查询当前连接来源

1.  通过Mongo Shell连接实例，详情请参见[连接实例](/cn.zh-CN/用户指南/连接实例/连接实例.md)，然后切换至admin数据库。

    ```
    use admin
    ```

2.  执行命令`db.runCommand({currentOp: 1, $all: true})`。

    ```
    mgset-123456:PRIMARY> db.runCommand({currentOp: 1, $all:[{"active" : true}]})                    
    ```


通过分析命令的输出结果，您可以查询每个连接对应的来源IP地址，从而得出各终端与MongoDB实例分别建立了多少连接。更多详情请参见[官方文档](https://docs.mongodb.com/manual/reference/method/db.currentOp/index.html)。

## 如何限制终端的连接数

云数据库MongoDB支持通过Connection String URI连接数据库。通过Connection String URI连接数据库时，在URI末尾加上`&maxPoolSize=<integer>`即可设置连接池的连接数。

Mongo Shell连接示例（设置连接数为10）：

```
mongo "mongodb://root:xxxxxx@dds-bpxxxxxxxx-pub.mongodb.rds.aliyuncs.com:3717,dds-bpxxxxxxxx-pub.mongodb.rds.aliyuncs.com:3717/admin?replicaSet=mgset-xxxxxx&maxPoolSize=10"
```

**说明：** 关于不同语言的客户端如何限制连接池的数量，请参见[MongoDB官网的API文档](https://docs.mongodb.com/ecosystem/drivers/)。

