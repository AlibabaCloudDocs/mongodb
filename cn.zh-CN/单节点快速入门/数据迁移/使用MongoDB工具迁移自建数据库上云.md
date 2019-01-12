# 使用MongoDB工具迁移自建数据库上云 {#concept_ztl_f4w_fgb .concept}

MongoDB数据库自带有 Mongodump 和 Mongorestore 工具。通过对这两个工具的使用，您可以将自建MongoDB数据库迁移至阿里云MongoDB单节点实例的数据库中。

## 注意事项 {#section_rh3_lgd_5fb .section}

-   本文操作适用于新购的实例且实例的数据库没有数据的场景。
-   该操作为全量数据迁移。为避免迁移前后数据不一致，迁移开始前请停止数据库写入。
-   请确保安装的 Mongodump 和 Mongorestore 软件版本，与自建的MongoDB数据库的版本一致。
-   如果您之前使用 Mongodump 命令对数据库进行过备份操作，请将备份在 dump 文件夹下的备份文件移动至其他目录。确保 dump 文件夹为空，否则将会覆盖该文件夹下之前备份的文件。
-   请在自建MongoDB数据库服务器上执行 Mongodump 和 Mongorestore命令，并非在 Mongo shell环境下执行。

## 备份自建数据库 {#section_czp_sjd_5fb .section}

该操作为全量数据迁移。为避免迁移前后数据不一致，迁移操作开始前请停止自建数据库的相关业务，并停止数据写入。

1.  在自建MongoDB数据库服务器上执行以下命令，备份所有数据库数据。

    ```
    mongodump --host <mongodb_host> --port <port>  -u <username>  --authenticationDatabase  <database>
    ```

    说明：

    -   <mongodb\_host\>：mongodb的服务器地址，本机可使用127.0.0.1。
    -   <port\>：数据库服务的端口号，默认为27017。
    -   <username\>：登录自建MongoDB数据库的账号。
    -   <database\>：对登录自建MongoDB数据库的账号和密码，进行认证的鉴权数据库，默认为 admin 。
    示例：

    ```
    mongodump --host 127.0.0.1 --port 27017 -u root --authenticationDatabase admin
    ```

2.  命令行提示 `Enter password:`时，输入数据库账号对应的密码，数据库开始备份。

等待备份完成，自建数据库将备份至当前目录下dump文件夹中。

## 迁移至阿里云数据库MongoDB {#section_nvh_r4d_5fb .section}

1.  获取单节点实例 Primary 节点的连接地址。

    1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/#/mongodb/list)。
    2.  选择目标实例所在地域。
    3.  在左侧导航栏，单击**副本集实例列表**。
    4.  单击目标实例ID或者单击实例右侧的**![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6723/154727636313851_zh-CN.png)** \> **管理**。
    5.  在左侧导航栏，单击**数据库连接**，查看数据库连接信息。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/82882/154727636335103_zh-CN.png)

    **说明：** 

    -   内网连接-专有网络：也称为VPC（Virtual Private Cloud）。VPC是一种隔离的网络环境，安全性和性能均高于传统的经典网络。

        适用于自建的MongoDB数据库搭建在[ECS实例](https://help.aliyun.com/document_detail/25367.html)上的场景。需要ECS实例和阿里云MongoDB实例在同一地域，同一VPC网络下。同时需要将ECS的私网IP地址加入到MongoDB实例的白名单中，详情请参见[设置白名单](cn.zh-CN/单节点快速入门/设置白名单.md#)。

    -   公网连接：为保障安全性，公网连接地址默认没有创建，需要您手动申请。详情请参考[申请公网连接地址](cn.zh-CN/单节点快速入门/申请公网连接地址.md#)。

        通过公网连接地址迁移数据库，需要将自建MongoDB数据库所在的公网IP地址加入到阿里云MongoDB实例的白名单。

2.  在自建数据库服务器上执行以下语句将数据库数据全部迁移至阿里云数据库MongoDB。

    ```
    mongorestore --host <Primary_host>  -u <username> --authenticationDatabase <database> <Backup directory>
    ```

    说明：

    -   <Primary\_host\>：副本集实例中 Primary 节点的连接地址。
    -   <username\>：登录阿里云MongoDB数据库的数据库账号，默认为 root。
    -   <database\>：对登录阿里云MongoDB数据库的账号和密码，进行认证的鉴权数据库，默认为 admin 。
    -   <Backup directory\>：备份文件存储目录，默认为 dump。
    示例：

    ```
    mongorestore --host dds-bp**********-pub.mongodb.rds.aliyuncs.com:3717 -u root --authenticationDatabase admin dump
    
    ```

3.  命令行提示 `Enter password:`时，输入阿里云MongoDB数据库账号对应的密码，数据开始迁移。

    **说明：** 忘记数据库密码，请参考[设置密码](cn.zh-CN/单节点快速入门/设置密码.md#)。


等待数据迁移完成，检查校验数据无误后即可将业务切换至阿里云MongoDB数据库。

