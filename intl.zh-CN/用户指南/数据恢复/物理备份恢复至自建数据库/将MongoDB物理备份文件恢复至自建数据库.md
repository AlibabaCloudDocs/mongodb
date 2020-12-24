---
keyword: [备份恢复, 数据库恢复]
---

# 将MongoDB物理备份文件恢复至自建数据库

您可以通过控制台下载MongoDB实例的物理备份文件。本文介绍如何将MongoDB物理备份中的数据，恢复至本地自建的MongoDB数据库中。

## 前提条件

-   实例类型为副本集。
-   实例未开启[TDE功能](/intl.zh-CN/用户指南/数据安全性/设置透明数据加密TDE.md)。
-   实例的存储引擎为WiredTiger或RocksDB。如果实例的存储引擎为TerarkDB ，请使用[逻辑备份恢复至自建数据库](/intl.zh-CN/用户指南/数据恢复/逻辑备份恢复至自建数据库.md)。

    **说明：**

    -   您可以在控制台的**基本信息**页面中查看实例的存储引擎。
    -   实例的存储引擎为RocksDB时，您需要自行编译安装带有RocksDB存储引擎的MongoDB应用程序。

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
|xbstream文件包|\_qp.xb|2019年3月26日及之后创建的实例，物理备份文件格式为xbstream文件包。**说明：** 由于Windows暂未支持解压此文件所需的percona-xtrabackup工具，因此xbstream文件包仅限Linux系统中解压使用。 |

