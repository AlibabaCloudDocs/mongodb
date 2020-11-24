# 使用MongoDB工具迁移自建数据库上云

Mongodump和Mongorestore是MongoDB数据库自带的备份恢复工具。您可以在本地设备或ECS实例中安装MongoDB数据库，然后借助该工具将自建MongoDB数据库迁移至阿里云MongoDB分片集群实例。

## 背景信息

-   建议通过DTS迁移分片集群架构的自建MongoDB数据库上云，可实现不停机迁移上云。详情请参见[使用DTS迁移分片集群架构的自建MongoDB数据库上云](/cn.zh-CN/副本集快速入门/数据迁移/使用DTS迁移分片集群架构的自建MongoDB数据库上云.md)。
-   更多数据迁移或同步场景的解决方案，请参见[MongoDB数据迁移和同步方案概览](/cn.zh-CN/用户指南/数据迁移和同步/MongoDB数据迁移和同步方案概览.md)。

## 前提条件

-   请确保安装的Mongodump和Mongorestore软件版本与自建MongoDB数据库的版本一致。安装步骤请参见官方文档[Install MongoDB](https://docs.mongodb.com/v3.4/installation/)。

    **说明：** 您也可以直接在自建MongoDB数据库所属的服务器上执行Mongodump和Mongorestore命令，无需安装。

-   目标分片集群实例的存储空间应大于自建MongoDB数据库已占用的存储空间。如存储空间不足，您可以升级存储空间，详情请参见[变更配置方案概览](/cn.zh-CN/用户指南/实例管理/变更实例配置/变更配置方案概览.md)。

## 注意事项

-   该操作为全量数据迁移。为保障数据一致性，迁移操作开始前请停止自建数据库的相关业务，并停止数据写入。
-   如果您之前使用Mongodump命令对数据库进行过备份操作，请将dump文件夹中的备份文件移动至其他目录并确保dump文件夹为空，否则执行备份操作将会覆盖该文件夹中的历史备份文件。
-   请在数据库服务器上执行Mongodump和Mongorestore命令，并非在mongo shell环境下执行。

## 步骤一：备份自建数据库

1.  在自建MongoDB数据库所属的服务器中执行以下命令，备份所有数据库的数据。

    ```
    mongodump --host <mongodb_host> --port <port>  -u <username>  --authenticationDatabase  <database>
    ```

    **说明：**

    -   <mongodb\_host\>：自建MongoDB数据库的服务器地址，本机可使用127.0.0.1。
    -   <port\>：数据库服务的端口号，默认为27017。
    -   <username\>：自建MongoDB数据库的数据库账号。
    -   <database\>：鉴权数据库名，即数据库账号所属的数据库。
    示例：

    ```
    mongodump --host 127.0.0.1 --port 27017 -u root --authenticationDatabase admin
    ```

2.  当命令行提示`Enter password:`时，输入数据库账号对应的密码并按回车键确认，即开始执行备份操作。

等待备份完成，自建数据库中的数据即备份至当前目录下的dump文件夹中。

## 步骤二：设置数据分片（可选）

没有设置数据分片的情况下，数据将被集中写入到Primary Shard节点中，导致其他Shard节点的存储空间和计算性能无法被充分利用。如需设置请参见[设置数据分片](/cn.zh-CN/最佳实践/性能/设置数据分片以充分利用Shard性能.md)。

**说明：** 您可以在迁移前，在目标MongoDB实例中建立需要数据分片的数据库和集合，配置数据分片。也可以在迁移后配置数据分片。

## 步骤三：将数据迁移至阿里云

1.  获取任一Mongos节点的公网或内网连接地址，详情请参见[分片集群实例连接说明]()。

    **说明：** 公网连接地址需要手动申请，详情请参见[申请公网连接地址](/cn.zh-CN/分片集群快速入门/申请公网连接地址.md)。

2.  将自建数据库所属服务器的IP地址加入至分片集群实例的白名单中，详情请参见[设置白名单](/cn.zh-CN/分片集群快速入门/设置白名单.md)。

    **说明：**

    -   通过专有网络或经典网络连接分片集群实例时，您需要将自建数据库所属ECS的内网IP地址加入至分片集群实例的白名单中。
    -   通过公网地址连接分片集群实例时，将需要将自建数据库所属本地服务器的公网IP地址加入至分片集群实例的白名单中。
3.  在自建数据库服务器上执行以下语句，将备份的数据全部迁移至分片集群实例。

    ```
    mongorestore --host <Mongos_host>  -u <username> --authenticationDatabase <database> <Backup directory>
    ```

    **说明：**

    -   <Mongos\_host\>：分片集群实例中任一Mongos节点的连接地址。
    -   <username\>：分片集群实例的数据库账号，初始账号为root。
    -   <database\>：鉴权数据库名，即数据库账号所属的数据库。当数据库账号为root时，对应的数据库为admin。
    -   <Backup directory\>：备份文件存储的目录，默认为dump。
    示例：

    ```
    mongorestore --host s-bp**********-pub.mongodb.rds.aliyuncs.com:3717 -u root --authenticationDatabase admin dump
    ```

4.  在命令行提示`Enter password:`时，输入分片集群实例的数据库账号对应的密码并按回车键确认，即开始执行数据迁移操作。

    **说明：**

    -   输入密码时，密码字符是不可见的。
    -   如果忘记了root账号的密码，您可以通过[设置密码](/cn.zh-CN/分片集群快速入门/设置密码.md)的方式来重置密码。

等待数据迁移完成，根据业务需求选择合适的时间，将业务切换至分片集群实例。

