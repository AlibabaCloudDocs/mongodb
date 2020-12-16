---
keyword: [备份恢复, 数据库恢复]
---

# 将MongoDB物理备份文件恢复至自建数据库

您可以通过控制台下载MongoDB实例的物理备份文件。本文介绍如何将MongoDB物理备份中的数据，恢复至本地自建的MongoDB数据库中。

## 前提条件

-   实例类型为副本集。
-   实例未开启[TDE功能](/cn.zh-CN/用户指南/数据安全性/设置透明数据加密TDE.md)。
-   实例的存储引擎为WiredTiger或RocksDB。如果实例的存储引擎为TerarkDB ，请使用[逻辑备份恢复至自建数据库](/cn.zh-CN/用户指南/数据恢复/逻辑备份恢复至自建数据库.md)。

    **说明：**

    -   您可以在控制台的**基本信息**页面中查看实例的存储引擎。
    -   实例的存储引擎为RocksDB时，您需要自行编译安装带有RocksDB存储引擎的MongoDB应用程序。
-   备份数据的数据库版本和需要恢复的自建数据库版本一致。

## 数据库版本要求

|MongoDB实例|自建MongoDB数据库|
|:--------|:-----------|
|3.2版本|3.2或3.4版本|
|3.4版本|3.4版本|
|4.0版本|4.0版本|
|4.2版本|4.2版本|

## 物理备份文件格式说明

|物理备份文件格式|文件后缀|说明|
|--------|----|--|
|tar压缩包|.tar.gz|2019年3月26日之前创建的实例，物理备份文件格式为tar压缩包。|
|xbstream文件包|\_qp.xb|2019年3月26日及之后创建的实例，物理备份文件格式为xbstream文件包。|

