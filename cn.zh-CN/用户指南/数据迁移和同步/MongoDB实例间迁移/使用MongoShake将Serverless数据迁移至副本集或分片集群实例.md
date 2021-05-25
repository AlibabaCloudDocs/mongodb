# 使用MongoShake将Serverless数据迁移至副本集或分片集群实例

通过阿里云自主研发的MongoShake开源工具，您可以实现MongoDB数据库间数据的迁移与同步。本文介绍使用MongoShake迁移MongoDB Serverless实例中的数据至MongoDB副本集实例或分片集群实例的方法。

## 影响

-   迁移任务会消耗源端的部分读写吞吐量CU。关于读写吞吐量CU的更多信息，请参见[读写吞吐量CU](/cn.zh-CN/MongoDB Serverless版/什么是MongoDB Serverless版.md)。
-   迁移过程中对源端进行读取或写入操作，可能会出现读取或写入不响应的现象。

## 数据库账号的权限要求

|实例|权限|
|--|--|
|源端MongoDB Serverless实例|readWrite权限。|
|目标端MongoDB副本集实例或分片集群实例|readWrite权限。|

数据库账号创建及授权方法请参见[使用DMS管理MongoDB数据库用户](/cn.zh-CN/用户指南/账号管理/MongoDB数据库账号权限管理.md)。

## 准备工作

1.  为达到最理想的同步性能，请确保源端MongoDB Serverless实例的网络类型为专有网络VPC，如果是经典网络，请切换成专有网络VPC。更多信息，请参见[切换实例网络类型](/cn.zh-CN/用户指南/管理网络连接/切换实例网络类型.md)。

2.  创建作为同步目标端的MongoDB副本集实例或分片集群实例，在创建的时候请选择与源端MongoDB Serverless实例相同的专有网络VPC，以获取最低的网络延迟。更多信息，请参见[创建副本集实例](/cn.zh-CN/快速入门/创建实例/创建副本集实例.md)或[创建分片集群实例](/cn.zh-CN/快速入门/创建实例/创建分片集群实例.md)。

    **说明：** 如果目标端为分片集群实例，您需要为目标端数据库开启分片功能并对集合设置片键（shardkey），设置方法请参见[设置数据分片以充分利用Shard性能](/cn.zh-CN/最佳实践/性能/设置数据分片以充分利用Shard性能.md)。

