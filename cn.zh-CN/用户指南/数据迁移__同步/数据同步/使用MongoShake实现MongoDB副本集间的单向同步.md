# 使用MongoShake实现MongoDB副本集间的单向同步 {#concept_761647 .concept}

通过阿里云自研的MongoShake工具，您可以实现MongoDB数据库间的数据同步，该功能可用于数据分析、灾备和多活等业务场景。本文介绍副本集实例间的单向数据同步的操作流程。

**说明：** 如果您需要实现副本集实例间的双向数据同步，您可以[提交工单](https://workorder-intl.console.aliyun.com/console.htm#/ticket/createIndex)申请。

## MongoShake介绍 {#section_b2y_51c_5hb .section}

MongoShake是阿里云以golang语言编写的通用平台型服务工具，它通过读取MongoDB的Oplog操作日志来复制MongoDB的数据以实现特定需求。

MongoShake还提供了日志数据的订阅和消费功能，可通过SDK、Kafka、MetaQ等方式的灵活对接，适用于日志订阅、数据中心同步、Cache异步淘汰等场景。

**说明：** 如需了解更多MongoShake相关信息，请参见[MongoDB-shake Github主页](https://github.com/alibaba/MongoShake)。

## 支持的数据源 {#section_cd4_rgd_5hb .section}

|源数据库|目标数据库|
|:---|:----|
| -   ECS上的自建MongoDB数据库
-   本地自建的MongoDB数据库
-   阿里云MongoDB实例
-   第三方云MongoDB数据库

 | -   ECS上的自建MongoDB数据库
-   本地自建的MongoDB数据库
-   阿里云MongoDB实例
-   第三方云MongoDB数据库

 |

本文以云数据库MongoDB实例间的数据实时同步为例介绍配置流程，该方法也同样适用于自建数据库之间的数据同步。

## 注意事项 {#section_miw_yxe_g61 .section}

-   在全量数据同步完成之前，请勿对源库进行DDL操作，否则可能导致数据不一致。
-   不支持同步admin和local数据库。

## 数据库用户的权限要求 {#section_xyh_iy0_v2p .section}

|同步的数据源|所需权限|
|:-----|:---|
|源MongoDB实例|readAnyDatabase权限、local库的read权限和mongoshake库的readWrite权限。|
|目标MongoDB实例|readWriteAnyDatabase权限或目标库的readWrite权限。|

**说明：** 关于MongoDB数据库用户的创建及授权操作请参见[使用DMS管理MongoDB数据库用户](intl.zh-CN/用户指南/账号管理/使用DMS管理MongoDB数据库用户.md#)或[db.createUser命令介绍](https://docs.mongodb.com/manual/reference/method/db.createUser/index.html)。

## 准备工作 {#section_7k2_hmq_6u0 .section}

1.  创建作为同步目标端的MongoDB副本集实例，详情请参见[创建副本集实例](../../../../intl.zh-CN/副本集快速入门/创建副本集实例.md#)。

    **说明：** 选择与源端的MongoDB实例相同的专有网络，便于ECS通过专有网络进行连接。

2.  创建用于运行MongoShake的ECS实例，详情请参见[创建ECS实例](https://www.alibabacloud.com/help/zh/doc-detail/25424.htm)。

    **说明：** ECS的操作系统选择为Linux，并选择与MongoDB实例相同的专有网络。

3.  将ECS的IP地址加入至源端和目标端MongoDB实例的白名单中，并确保ECS可以连接源端和目标端MongoDB实例。

    **说明：** 建议通过专有网络进行互连，以获取最低的网络延迟。


## 操作步骤 {#section_wqw_bcd_5hb .section}

1.  [登录ECS实例](https://www.alibabacloud.com/help/zh/doc-detail/25434.htm)。
2.  执行下述命令，下载MongoShake程序。

    ``` {#codeblock_6rv_7hr_gjb}
    wget https://github.com/alibaba/MongoShake/releases/download/release-v2.0.0-20190619/mongoshake-2.0.tar.gz
    ```

3.  解压MongoShake程序。

    ``` {#codeblock_wy3_xj6_l9g}
    tar xvf mongoshake-2.0.tar.gz
    ```

4.  通过`vim`命令，修改MongoShake的配置文件collector.conf，涉及的主要参数的说明如下表所示。

    |参数|说明|示例值|
    |:-|:-|:--|
    |mongo\_urls|源端MongoDB实例的ConnectionStringURI格式连接地址。 **说明：** 

    -   建议通过专有网络地址进行互连，以获取最低的网络延迟。
    -   关于ConnectionStringURI格式详情请参见[副本集实例连接说明](../../../../intl.zh-CN/副本集快速入门/连接实例/副本集实例连接说明.md#)。
 |`mongo_urls = mongodb://root:Ftxxxxxx@dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717,dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717`|
    |tunnel.address|目标端MongoDB实例的ConnectionStringURI格式连接地址。|`tunnel.address = mongodb://root:Ftxxxxxx@dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717,dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717`|
    |sync\_mode|数据同步的方式，取值：     -   **all**：执行全量数据同步和增量数据同步。
    -   **document**：仅执行全量数据同步。
    -   **oplog**：仅执行增量数据同步。
 **说明：** 默认取值为**opolog**。

 |`sync_mode = all`|
    |replayer.dml\_only|是否仅同步DML操作，取值：     -   **false**：同步DML操作和DDL操作。
    -   **true**：仅同步DML操作。
 **说明：** 默认取值为**true**。

 |`replayer.dml_only = false`|
    |filter.namespace.black|指定数据同步的黑名单，这些指定的命名空间不会被同步至目标数据库，多个命名空间用英文分号（;）分隔。 **说明：** 命名空间是指MongoDB中集合或索引的规范名称，是由数据库名称和集合/索引名称的组合，例如`mongodbtest.customer`。

 |`filter.namespace.black = mongodbtest.customer;testdata.test123`|
    |filter.namespace.white|指定数据同步的白名单，只有这些指定的命名空间会被同步至目标数据库，多个命名空间用英文分号（;）分隔。|`filter.namespace.white = mongodbtest.customer;test123`|

5.  执行下述命令启动同步任务，并打印日志信息。

    ``` {#codeblock_odl_801_cbn}
    ./collector -conf=collector.conf -verbose
    ```

6.  观察打印的日志信息，当出现如下日志时，即代表全量数据同步已完成，并进入增量数据同步模式。

    ``` {#codeblock_ni6_9y5_fam}
    [09:38:57 CST 2019/06/20] [INFO] (mongoshake/collector.(*ReplicationCoordinator).Run:80) finish full sync, start incr sync with timestamp: fullBeginTs[1560994443], fullFinishTs[1560994737]
    ```


## 监控MongoShake状态 {#section_537_5ui_a5u .section}

增量数据同步开始后，您可以再开启一个命令行窗口，通过如下命令来监控MongoShake。

``` {#codeblock_6rh_bzr_pbw}
./mongoshake-stat --port=9100
```

监控输出示例：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/614897/156496828249777_zh-CN.png)

|参数|说明|
|--|--|
|logs\_get/sec|每秒获取的oplog数量。|
|logs\_repl/sec|每秒执行重放操作的oplog数量。|
|logs\_success/sec|每秒成功执行重放操作的oplog数量。|
|lsn.time|最后发送oplog的时间。|
|lsn\_ack.time|目标端确认写入的时间。|
|lsn\_ckpt.time|Check Point持久化的时间。|
|now.time|当前时间。|
|replset|源数据库的副本集名称。|

