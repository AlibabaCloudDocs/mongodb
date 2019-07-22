# 使用MongoDB工具将腾讯云MongoDB迁移至阿里云 {#concept_srk_yky_ggb .concept}

使用MongoDB数据库自带的备份还原工具mongodump和mongorestore，您可以将3.2版本的腾讯云MongoDB副本集实例全量迁移至阿里云。

## 背景信息 {#section_vst_zqz_ngb .section}

当您因业务调整或需要使用阿里云MongoDB特性功能时，您可以使用MongoDB自带的备份还原工具（ mongodump 和 mongorestore），通过**全量数据迁移**方法，将腾讯云MongoDB数据库迁移至阿里云MongoDB数据库。

## 前提条件 {#section_p1c_1rz_ngb .section}

-   mongodump和mongorestore的软件版本，与腾讯云MongoDB数据库的版本一致。
-   已创建阿里云MongoDB实例。如果尚未创建，请参见[创建副本集实例](../../../../cn.zh-CN/副本集快速入门/创建副本集实例.md#)或[创建分片集群实例](../../../../cn.zh-CN/分片集群快速入门/创建分片集群实例.md#)。

    **说明：** 阿里云MongoDB实例的存储空间应大于腾讯云MongoDB副本集实例已使用的存储空间。如果创建的阿里云MongoDB实例存储空间过低，您需要升级存储空间，详情请参见[变更配置](cn.zh-CN/用户指南/实例管理/变更配置.md#)。

-   如需迁移至阿里云MongoDB分片集群实例，建议对数据进行分片以更好地发挥性能，详情请参见[设置数据分片](../../../../cn.zh-CN/最佳实践/设置数据分片以充分利用Shard性能.md#)。

## 注意事项 {#section_bpr_ufb_cmn .section}

-   该操作为全量迁移，迁移开始前需要停止腾讯云MongoDB数据库的相关业务，同时为了保障数据一致性，全量数据迁移期间请勿在腾讯云MongoDB数据库中写入新的数据。
-   为避免影响您的业务使用，请在业务低峰期进行数据迁移操作。
-   如果您之前使用mongodump命令对数据库进行过备份操作，请将备份在dump文件夹下的文件移动至其他目录。确保dump文件夹为空，否则执行备份的操作会覆盖该文件夹下的原有备份文件。
-   阿里云MongoDB实例支持的版本与存储引擎请参见[版本及存储引擎](../../../../cn.zh-CN/产品简介/版本及存储引擎.md#)，如需跨版本或跨引擎迁移，请提前确认兼容性。

## 数据库账号权限要求 {#section_oyv_j2l_5fb .section}

|迁移对象|权限要求|
|:---|:---|
|腾讯云MongoDB实例|待迁移库的read权限|
|阿里云MongoDB实例|目标库的readWrite权限|

## 操作步骤 {#section_nf4_mby_ggb .section}

由于腾讯云MongoDB实例只有内网连接地址，没有公网连接地址。此时需要创建一个具有公网地址的腾讯云服务器用作端口数据转发，以完成数据库的迁移操作。迁移操作完成后如不再需要，可释放腾讯云服务器。

1.  创建腾讯云服务器。本案例中创建的腾讯云服务器使用的是Linux操作系统。

    **说明：** 为保障腾讯云服务器和腾讯云MongoDB副本集实例的正常通信，腾讯云服务器的地域、可用区、私有网络和子网需配置与腾讯云MongoDB副本集实例一致。

2.  登录腾讯云服务器，安装MongoDB程序，详情请参见[安装MongoDB](https://docs.mongodb.com/manual/administration/install-community/)。

    **说明：** 请确保安装的MongoDB程序的软件版本与腾讯云MongoDB数据库的版本一致。

3.  返回腾讯云服务器控制台，在左侧导航栏，单击**安全组**。
4.  在入站规则页签，单击**添加规则**，放通MongoDB数据库端口27017，允许外网访问该端口。

    ![安全组配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84333/156376527535723_zh-CN.png)

5.  进入腾讯云MongoDB控制台，单击目标MongoDB实例名。
6.  单击安全组页签，并单击**配置安全组**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/519067/156376527649246_zh-CN.png)

7.  在弹出的配置安全组对话框，选择已放通27017端口的安全组，并单击**确定**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/519067/156376527649247_zh-CN.png)

8.  进入腾讯云MongoDB控制台，获取腾讯云MongoDB实例的内网IP地址。

    ![查看MongoDB实例的内网IP地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84333/156376527635670_zh-CN.png)

9.  登录腾讯云服务器，并执行以下命令进行数据备份，将数据备份至该服务器上。

    ``` {#codeblock_7fy_upg_dq7}
    mongodump --host <host>:27017 -u <username> --authenticationDatabase admin
    ```

    **说明：** 

    -   <host\>：腾讯云MongoDB实例的内网IP地址。
    -   <username\>：连接腾讯云MongoDB数据库的账号，默认为mongouser。
    示例：

    ``` {#codeblock_aqe_cmf_9yj}
    mongodump --host 10.10.0.7:27017 -u mongouser --authenticationDatabase admin
    ```

10. 命令行提示`Enter password:`时，输入数据库账号对应的密码，数据库开始备份。

    **说明：** 等待备份完成，数据将备份至当前目录下dump文件夹中。

11. 在腾讯云控制台，获取腾讯云服务器的公网IP地址。

    ![查看云服务器的公网IP地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84380/156376527649350_zh-CN.png)

12. 登录[阿里云MongoDB控制台](https://mongodb.console.aliyun.com)，将腾讯云服务器的公网IP地址加入到阿里云MongoDB实例的白名单中。详情请参见[设置白名单](cn.zh-CN/用户指南/数据安全性/设置白名单.md#)。
13. 获取阿里云MongoDB实例的公网连接地址。

    -   如需迁移至阿里云MongoDB副本集实例，请获取Primary节点公网连接地址，详情请参见[副本集实例连接说明](../../../../cn.zh-CN/副本集快速入门/连接实例/副本集实例连接说明.md#)。
    -   如需迁移至阿里云MongoDB分片集群实例，请获取任一Mongos节点的公网连接地址，详情请参见[分片集群实例连接说明](../../../../cn.zh-CN/分片集群快速入门/连接实例/分片集群实例连接说明.md#)。
    **说明：** 公网连接地址需要手动申请，详情请参见[申请公网连接地址](cn.zh-CN/用户指南/管理网络连接/申请公网连接地址.md#)。

14. 在腾讯云服务器上执行以下命令将数据导入至阿里云MongoDB数据库。

    ``` {#codeblock_b6y_r0c_y7d}
    mongorestore --host <mongodb_host>:3717 -u <username> -d <database>  <dir> --authenticationDatabase admin
    ```

    **说明：** 

    -   <mongodb\_host\>：阿里云MongoDB实例的公网连接地址。（不包含端口号）
    -   <username\>：连接阿里云MongoDB实例的数据库账号。
    -   <database\>：需要导入的数据库。备份文件中如有多个数据库，需要重复本步骤进行其它数据库的导入。
    -   <dir\>：数据库备份文件所在的目录。
    示例：

    -   导入数据库备份文件中的mongodbtest数据库

        ``` {#codeblock_ga8_o29_vpg}
        mongorestore --host dds-bpxxxxxxxxxx-pub.mongodb.rds.aliyuncs.com:3717 -u root --authenticationDatabase admin -d mongodbtest /dump/mongodbtest 
        ```

    -   导入数据库备份文件中的test123数据库

        ``` {#codeblock_729_6sc_r4z}
        mongorestore --host dds-bpxxxxxxxxxx-pub.mongodb.rds.aliyuncs.com:3717  -u root -authenticationDatabase admin -d test123 /dump/test123
        ```

15. 命令行提示`Enter password:`时，输入数据库账号对应的密码，数据库开始导入。

    **说明：** 等待备份完成，数据将导入至阿里云MongoDB数据库中。

16. 根据业务需求选择合适的时间，将业务切换至阿里云MongoDB实例中。

## 如何连接阿里云MongoDB数据库 {#section_2gv_zab_ct1 .section}

-   [副本集实例连接说明](../../../../cn.zh-CN/副本集快速入门/连接实例/副本集实例连接说明.md#)
-   [分片集群实例连接说明](../../../../cn.zh-CN/分片集群快速入门/连接实例/分片集群实例连接说明.md#)

