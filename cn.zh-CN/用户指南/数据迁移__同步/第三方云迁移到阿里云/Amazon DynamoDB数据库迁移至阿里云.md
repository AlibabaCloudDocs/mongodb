# Amazon DynamoDB数据库迁移至阿里云 {#concept_186795 .concept}

使用MongoDB数据库自带的数据导入工具mongoimport，您可以将Amazon DynamoDB数据库迁移至阿里云MongoDB数据库。

## 前提条件 {#section_pnm_tgw_mhb .section}

已经创建阿里云MongoDB实例，详情请参考[创建副本集实例](../../../../cn.zh-CN/副本集快速入门/创建副本集实例.md#)或[创建分片集群实例](../../../../cn.zh-CN/分片集群快速入门/创建分片集群实例.md#)。

## 注意事项 {#section_xj3_k3w_mhb .section}

-   该操作为全量数据迁移，暂不支持增量数据迁移。为避免迁移前后数据不一致，在迁移开始前请停止数据库写入。
-   请在安装有MongoDB服务的服务器上执行mongoimport命令，并非在mongo shell环境下执行。

## 术语/概念对应关系 {#section_ywn_0y5_3jb .section}

|DynamoDB中的术语/概念|MongoDB中的术语/概念|
|:--------------|:-------------|
|Table|Collection|
|Item|Document|
|Attribute|Field|

## 环境准备 {#section_u4c_ygw_mhb .section}

在本地设备上安装MongoDB程序，程序版本与阿里云MongoDB数据库的版本一致。该设备将作为数据迁移的中转。本案例将MongoDB程序安装在Ubuntu Linux上进行演示。

1.  在本地设备上安装MongoDB程序，详情请参考[安装MongoDB](https://docs.mongodb.com/manual/administration/install-community/)。

    **说明：** 该设备仅作为数据备份与恢复的临时中转平台，迁移操作完成后不再需要。

2.  将本地设备的公网IP地址，加入至阿里云MongoDB实例的白名单中，详情请参考[设置白名单](cn.zh-CN/用户指南/数据安全性/设置白名单.md#)。

## 迁移操作步骤 {#section_p2d_rzv_mhb .section}

1.  登录DynamoDB控制台。
2.  在左侧导航栏，单击**表**。
3.  选择需要迁移的表，本案例选择**customer**表。

    ![选择DynamoDB表](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/161016/156879129345065_zh-CN.png)

4.  选择需要迁移的数据，导出为**.csv**格式。

    ![选择DynamoDB待迁移数据](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/161016/156879129345066_zh-CN.png)

    1.  单击项目页签。
    2.  选择需要迁移的数据。
    3.  单击**操作** \> **导出到.csv**。
5.  将导出的.csv文件复制至[环境准备](#section_u4c_ygw_mhb)中的本地设备。
6.  登录[阿里云MongoDB控制台](https://mongodb.console.aliyun.com/)，获取阿里云MongoDB实例的公网连接地址。

    -   如要迁移至阿里云MongoDB副本集实例，请获取Primary节点公网连接地址，详情请参考[副本集实例连接说明](../../../../cn.zh-CN/副本集快速入门/连接实例/副本集实例连接说明.md#)。
    -   如要迁移至阿里云MongoDB分片集群实例，请获取任一Mongos节点的公网连接地址，详情请参考[分片集群实例连接说明](../../../../cn.zh-CN/分片集群快速入门/连接实例/分片集群实例连接说明.md#)。
    **说明：** 公网连接地址需要手动申请，详情请参考[申请公网连接地址](cn.zh-CN/用户指南/管理网络连接/申请公网连接地址.md#)。

7.  在本地设备上，执行以下命令将数据库数据导入至阿里云MongoDB数据库。

    ``` {#codeblock_miy_rxp_uon}
    mongoimport --host <mongodb_host:port> --authenticationDatabase admin -u <username> --db <database> --collection <collection> --file <filename>  --type csv --headerline                    
    ```

    **说明：** 

    -   <mongodb\_host:port\>：阿里云MongoDB副本集实例的Primary节点或分片集群实例的Mongos节点连接地址。
    -   <username\>：阿里云MongoDB实例的数据库用户名，默认为root。该用户需具备目标数据库的readWrite权限。
    -   <database\>：指定要导入数据的数据库名。
    -   <collection\>：指定要导入数据的集合名。
    -   <filename\> ：.csv文件的路径和名称。
    示例：将customer.csv中的数据导入至mongodbtest数据库的customer集合中。

    ``` {#codeblock_5fi_z5z_m4c}
    mongoimport --host dds-bpxxxxxxxx-pub.mongodb.rds.aliyuncs.com:3717 --authenticationDatabase admin -u root --db mongodbtest --collection customer --file ~/download/customer.csv  --type csv --headerline
    ```

8.  命令行提示 `Enter password:`时，输入阿里云MongoDB数据库账号对应的密码，数据开始导入。

    **说明：** 如过还有表需要迁移，请重复步骤3到步骤8。


等待数据导入完成，即完成Amazon DynamoDB数据迁移至阿里云的操作。

## 后续操作 {#section_el1_3ta_198 .section}

为提升数据操作的性能，数据导入后您还需要根据业务需求建立索引，详情请参考[db.collection.createIndex](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/index.html)。