3.  创建用于运行MongoShake的ECS实例，在创建的时候请选择与源端MongoDB Serverless实例相同的专有网络VPC，以获取最低的网络延迟。更多信息，请参见[t9601.dita\#topic\_2386095]()。

4.  将ECS的内网IP地址加入至源端和目标端MongoDB实例的白名单中，并确保ECS可以连接源端和目标端MongoDB实例。 更多信息，请参见[设置白名单及安全组](/cn.zh-CN/用户指南/数据安全性/设置白名单及安全组.md)。


**说明：** 如果您没有达到上述网络类型的要求，可以分别申请源端和目标端MongoDB实例的公网连接地址，并将ECS的公网地址加入至源端和目标端MongoDB实例的白名单中，通过公网地址进行同步操作。更多信息，请参见[申请公网连接地址](/cn.zh-CN/用户指南/管理网络连接/公网连接地址/申请公网连接地址.md)和[设置白名单及安全组](/cn.zh-CN/用户指南/数据安全性/设置白名单及安全组.md)。

## 操作步骤

下面以使用私网登录ECS服务器（Alibaba Cloud Linux操作系统）为例介绍迁移步骤。

1.  登录ECS实例，具体方法请参见[登录ECS实例](/cn.zh-CN/实例/连接实例/连接方式概述.md)。

2.  执行如下命令，下载最新版本的MongoShake程序。

    ```
    wget 最新版本MongoShake包下载地址
    ```

    示例：

    ```
    wget https://github.com/alibaba/MongoShake/releases/download/release-v2.6.4-20210414/mongo-shake-v2.6.4_2.tar.gz
    ```

    **说明：** 示例提供的下载地址是MongoShake 2.6.4\_2版本，最新版MongoShake下载地址，请参见[MongoShake releases](https://github.com/alibaba/MongoShake/releases)。

3.  执行如下命令，解压MongoShake程序。

    ```
    tar xvf mongoshake包文件名
    ```

    示例：

    ```
    tar xvf mongo-shake-v2.6.4_2.tar.gz
    ```

4.  执行如下命令，进入collector.conf所在目录。

    ```
    cd 配置文件collector.conf所在目录
    ```

    示例：

    ```
    cd mongo-shake-v2.6.4
    ```

5.  执行如下命令，修改MongoShake的配置文件collector.conf。

    ```
    vi collector.conf
    ```

    进入vi编辑器后，输入i，修改以下字段的值：

    |参数|说明|示例|
    |--|--|--|
    |sync\_mode|数据同步的方式，默认值为incr，请配置为all。    -   all：执行全量数据同步和增量数据同步。
    -   full：仅执行全量数据同步。
    -   incr：仅执行增量数据同步。
|`sync_mode = all`|
    |mongo\_urls|源端MongoDB ServerLess实例的ConnectionStringURI格式连接地址。 **说明：**

    -   建议通过专有网络地址进行互连，以获取最低的网络延迟。
    -   关于ConnectionStringURI格式详情请参见[Serverless实例连接说明]()。
|`mongo_urls = mongodb://user46436397:********@dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717/admin`**说明：** 密码中不得包含艾特（@）字符，否则会导致连接失败。 |
    |tunnel.address|目标端MongoDB实例的ConnectionStringURI格式连接地址。**说明：**

    -   建议通过专有网络地址进行互连，以获取最低的网络延迟。
    -   关于ConnectionStringURI格式详情请参见[副本集实例连接说明]()或[分片集群实例连接说明]()。
|`tunnel.address = mongodb://root:****@dds-bpxxxxxxx.mongodb.rds.aliyuncs.com:3717,dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717/admin?replicaSet=mgset-xxxxxx`**说明：** 密码中不得包含艾特（@）字符，否则会导致连接失败。 |
    |filter.ddl\_enable|是否开启DDL同步，默认值为false，请配置为true。    -   true：开启
    -   false：关闭
|`filter.ddl_enable = true`|
    |full\_sync.reader.collection\_parallel|设置MongoShake单次最多并发拉取多少个集合，默认值为6，请配置为1。|`full_sync.reader.collection_parallel = 1`|
    |full\_sync.reader.write\_document\_parallel|设置MongoShake对单个集合写入的并发线程数，默认值为8，请配置为4。|`full_sync.reader.write_document_parallel = 4`|
    |full\_sync.create\_index|完成同步后是否创建索引，请配置为foreground。    -   foreground：创建前台索引
    -   background：创建后台索引
    -   none：不创建索引
|`full_sync.create_index = foreground`|
    |incr\_sync.mongo\_fetch\_method|配置数据库的拉取方法，默认值为oplog，请配置为change\_stream。    -   oplog：从源端中拉取oplog。
    -   change\_stream：从源端中拉取change事件（仅支持MongoDB 4.0及以上版本，对于部分DDL的同步，仅支持库表的创建、删除和重命名）。
|`incr_sync.mongo_fetch_method = change_stream`|
    |special.source.db.flag|特殊形态支持。请配置为aliyun\_serverless。|`special.source.db.flag = aliyun_serverless`|

    **说明：** 关于collector.conf全量参数说明，请参见[附件](/cn.zh-CN/用户指南/数据迁移和同步/数据同步/使用MongoShake实现MongoDB副本集间的单向同步.md)中的collector.conf全量参数说明。

    修改完成后，按ESC键，输入:wq!并按Enter。

6.  执行如下命令，启动迁移任务。

    ```
    ./collector.linux -conf=collector.conf &
    ```

    **说明：** 由于MongoDB Serverless实例受到读写吞吐量CU的限制，迁移速度较慢，请您耐心等待。

7.  执行如下命令，进入日志文件collector.log所在目录。查看日志信息。

    ```
    cd logs
    ```

8.  执行如下命令，查看日志信息。

    ```
    vi collector.log
    ```

    当日志信息中出现如下信息时，说明全量数据迁移已完成并进入增量数据迁移模式。

    ```
    [2021/04/30 14:20:38 CST] [INFO] ------------------------full sync done!------------------------
    ```

    查看完成后，按ESC键，输入:q并按Enter。

9.  查看增量迁移数据是否与当前时间点数据一致。

    1.  执行如下命令，进入MongoShake程序的安装目录。

        ```
        cd - MongoShake程序的安装目录
        ```

        示例：

        ```
        cd - mongo-shake-v2.6.4
        ```

    2.  执行如下命令，查看增量迁移数据是否与当前时间点数据一致。

        ```
        curl -s http://127.0.0.1:9100/repl | python -m json.tool
        ```

        回显类似如下信息，部分参数说明请参见[\#table\_6xm\_imr\_zj2](#table_6xm_imr_zj2)。

        ```
        {
            "log_size_avg": "320.00B",
            "log_size_max": "332.00B",
            "logs_get": 5,
            "logs_repl": 5,
            "logs_success": 5,
            "lsn": {
                "time": "2021-05-21 14:18:37",
                "ts": "6964624121430802437",
                "unix": 1621577917
            },
            "lsn_ack": {
                "time": "2021-05-21 14:18:37",
                "ts": "6964624121430802437",
                "unix": 1621577917
            },
            "lsn_ckpt": {
                "time": "2021-05-21 14:19:19",
                "ts": "0",
                "unix": 0
            },
            "now": {
                "time": "2021-05-21 14:19:19",
                "unix": 1621577959
            },
            "replset": "default-0",
            "tag": "$",
            "tps": 0,
            "who": "mongoshake"
        }
        ```

        当`lsn_ckpt`和`now`的`time`值相同时，说明增量迁移与当前时间一致。


## 参数说明

|参数|说明|
|--|--|
|`logs_get`|拉取的oplog总数。|
|`logs_repl`|尝试写入目标库的oplog总数。|
|`logs_success`|成功写入目标库的oplog总数。|
|`lsn`|拉取数据的checkpoint时间，即初始时间，当前没有数据写入。|
|`lsn_ack`|成功写入目标库的checkpoint时间，该时间会随着数据写入变化。|
|`lsn_ckpt`|成功写入目标库的checkpoint时间，该时间已经稳定持久。|
|`now`|当前时间。|
|`replset`|源端名称。|

