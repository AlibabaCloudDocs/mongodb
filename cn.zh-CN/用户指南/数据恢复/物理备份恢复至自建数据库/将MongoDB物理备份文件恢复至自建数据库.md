# 将MongoDB物理备份文件恢复至自建数据库 {#concept_lf5_qxp_5fb .concept}

您可以通过控制台下载MongoDB实例的的物理备份文件。本文介绍如何将MongoDB物理备份中的数据，恢复至本地自建的MongoDB数据库中。

## 前提条件 {#section_kdp_sxp_5fb .section}

-   实例架构为副本集实例。
-   实例未开启[TDE功能](cn.zh-CN/用户指南/数据安全性/设置透明数据加密TDE.md#)。
-   实例的存储引擎为WiredTiger或RocksDB。

    **说明：** 如果实例的存储引擎为TerarkDB ，请使用[逻辑备份恢复至自建数据库](cn.zh-CN/用户指南/数据恢复/逻辑备份恢复至自建数据库.md#)。

-   实例的存储引擎为RocksDB 时，您需要自行编译安装带有RocksDB存储引擎的MongoDB应用程序。

## 数据库版本对照表 {#section_0k2_6za_e1q .section}

|MongoDB实例的数据库版本|要求自建MongoDB数据库版本|
|:--------------|:---------------|
|3.2版本|3.2或3.4版本|
|3.4版本|3.4版本|
|4.0版本|4.0版本|

## 物理备份文件格式说明 {#section_lcw_2kt_jfj .section}

|物理备份文件格式|文件后缀|说明|
|--------|----|--|
|tar压缩包|.tar.gz|2019年3月26日之前的实例，物理备份文件格式为tar压缩包。|
|xbstream文件包|\_qp.xb|自2019年3月26日后新建的实例，物理备份文件格式为xbstream文件包。|

**说明：** 上述两种格式的文件，对应的解压操作有所不同，详情请参见[下载及解压物理备份文件](#section_lxg_5xp_5fb)。

## 下载及解压物理备份文件 {#section_lxg_5xp_5fb .section}

以下演示所用的服务器为阿里云ECS实例，镜像为Ubuntu 16.04（64位），更多详情请参见[创建ECS实例](https://help.aliyun.com/document_detail/25424.html)。

**说明：** 

-   该服务器已安装对应版本的 MongoDB 服务，安装方法请参见MongoDB官方文档。
-   该服务器将/path/to/mongo/data作为MongoDB物理恢复操作的数据库所在目录（该目录是空的）。

1.  [下载MongoDB物理备份文件](cn.zh-CN/用户指南/数据恢复/物理备份恢复至自建数据库/副本集实例下载物理备份.md#)，您也可以通过`wget`命令下载。
2.  将下载的MongoDB物理备份文件复制至/path/to/mongo/data/目录中。
3.  对物理备份文件执行解压操作。
    -   当下载的物理备份文件后缀为.tar.gz时，例如文件名为hins20190412.tar.gz，请使用下述方法解压。

        ``` {#codeblock_486_tut_g8j}
        cd /path/to/mongo/data/
        tar xzvf hins20190412.tar.gz 
        ```

    -   当下载的物理备份文件后缀为\_qp.xb时，例如文件名为hins20190412\_qp.xb，请使用下述方法解压。
        1.  安装percona-xtrabackup工具。

            ``` {#codeblock_59t_ecw_55f}
            apt-get update
            apt install percona-xtrabackup
            ```

        2.  前往[QuickLZ网站](http://www.quicklz.com/)，下载qpress工具。
        3.  解压并安装qpress工具。

            ``` {#codeblock_3si_bwc_uab}
            tar xvf qpress-11-linux-x64.tar
            chmod 775 qpress
            cp qpress /usr/bin
            ```

        4.  解压物理备份文件，例如数据库备份文件名为hins20190412\_qp.xb。

            ``` {#codeblock_mtu_bu6_9om}
            cd /path/to/mongo/data/
            cat hins20190412_qp.xb | xbstream -x -v
            innobackupex --decompress --remove-original /path/to/mongo/data
            ```


## 以单节点模式恢复MongoDB物理备份的数据 {#section_pwz_yxp_5fb .section}

1.  在/path/to/mongo文件夹中新建配置文件mongod.conf。

    ``` {#codeblock_xo6_6wl_sov}
    touch mongod.conf
    ```

2.  修改mongod.conf配置文件，使得符合启动的配置要求。

    根据存储引擎选择云数据库MongoDB物理备份启动的配置模板（单节点模式启动并开启认证），您可以复制至mongod.conf文件中。

    -   WiredTiger 存储引擎

        ``` {#codeblock_3f2_8fb_ci7}
        systemLog:
            destination: file
            path: /path/to/mongo/mongod.log
            logAppend: true
        security:
            authorization: enabled
        storage:
            dbPath: /path/to/mongo/data
            directoryPerDB: true
        net:
            http:
                enabled: false
            port: 27017
            unixDomainSocket:
                enabled: false
        processManagement:
            fork: true
            pidFilePath: /path/to/mongo/mongod.pid
        ```

        **说明：** 云数据库MongoDB默认使用的是WiredTiger存储引擎，并且开启了**directoryPerDB**选项，因此配置中指定了这个选项。

    -   RocksDB 存储引擎

        ``` {#codeblock_3d2_occ_r1b}
        systemLog:
            destination: file
            path: /path/to/mongo/logs/mongod.log
            logAppend: true
        security:
            authorization: enabled​
        storage:
            dbPath: /path/to/mongo/data
                engine: rocksdb
        net:
            http:
                enabled: false
            port: 27017
            unixDomainSocket:
                enabled: false
        processManagement:
            fork: true
            pidFilePath: /path/to/mongo/logs/mongod.pid
        ```

3.  指定新建的配置文件 mongod.conf 来启动 MongoDB。

    ``` {#codeblock_blt_9vy_8zt}
    /usr/bin/mongod -f /path/to/mongo/mongod.conf
    ```

4.  等待启动完成后，可通过服务器的 mongo shell 登录 MongoDB 数据库。

    ``` {#codeblock_o0b_sl3_kst}
    mongo --host 127.0.0.1 -u <username> -p <password> --authenticationDatabase admin
    ```

    说明：

    -   <username\>：云数据库MongoDB上该实例的用户名，默认为 root 。
    -   <password\>：云数据库MongoDB上该实例设置的密码。

## 副本集模式启动MongoDB数据库 {#section_c4j_fcs_5fb .section}

云数据库MongoDB的物理备份默认带有原实例的副本集配置。启动时需以单节点模式启动，否则可能无法访问。

如需以副本集模式启动，需要先[以单节点模式恢复MongoDB数据](#section_pwz_yxp_5fb)，再按照以下步骤执行：

1.  通过服务器的mongo shell登录MongoDB数据库。
2.  移除原有副本集配置。

    ``` {#codeblock_wq1_8ah_3nu}
    use local
    db.system.replset.remove({})
    ```

3.  关闭mongodb进程服务。

    ``` {#codeblock_6ts_5w8_pjl}
    use admin
    db.shutdownServer()                   
    ```

4.  修改/path/to/mongo/目录下的配置文件mongod.conf，添加replication相关配置。详细命令用法请参见MongoDB官方文档[部署副本集](https://docs.mongodb.com/manual/tutorial/deploy-replica-set/index.html)。
5.  指定新建的配置文件 mongod.conf 来启动 MongoDB。

    ``` {#codeblock_nef_p78_vz7}
    /usr/bin/mongod -f /path/to/mongo/mongod.conf
    ```

6.  将成员加入副本集并初始化副本集。

    **说明：** 此步骤使用`rs.initiate()`命令进行操作，详细命令用法请参见MongoDB官方文档[rs.initiate\(\)命令介绍](https://docs.mongodb.com/manual/reference/method/rs.initiate/)。