**说明：** 上述两种格式的文件，对应的解压操作有所不同，详情请参见[步骤一：下载及解压物理备份文件](#section_lxg_5xp_5fb)。

## 演示环境说明

以下演示所用的服务器为阿里云ECS实例，镜像为Ubuntu 16.04（64位），更多详情请参见[创建ECS实例](~~25424~~)。

**说明：**

-   该服务器已安装对应版本的MongoDB，安装方法请参见[MongoDB官方文档](https://docs.mongodb.com/guides/server/install/)。
-   该服务器已对MongoDB[配置环境变量](#section_qbj_vae_xyv)，执行命令时无需再输入可执行文件的路径。
-   该服务器将/root/mongo/data作为MongoDB物理恢复操作的数据库所在目录（该目录是空的）。

## 配置环境变量

对自建库环境中的MongoDB配置环境变量，避免执行命令时繁琐的路径输入步骤。在执行此步骤前，请确认您已[安装MongoDB](https://docs.mongodb.com/guides/server/install/)。

1.  执行如下命令打开Linux系统的`profile`环境变量文件。

    ```
    vi /etc/profile
    ```

2.  键盘输入`i`进入编辑模式，在最后一行输入如下格式的内容：

    ```
    export PATH=$PATH:/<MongoDB服务端路径>/bin
    ```

    示例：

    ![配置环境变量](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8717728061/p201717.png)

    **说明：** 本示例中，MongoDB服务端的路径为/root/mongo/bin，请根据您的实际情况配置路径。

3.  按Esc键退出编辑模式，键盘输入`:wq`保存并退出。
4.  执行如下命令使新更改的环境变量文件生效：

    ```
    source /etc/profile
    ```


## 步骤一：下载及解压物理备份文件

1.  [下载MongoDB物理备份文件](/intl.zh-CN/用户指南/数据恢复/物理备份恢复至自建数据库/副本集实例下载物理备份.md)，您可以通过如下命令进行下载。

    ```
    wget -c '<数据备份文件外网下载地址>' -O <自定义文件名>.<后缀>
    ```

    **说明：** 请根据下载文件的类型，确保文件后缀名为`.tar.gz`或`_qp.xb`。

2.  执行`mkdir -p /root/mongo/data`命令在/root/mongo/中新建一个`data`目录，并执行如下命令将下载的MongoDB物理备份文件移动到/root/mongo/data/目录中。

    ```
    mv <物理备份文件名.后缀> /root/mongo/data
    ```

3.  对物理备份文件执行解压操作。
    -   当下载的物理备份文件后缀为.tar.gz时，例如文件名为hins20190412.tar.gz时，请使用下述方法解压。

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


## 步骤二：以单节点模式恢复MongoDB物理备份的数据

1.  在/root/mongo文件夹中新建配置文件mongod.conf。

    ```
    touch /root/mongo/mongod.conf
    ```

2.  在命令行中输入`vi /root/mongo/mongod.conf`打开mongod.conf文件，键盘输入`i`开启编辑模式。

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
            pidFilePath: /root/mongo/mongod.pid
        ```

3.  按Esc键退出编辑模式，键盘输入`:wq`保存并退出。
4.  指定新建的配置文件mongod.conf来启动MongoDB。

    ```
    mongod -f /root/mongo/mongod.conf
    ```

5.  等待启动完成后，执行如下命令登录MongoDB数据库，进入Mongo Shell。

    ```
    mongo --host 127.0.0.1 -u <username> -p <password> --authenticationDatabase admin
    ```

    说明：

    -   <username\>：该MongoDB实例的数据库账号，默认为root。
    -   <password\>：该数据库账号对应的密码。
6.  在Mongo Shell中，执行`show dbs`查询当前本地MongoDB中所有的数据库，以验证是否恢复成功。
7.  至此恢复工作已成功完成，您可以在Mongo Shell中执行`exit`命令退出Mongo Shell。

## 步骤三：副本集模式启动MongoDB数据库

云数据库MongoDB的物理备份默认带有原实例的副本集配置。启动时需以单节点模式启动，否则可能无法访问。

如需以副本集模式启动，需要先[以单节点模式恢复MongoDB数据](#section_pwz_yxp_5fb)，再按照以下步骤执行：

1.  在命令行中通过服务器的Mongo Shell使用root用户登录MongoDB数据库。

    ```
    mongo --host 127.0.0.1 -u root -p <root用户密码> --authenticationDatabase admin
    ```

2.  登录完成后，执行如下命令在admin库中创建一个临时用户，赋予该用户临时的local库读写权限，并移除local库中原有副本集配置。

    ```
    use admin
    db.runCommand({
        createRole: "tmprole",
        roles: [
            {
                role: "root",
                db: "admin"
            }
        ],
        privileges: [
            {
                resource: {
                    db: 'local',
                    collection: 'system.replset'
                },
                actions: [
                    'remove'
                ]
            }
        ]
    })
    db.runCommand({
        createUser: "tmpuser",
        pwd: "tmppwd",
        roles: [
            'tmprole'
        ]
    })
    db.auth('tmpuser','tmppwd')
    use local
    db.system.replset.remove({})
    ```

    **说明：** 对于local库的`system.replset`集合，root用户只有只读权限，且由于root用户无法更改自身的权限，因此只能通过其他用户进行删除。

3.  执行如下命令关闭MongoDB服务并退出Mongo Shell。

    ```
    use admin
    db.shutdownServer()
    exit
    ```

4.  创建副本集认证文件。

    如需以副本集模式启动MongoDB，您需要创建一个key文件作为每个副本集节点之间的认证文件。

    1.  执行`mkdir -p /root/mongo/keyFile`命令在mongo目录下创建keyFile文件夹作为认证文件的目录，然后执行如下命令在该目录中创建一个key文件。

        ```
        touch /root/mongo/keyFile/mongodb.key
        ```

    2.  执行`vi /root/mongo/keyFile/mongodb.key`打开mongodb.key文件，按键盘上的`i`进入编辑模式，输入任意内容作为加密内容。例如：

        ```
        MongoDB Encrypting File
        ```

    3.  按Esc键退出编辑模式，输入`:wq`保存并退出文件。
    4.  在命令行中执行`sudo chmod 600 /root/mongo/keyFile/mongodb.key`将认证文件的权限修改为`600`，否则在启动mongod进程的过程中会报错。
    **说明：** 此认证文件将应用于所有副本集节点。

5.  通过下列步骤为副本集准备两个空的节点。
    1.  分别执行如下两个命令复制两份mongod.conf文件作为另外两个节点的启动配置文件。

        ```
        cp /root/mongo/mongod.conf /root/mongo/mongod1.conf
        cp /root/mongo/mongod.conf /root/mongo/mongod2.conf
        ```

    2.  分别执行如下两个命令为另外两个节点创建数据目录。

        ```
        mkdir -p /root/mongo/data1
        mkdir -p /root/mongo/data2
        ```

6.  分别通过下列指示修改各节点的配置文件。

    -   执行`vi /root/mongo/mongod.conf`打开节点1的配置文件，并按照如下内容修改完成后保存退出。

        ```
        systemLog:
            destination: file
            path: /root/mongo/mongod.log
            logAppend: true
        security:
            authorization: enabled
            keyFile: /root/mongo/keyFile/mongodb.key
        storage:
            dbPath: /root/mongo/data
            directoryPerDB: true
        net:
            bindIp: 127.0.0.1
            port: 27017
            unixDomainSocket:
                enabled: false
        processManagement:
            fork: true
            pidFilePath: /root/mongo/mongod.pid
        replication:
            replSetName: "rs0"
        ```

    -   执行`vi /root/mongo/mongod1.conf`打开节点2的配置文件，并按照如下内容修改完成后保存退出。

        ```
        systemLog:
            destination: file
            path: /root/mongo/mongod1.log
            logAppend: true
        security:
            authorization: enabled
            keyFile: /root/mongo/keyFile/mongodb.key
        storage:
            dbPath: /root/mongo/data1
            directoryPerDB: true
        net:
            bindIp: 127.0.0.1
            port: 27018
            unixDomainSocket:
                enabled: false
        processManagement:
            fork: true
            pidFilePath: /root/mongo/mongod1.pid
        replication:
            replSetName: "rs0"
        ```

    -   执行`vi /root/mongo/mongod2.conf`打开节点3的配置文件，并按照如下内容修改完成后保存退出。

        ```
        systemLog:
            destination: file
            path: /root/mongo/mongod2.log
            logAppend: true
        security:
            authorization: enabled
            keyFile: /root/mongo/keyFile/mongodb.key
        storage:
            dbPath: /root/mongo/data2
            directoryPerDB: true
        net:
            bindIp: 127.0.0.1
            port: 27019
            unixDomainSocket:
                enabled: false
        processManagement:
            fork: true
            pidFilePath: /root/mongo/mongod2.pid
        replication:
            replSetName: "rs0"
        ```

    **说明：** 各重要参数说明如下：

    -   systemLog.path：当前节点的MongoDB日志文件路径，
    -   dbpath：当前节点的MongoDB数据文件路径。
    -   pidFilePath：当前节点的MongoDB的PID文件（记录进程ID的文件）路径。
    -   keyFile：副本集认证文件路径，所有节点必须使用同一个认证文件。
    -   bindIp：当前节点的IP地址。如果是在同一台服务器上部署副本集，所有节点可采用相同的IP地址。
    -   port：当前节点的端口号。如果是在同一台服务器上部署副本集，所有节点应采用不同的端口号。
    -   replication：副本集配置。
    -   replSetName：设置副本集的名称。
7.  分别执行如下3个命令启动3个节点。

    ```
    mongod -f /root/mongo/mongod.conf
    mongod -f /root/mongo/mongod1.conf
    mongod -f /root/mongo/mongod2.conf
    ```

8.  等待启动完成后，使用root账号登录MongoDB数据库。

    ```
    mongo -u root -p <root账号的密码> --authenticationDatabase admin
    ```

9.  在Mongo Shell中通过如下命令将上述步骤中创建的副本集成员节点加入副本集并初始化。

    ```
    rs.initiate( {
       _id : "rs0",
       version : 1,
       members: [
          { _id: 0, host: "127.0.0.1:27017" , priority : 1},
          { _id: 1, host: "127.0.0.1:27018" , priority : 0},
          { _id: 2, host: "127.0.0.1:27019" , priority : 0}
       ]
    })
    ```

    **说明：** 此步骤使用`rs.initiate()`命令进行操作，详细命令用法请参见MongoDB官方文档[rs.initiate\(\)命令介绍](https://docs.mongodb.com/manual/reference/method/rs.initiate/)。

    执行成功后，新加入的两个节点将会与主节点进行数据同步，注意此过程的耗时根据备份文件的大小会有较大差异。等待数据同步完成后，副本集模式启动完成。

10. 通过如下步骤验证是否启动成功。
    1.  执行`exit`退出Mongo Shell。
    2.  执行如下命令重新登录MongoDB数据库。

        ```
        mongo -u <username> -p <password> --authenticationDatabase admin
        ```

        说明：

        -   <username\>：该MongoDB实例的数据库账号，默认为root。
        -   <password\>：该数据库账号对应的密码。
    3.  观察Mongo Shell命令行左侧，各情况说明如下：
        -   显示`<副本集名称>:PRIMARY>`：副本集模式启动成功。
        -   显示`<副本集名称>:RECOVERYING>`：正在进行节点之间的数据同步操作，需要等待同步完成。

## 常见问题

Q：为什么我使用指定的`mongod.conf`配置文件启动自建数据库报错？

-   您可能在指定`mongod.conf`配置文件之前已经启动过一次数据库，导致data目录下自动生成了`storage.bson`文件。只需要移走这个文件并重新指定`mongod.conf`配置文件启动数据库即可。
-   当前系统中可能已经有正在执行中的mongod进程，您可以通过`ps -e | grep mongod`命令查询到mongod的进程ID，并通过`kill <进程ID>`命令关闭mongod进程并重新指定`mongod.conf`配置文件启动数据库即可。

