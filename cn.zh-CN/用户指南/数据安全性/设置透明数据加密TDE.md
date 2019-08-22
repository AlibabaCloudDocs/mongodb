# 设置透明数据加密TDE {#task_1796793 .task}

透明数据加密TDE（Transparent Data Encryption）可对数据文件执行实时I/O加密和解密，数据在写入磁盘之前进行加密，从磁盘读入内存时进行解密。TDE不会增加数据文件的大小，您无需更改任何应用程序，即可使用TDE功能。为提高数据安全性，您可以通过控制台启用TDE功能，对实例数据进行加密。

-   实例架构为副本集实例或分片集群实例。
-   实例的存储引擎为WiredTiger。
-   实例的数据库版本为4.0。如果实例数据库版本过低，您可以[升级数据库版本](cn.zh-CN/用户指南/实例管理/升级数据库版本.md#)。

    **说明：** 正式开通TDE前，您可以创建一个4.0版本的按量付费的实例来测试应用与版本兼容性，测试完毕可释放该实例。


如果您的实例不满足实例架构或存储引擎的条件，您可以通过其他方式变更，详情请参见[变更配置方案概览](cn.zh-CN/用户指南/实例管理/变更配置方案概览.md#)。

## 影响 {#section_g8k_xww_twd .section}

-   开通TDE的过程中，实例会重启一次并出现连接闪断，建议您在业务低峰期操作并确保应用有重连机制。
-   开通TDE功能后，会增加实例的CPU使用率。
-   加密后的集合不再支持[通过物理备份恢复至自建数据库](cn.zh-CN/用户指南/数据恢复/物理备份恢复至自建数据库/将MongoDB物理备份文件恢复至自建数据库.md#)。如果您需要将加密后的集合恢复到自建数据库，您可以[通过逻辑备份恢复至自建数据库](cn.zh-CN/用户指南/数据恢复/逻辑备份恢复至自建数据库.md#)。

## 注意事项 {#section_mtu_6ny_osd .section}

-   TDE功能开通后无法关闭。
-   当前TDE的开启粒度为实例，可支持集合粒度的控制。

    **说明：** 如果业务上有特殊需求，您可以在创建集合时，指定该集合不被加密，详情请参见[设置指定的集合不被加密](#section_1ip_yvb_vv4)。

-   TDE功能开启后，仅加密新创建的集合，已有的集合不会被加密。
-   TDE所使用的密钥，由[密钥管理服务KMS](https://help.aliyun.com/document_detail/28935.html)（Key Management Service）统一生成和管理，云数据库MongoDB不提供加密所需的密钥和证书。

## 操作步骤 {#section_e71_rel_z50 .section}

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/#/mongodb/list)。
2.  在左侧导航栏，单击**副本集实例列表**或**分片集群实例列表**。
3.  找到目标实例，单击实例ID。
4.  在左侧导航栏，选择**数据安全性** \> **TDE** 。
5.  单击**TDE状态**右侧的滑块，开启TDE加密。 

    ![TDE加密](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1422772/156643740656526_zh-CN.png)

6.  在弹出的重启实例对话框中，单击**确定**。 实例进入**TDE修改中**状态，当转变为**运行中**状态即代表操作完成。

## 设置指定的集合不被加密 {#section_1ip_yvb_vv4 .section}

开启TDE加密后，所有新创建的集合都会被加密。如果业务上有特殊需求，您可以在创建集合时，指定该集合不被加密。

1.  通过Mongo Shell连接数据库，详情请参见[连接副本集实例](../../../../cn.zh-CN/副本集快速入门/连接实例/通过Mongo Shell登录MongoDB数据库.md#)或[连接分片集群实例](../../../../cn.zh-CN/分片集群快速入门/连接实例/通过 Mongo Shell 登录MongoDB数据库.md#)。
2.  执行下述命令创建集合，指定该集合不被加密。 

    ``` {#codeblock_nhe_u9h_ytg}
    db.createCollection("<collection_name>",{ storageEngine: { wiredTiger: { configString: "encryption=(name=none)" } } })
    ```

    **说明：** <collection\_name\>：集合名。

    示例

    ``` {#codeblock_udx_vty_dlk}
    db.createCollection("customer",{ storageEngine: { wiredTiger: { configString: "encryption=(name=none)" } } })
    ```


