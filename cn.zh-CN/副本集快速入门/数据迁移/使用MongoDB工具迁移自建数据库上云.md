# 使用MongoDB工具迁移自建数据库上云 {#concept_uvj_jgd_5fb .concept}

MongoDB程序自带有 mongodump 和 mongorestore 工具。通过对这两个工具的使用，您可以将自建的MongoDB数据库，迁移至阿里云MongoDB副本集实例。

推荐[使用DTS迁移副本集架构的自建MongoDB数据库上云](cn.zh-CN/副本集快速入门/数据迁移/使用DTS迁移副本集架构的自建MongoDB数据库上云.md#)，可实现不停机迁移上云。

更多数据迁移/同步场景的解决方案，请参见[MongoDB数据迁移/同步方案概览](../../../../cn.zh-CN/用户指南/数据迁移__同步/MongoDB数据迁移__同步方案概览.md#)。

## 注意事项 {#section_rh3_lgd_5fb .section}

-   该操作为全量数据迁移。为避免迁移前后数据不一致，迁移开始前请停止数据库写入。
-   请确保安装的 mongodump 和 mongorestore 软件版本，与自建的MongoDB数据库的版本一致。
-   如果您之前使用 mongodump 命令对数据库进行过备份操作，请将备份在dump文件夹下的文件移动至其他目录。确保默认的dump备份文件夹为空，否则将会覆盖该文件夹下之前备份的文件。
-   请在数据库服务器上执行 mongodump 和 mongorestore 命令，并非在mongo shell环境下执行。

## 备份自建数据库 {#section_czp_sjd_5fb .section}

该操作为全量数据迁移。为避免迁移前后数据不一致，迁移操作开始前请停止自建数据库的相关业务，并停止数据写入。

1.  在自建MongoDB数据库服务器上执行以下命令，备份所有数据库数据。

    ``` {#codeblock_fbm_vbl_n8m}
    mongodump --host <mongodb_host> --port <port>  -u <username>  --authenticationDatabase  <database>
    ```

    说明：

    -   <mongodb\_host\>：mongodb的服务器地址，本机可使用127.0.0.1。
    -   <port\>：数据库服务的端口号，默认为27017。
    -   <username\>：登录自建MongoDB数据库的账号。
    -   <database\>：对登录自建MongoDB数据库的账号和密码，进行认证的鉴权数据库，默认为 admin 。
    示例：

    ``` {#codeblock_kya_lne_low}
    mongodump --host 127.0.0.1 --port 27017 -u root --authenticationDatabase admin
    ```

2.  命令行提示 `Enter password:`时，输入数据库账号对应的密码，数据库开始备份。

等待备份完成，MongoDB数据库数据将备份至当前目录下dump文件夹中。

## 迁移至云数据库MongoDB {#section_nvh_r4d_5fb .section}

1.  获取副本集实例 Primary 节点的公网连接地址，详情请参考[副本集实例连接说明](cn.zh-CN/副本集快速入门/连接实例/副本集实例连接说明.md#)。

    **说明：** 公网连接地址需要手动申请，详情请参考[申请公网连接地址](cn.zh-CN/副本集快速入门/申请公网连接地址.md#)。

2.  在自建数据库服务器上执行以下命令，将数据库数据全部迁移至阿里云MongoDB数据库中。

    ``` {#codeblock_vq6_g4c_imk}
    mongorestore --host <Primary_host>  -u <username> --authenticationDatabase <database> <Backup directory>
    ```

    说明：

    -   <Primary\_host\>：副本集实例中 Primary 节点的连接地址。
    -   <username\>：登录阿里云MongoDB数据库的数据库账号，默认为 root。
    -   <database\>：对登录阿里云MongoDB数据库的账号和密码，进行认证的鉴权数据库，默认为 admin 。
    -   <Backup directory\>：备份文件存储目录，默认为 dump。
    示例：

    ``` {#codeblock_mk7_ynf_5bw}
    mongorestore --host dds-bp**********-pub.mongodb.rds.aliyuncs.com:3717 -u root --authenticationDatabase admin dump
    						
    ```

3.  命令行提示 `Enter password:`时，输入阿里云MongoDB数据库账号对应的密码，数据开始迁移。

    **说明：** 忘记数据库密码，请参考[设置密码](cn.zh-CN/单节点快速入门/设置密码.md#)。


等待数据迁移完成，检查校验数据无误后即可将业务切换至阿里云MongoDB数据库。