**说明：** 上述两种格式的文件，对应的解压操作有所不同，详情请参见[下载及解压物理备份文件](#section_lxg_5xp_5fb)。

## 演示环境说明

以下演示所用的服务器为阿里云ECS实例，镜像为Ubuntu 16.04（64位），更多详情请参见[创建ECS实例](~~25424~~)。

**说明：**

-   该服务器已安装对应版本的MongoDB，安装方法请参见[MongoDB官方文档](https://docs.mongodb.com/guides/server/install/)。
-   该服务器将/root/mongo/data作为MongoDB物理恢复操作的数据库所在目录（该目录是空的）。

## 下载及解压物理备份文件

1.  [下载MongoDB物理备份文件](/cn.zh-CN/用户指南/数据恢复/物理备份恢复至自建数据库/副本集实例下载物理备份.md)，您可以通过如下命令进行下载。

    ```
    wget "<物理备份文件链接>"
    ```

    **说明：** 通过`wget`下载的文件末尾可能会存在多余字符，请根据实际情况删除多余字符，确保文件后缀名为`.tar.gz`或`_qp.xb`

2.  将下载的MongoDB物理备份文件移动到/root/mongo/data/目录中。

    ```
    mv <物理备份文件名> /root/mongo/data
    ```

3.  对物理备份文件执行解压操作。
    -   当下载的物理备份文件后缀为.tar.gz时，例如文件名为hins20190412.tar.gz，请使用下述方法解压。

        ```
        cd /root/mongo/data/
        tar xzvf hins20190412.tar.gz 
        ```

        ![解压结果](../images/p70466.png "解压结果")

    -   当下载的物理备份文件后缀为\_qp.xb时，例如文件名为hins20190412\_qp.xb，请使用下述方法解压。
        1.  安装percona-xtrabackup工具。

            ```
            apt-get update
            apt install percona-xtrabackup
            ```

        2.  前往[QuickLZ网站](http://www.quicklz.com/)，下载qpress工具。
        3.  解压并安装qpress工具。

            ```
            tar xvf qpress-11-linux-x64.tar
            chmod 775 qpress
            cp qpress /usr/bin
            ```

        4.  解压物理备份文件，例如数据库备份文件名为hins20190412\_qp.xb。

            ```
            cd /root/mongo/data/
            cat hins20190412_qp.xb | xbstream -x -v
            innobackupex --decompress --remove-original /root/mongo/data
            ```

            ![解压结果](../images/p70454.png "解压结果")


## 以单节点模式恢复MongoDB物理备份的数据

1.  在/root/mongo文件夹中新建配置文件mongod.conf。

    ```
    touch mongod.conf
    ```

2.  修改mongod.conf配置文件，使得符合启动的配置要求。

    根据云数据库MongoDB版的存储引擎选择启动的配置模板，您可以将其复制到mongod.conf文件中。

    **说明：** 配置文件设置了启动模式为单节点模式并开启认证功能。

    -   WiredTiger存储引擎

        ```
        systemLog:
            destination: file
            path: /root/mongo/mongod.log
            logAppend: true
        security:
            authorization: enabled
        storage:
            dbPath: /root/mongo/data
            directoryPerDB: true
        net:
            port: 27017
            unixDomainSocket:
                enabled: false
        processManagement:
            fork: true
            pidFilePath: /root/mongo/mongod.pid
        ```

        **说明：** 云数据库MongoDB默认使用的是WiredTiger存储引擎，并且开启了directoryPerDB选项，因此配置中指定了这个选项。

    -   RocksDB存储引擎

        ```
        systemLog:
            destination: file
            path: /root/mongo/logs/mongod.log
            logAppend: true
        security:
            authorization: enabled​
        storage:
            dbPath: /root/mongo/data
                engine: rocksdb
        net:
            port: 27017
            unixDomainSocket:
                enabled: false
        processManagement:
            fork: true
            pidFilePath: /root/mongo/logs/mongod.pid
        ```

3.  指定新建的配置文件mongod.conf来启动 MongoDB。

    ```
    mongod -f /root/mongo/mongod.conf
    ```

4.  等待启动完成后，可通过服务器的mongo shell登录MongoDB数据库。

    ```
    mongo --host 127.0.0.1 -u <username> -p <password> --authenticationDatabase admin
    ```

    说明：

    -   <username\>：该MongoDB实例的数据库账号，默认为root。
    -   <password\>：该数据库账号对应的密码。

## 副本集模式启动MongoDB数据库

云数据库MongoDB的物理备份默认带有原实例的副本集配置。启动时需以单节点模式启动，否则可能无法访问。

如需以副本集模式启动，需要先[以单节点模式恢复MongoDB数据](#section_pwz_yxp_5fb)，再按照以下步骤执行：

1.  通过服务器的mongo shell登录MongoDB数据库。
2.  移除原有副本集配置。

    ```
    use local
    db.system.replset.remove({})
    ```

3.  关闭MongoDB服务。

    ```
    use admin
    db.shutdownServer()                   
    ```

4.  修改/root/mongo/目录下的配置文件mongod.conf，添加replication相关配置。详细命令用法请参见MongoDB官方文档[部署副本集](https://docs.mongodb.com/manual/tutorial/deploy-replica-set/index.html)。
5.  指定新建的配置文件mongod.conf来启动 MongoDB。

    ```
    mongod -f /root/mongo/mongod.conf
    ```

6.  将成员加入副本集并初始化副本集。

    **说明：** 此步骤使用`rs.initiate()`命令进行操作，详细命令用法请参见MongoDB官方文档[rs.initiate\(\)命令介绍](https://docs.mongodb.com/manual/reference/method/rs.initiate/)。


## 常见问题

Q：为什么我使用指定的`mongod.conf`配置文件启动自建数据库报错？

A：您可能在指定`mongod.conf`配置文件之前已经启动过一次数据库，导致data目录下自动生成了`storage.bson`文件。只需要移走这个文件并重新指定`mongod.conf`配置文件启动数据库即可。

