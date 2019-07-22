# Atlas MongoDB数据库迁移至阿里云 {#concept_phx_ws5_jgb .concept}

使用MongoDB数据库自带的备份还原工具 mongodump 和 mongorestore，您可以将Atlas MongoDB数据库迁移至阿里云MongoDB数据库。

## 注意事项 {#section_j3k_5sk_5fb .section}

-   MongoDB实例支持的版本与存储引擎请参见[版本及存储引擎](../../../../cn.zh-CN/产品简介/版本及存储引擎.md#)，如需跨版本或跨引擎迁移，请提前确认兼容性。
-   该操作为全量数据迁移，暂不支持[增量数据迁移](https://help.aliyun.com/knowledge_detail/39252.html)。为避免迁移前后数据不一致，迁移开始前请停止数据库写入。
-   请确保安装的 mongodump 和 mongorestore 软件版本，与Atlas MongoDB的数据库版本一致。
-   如果您之前使用 mongodump 命令对数据库进行过备份操作，请将备份在dump文件夹下的文件移动至其他目录。确保默认的dump备份文件夹为空，否则将会覆盖该文件夹下之前备份的文件。
-   请在安装有MongoDB服务的服务器上执行 mongodump 和 mongorestore 命令，并非在mongo shell环境下执行。

## 数据库账号权限要求 {#section_oyv_j2l_5fb .section}

|迁移数据源|账号权限|
|:----|:---|
|Atlas MongoDB实例|待迁移库的read权限|
|阿里云MongoDB实例|目标库的readWrite权限|

## 迁移前准备工作一 {#section_y4p_ztk_5fb .section}

1.  创建阿里云MongoDB实例，详情请参考[创建副本集实例](../../../../cn.zh-CN/副本集快速入门/创建副本集实例.md#)或[创建分片集群实例](../../../../cn.zh-CN/分片集群快速入门/创建分片集群实例.md#)。

    **说明：** 

    -   阿里云MongoDB实例的存储空间要大于Atlas MongoDB的存储空间。
    -   如需迁移至阿里云MongoDB分片集群实例，建议对数据进行分片，详情请参考[设置数据分片](../../../../cn.zh-CN/最佳实践/设置数据分片以充分利用Shard性能.md#)。
2.  设置阿里云MongoDB数据库的数据库密码，详情请参考[设置密码](https://help.aliyun.com/document_detail/54956.html#task-xxj-svb-kfb)。

## 迁移前准备工作二 {#section_thc_nt5_jgb .section}

在本地设备上，安装MongoDB程序，程序版本与Atlas MongoDB数据库的版本一致。该服务器作将为数据迁移的中转。本案例将MongoDB服务安装在Linux服务器上进行演示。

1.  在本地设备上安装MongoDB程序，详情请参考[安装MongoDB](https://docs.mongodb.com/manual/administration/install-community/)。

    **说明：** 

    -   该设备仅作为数据备份与恢复的临时中转平台，迁移操作完成后不再需要。
    -   备份目录所在分区的可用磁盘空间要大于Atlas MongoDB数据库的存储空间。
2.  将本地设备的公网IP地址，加入至阿里云MongoDB实例的白名单中，详情请参考[设置白名单](http://1)。

## 数据迁移操作步骤 {#section_nf4_mby_ggb .section}

1.  登录Atlas MongoDB数据库控制台。
2.  将用于数据迁移的本地设备的公网IP地址，加入至Atlas MongoDB实例的白名单中。

    ![Atlas MongoDB白名单配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/91579/156376518636508_zh-CN.png)

3.  在Clusters页面，单击 Clusters 的名称。

    ![Clusters名称](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/91579/156376518636523_zh-CN.png)

4.  在Command Line Tools页签，单击 mongodump 命令后的**COPY**，复制包含Atlas MongoDB数据库连接信息的 mongodump 命令。

    ![复制包含连接信息的mongodump命令](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/91579/156376518636524_zh-CN.png)

5.  在本地设备上，备份Atlas MongoDB数据库。

    1.  在本地设备上，粘贴包含Atlas MongoDB数据库连接信息的 mongodump 命令。
    2.  将<PASSWORD\>替换为root用户的密码，将<DATABASE\>替换为要备份的数据库名称。
    3.  执行该命令，等待数据备份完毕。
    示例：

    ![mongodump操作示例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/91579/156376518636534_zh-CN.png)

6.  登录[阿里云MongoDB控制台](https://mongodb.console.aliyun.com)，获取阿里云MongoDB实例的公网连接地址。

    -   如要迁移至阿里云MongoDB副本集实例，请获取 Primary 节点公网连接地址，详情请参考[副本集实例连接说明](../../../../cn.zh-CN/副本集快速入门/连接实例/副本集实例连接说明.md#)。
    -   如要迁移至阿里云MongoDB分片集群实例，请获取任一 Mongos 节点的公网连接地址，详情请参考[分片集群实例连接说明](../../../../cn.zh-CN/分片集群快速入门/连接实例/分片集群实例连接说明.md#)。
    **说明：** 公网连接地址需要手动申请，详情请参考[申请公网连接地址](cn.zh-CN/用户指南/管理网络连接/申请公网连接地址.md#)。

7.  在本地设备上，执行以下命令将数据库数据导入至阿里云MongoDB数据库。

    ``` {#codeblock_ogz_ixk_ans}
    mongorestore --host <mongodb_host>:3717 --authenticationDatabase admin -u <username> -d <database> <database_backupfile_directory>
    ```

    **说明：** 

    -   <mongodb\_host\>：阿里云MongoDB副本集实例的 Primary 节点或阿里云MongoDB分片集群实例的 Mongos 节点连接地址。
    -   <username\>：阿里云MongoDB实例的数据库用户名。
    -   <database\>：需要恢复的数据库。备份文件中如有多个数据库，需要重复本步骤进行其它数据库的恢复。
    -   <database\_backupfile\_directory\>：数据库备份文件所在的目录。
    示例：

    恢复数据库备份文件中的 mongodbtest 数据库

    ``` {#codeblock_otl_5zy_bjt}
    mongorestore --host dds-bp**********-pub.mongodb.rds.aliyuncs.com:3717 --authenticationDatabase admin -u root -d mongodbtest /dump/mongodbtest
    ```

    恢复数据库备份文件中的 test123 数据库

    ``` {#codeblock_kiu_gr0_ow9}
    mongorestore --host dds-bp**********-pub.mongodb.rds.aliyuncs.com:3717 --authenticationDatabase admin -u root -d test123 /dump/test123
    ```

8.  命令行提示 `Enter password:`时，输入阿里云MongoDB数据库账号对应的密码。

等待数据恢复完成，Atlas MongoDB数据库即迁移至阿里云MongoDB数据库中。

