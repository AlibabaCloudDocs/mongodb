# 使用MongoShake实现MongoDB实例间的延迟同步

本文档介绍如何通过MongoShake实现实例间的延迟同步。

MongoShake版本为2.4.6及以上。详情请参见[MongoShake发布页面](https://github.com/alibaba/MongoShake)。

在使用MongoShake实时同步多个实例时，当用户在主实例中执行了误操作以后，MongoShake会将该误操作实时同步到从实例，导致最终只能通过数据恢复来复原。因此，MongoShake在2.4.6版本的更新中提供了设置延迟同步的参数，给主从实例之间的同步设置一段缓冲的时间，当主实例中执行了误操作后，可以在这段时间内关闭同步，并直接将业务切换到还未发生误操作的从实例。

**说明：** 本文档着重介绍延迟同步参数`incr_sync.target_delay`，有关使用MongoShake的其他事项请参见[使用MongoShake实现MongoDB副本集间的单向同步](/cn.zh-CN/用户指南/数据迁移和同步/数据同步/使用MongoShake实现MongoDB副本集间的单向同步.md)。

## 准备工作

1.  为达到最理想的同步性能，请确保源端MongoDB副本集实例的网络类型为专有网络VPC，如果是经典网络，请切换成专有网络VPC。更多信息，请参见[切换实例网络类型](/cn.zh-CN/用户指南/管理网络连接/切换实例网络类型.md)。

2.  创建作为同步目标端的MongoDB副本集实例，在创建的时候请选择与源端MongoDB副本集实例相同的专有网络VPC，以获取最低的网络延迟。更多信息，请参见[创建副本集实例](/cn.zh-CN/快速入门/创建实例/创建副本集实例.md)。

3.  创建用于运行MongoShake的ECS实例，在创建的时候请选择与源端MongoDB副本集实例相同的专有网络VPC，以获取最低的网络延迟。更多信息，请参见[t9601.dita\#topic\_2386095]()。

4.  将ECS的内网IP地址加入至源端和目标端MongoDB实例的白名单中，并确保ECS可以连接源端和目标端MongoDB实例。 更多信息，请参见[设置白名单及安全组](/cn.zh-CN/用户指南/数据安全性/设置白名单及安全组.md)。


**说明：** 如果您没有达到上述网络类型的要求，可以分别申请源端和目标端MongoDB实例的公网连接地址，并将ECS的公网地址加入至源端和目标端MongoDB实例的白名单中，通过公网地址进行同步操作。更多信息，请参见[申请公网连接地址](/cn.zh-CN/用户指南/管理网络连接/公网连接地址/申请公网连接地址.md)和[设置白名单及安全组](/cn.zh-CN/用户指南/数据安全性/设置白名单及安全组.md)。

## 搭建MongoDB间的延迟同步架构

本示例以ECS上的Ubuntu系统为例介绍如何搭建延迟同步架构。详情请参见[准备工作](#section_3kv_hrf_0d1)。

1.  登录[ECS实例](https://help.aliyun.com/document_detail/25434.html)。

2.  执行如下命令格式下载MongoShake程序。

    ```
    wget 最新版MongoShake包下载地址
    ```

    示例：

    ```
    wget https://github.com/alibaba/MongoShake/releases/download/release-v2.0.7-20190817/mongo-shake-2.0.7.tar.gz
    ```

    **说明：** 最新版本的MongoShake包下载地址请参见[releases页面](https://github.com/alibaba/MongoShake/releases)。

3.  执行如下命令格式解压MongoShake程序。

    ```
    tar xvf mongoshake包文件名
    ```

    示例：

    ```
    tar xvf mongoshake-2.0.tar.gz
    ```

4.  执行`vi collector.conf`命令配置MongoShake。各参数说明请参见[MongoShake参数表](/cn.zh-CN/用户指南/数据迁移和同步/数据同步/使用MongoShake实现MongoDB副本集间的单向同步.md)。找到`incr_sync.target_delay`参数，根据实际业务需求设置该参数的值，单位为秒。本示例中将延迟时间设置为30分钟。

    ```
    incr_sync.target_delay = 1800
    ```

5.  保存并退出collector.conf文件，至此延迟同步架构已经搭建完毕。

6.  执行如下命令使用配置好的collector.conf文件开启同步，并打印日志信息。

    ```
    ./collector.linux -conf=collector.conf -verbose
    ```

    **说明：** 此时您在主实例中执行的任何更改，都将会在30分钟后同步到从实例。


## 误操作后切换主从实例

在主实例中日常执行CURD操作时，可能会存在某条语句误写入等误操作的情况发生，此时您可以通过下列步骤将业务切换到还没有发生误操作的从实例中。

1.  通过查询MongoDB的操作日志（oplog）定位到误操作发生的时间点。例如：您可以通过执行如下命令来查询2020年6月1日至2020年6月2日之间所有的操作日志。关于查询oplog的详情请参见[MongoDB官方文档](https://docs.mongodb.com/manual/reference/command/find/)。

    ```
    use local #切换到local数据库
    db.oplog.rs.find({"o.createTime": {$gte:new Date(2020,6,1),$lte:new Date(2020,6,2)}}) #根据条件查看oplog。
    ```

2.  通过RESTful接口远程向MongoShake注入ExitPoint参数来实现在指定时间点终止MongoShake程序的目的。命令格式如下：

    ```
    curl -X POST --data '{"ExitPoint": <Unix时间戳>}' <MongoShake服务器ID>:<端口号>/sentinel/options
    ```

    示例：

    ```
    curl -X POST --data '{"ExitPoint": 1593534600}' 127.0.0.1:9100/sentinel/options
    ```

    **说明：** `1593534600`是Unix时间戳，表示2020年6月30日16:30:00。MongoShake同步到这个时间点后将会自动退出。

3.  执行`vi collector.conf`命令打开配置文件，将原主从实例的地址调换。详细操作方法请参见[使用MongoShake实现MongoDB副本集间的单向同步](/cn.zh-CN/用户指南/数据迁移和同步/数据同步/使用MongoShake实现MongoDB副本集间的单向同步.md)。

4.  执行如下命令使用配置好的collector.conf文件重新开启同步，并打印日志信息。

    ```
    ./collector.linux -conf=collector.conf -verbose
    ```

5.  将业务切换到最新的主实例上，完成主从实例切换操作。


## 监控MongoShake状态

详情请参见[监控MongoShake状态](/cn.zh-CN/用户指南/数据迁移和同步/数据同步/使用MongoShake实现MongoDB副本集间的单向同步.md)。

