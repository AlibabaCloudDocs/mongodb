# 使用Mongo Shell通过SSL加密连接数据库 {#concept_ls5_jks_ngb .concept}

在使用Mongo Shell连接数据库时，您可以启用SSL（Secure Sockets Layer）加密功能提高数据链路的安全性。通过SSL加密功能可以在传输层对网络连接进行加密，在提升通信数据安全性的同时，保障数据的完整性。

## 前提条件 {#section_d41_xks_ngb .section}

-   实例类型为副本集实例，且数据库版本为3.4版本或4.0版本。

    **说明：** 如果版本过低，您可以[升级数据库版本](cn.zh-CN/用户指南/实例管理/升级数据库版本.md#)。

-   实例已开启SSL加密功能，详情请参见[设置SSL加密](cn.zh-CN/用户指南/数据安全性/设置 SSL 加密.md#)。
-   待连接数据库的本地服务器或[ECS](https://help.aliyun.com/document_detail/25367.html)实例上已安装3.0及以上版本的Mongo Shell。安装步骤请参见[Install MongoDB](https://docs.mongodb.com/v3.4/installation/)。
-   待连接数据库的本地服务器或ECS实例的IP地址已加入到MongoDB实例的白名单中，详情请参见[设置白名单](cn.zh-CN/用户指南/数据安全性/设置白名单.md#)。

## 注意事项 {#section_s6r_d14_5u4 .section}

由于SSL加密的固有缺陷，启用SSL加密会显著增加CPU使用率，建议您仅在外网链路有加密需求的时候启用SSL加密。内网链路相对较安全，一般无需对链路加密。

## 操作步骤 {#section_tsc_1rs_ngb .section}

本案例以Linux操作系统的本地服务器为例演示具体操作流程。

1.  下载SSL CA证书，详情请参见[下载SSL CA证书](cn.zh-CN/用户指南/数据安全性/设置 SSL 加密.md#section_ajh_sdv_y2b)。
2.  将解压后的证书文件上传至安装有Mongo Shell的本地服务器或ECS实例中。

    **说明：** 本案例中，将.pem证书文件上传至本地服务器的/root/sslcafile/目录中。

3.  在安装有Mongo Shell的本地服务器或ECS实例中，执行以下命令进行连接。

    ``` {#codeblock_hee_9ho_fwi}
    mongo --host <host> -u <username> -p --authenticationDatabase <database> --ssl --sslCAFile <sslCAFile_path> --sslAllowInvalidHostnames
    ```

    **说明：** 

    -   <host\>：Primary节点或Secondary节点的连接地址（含端口号），详情请参见[副本集实例连接说明](../../../../cn.zh-CN/副本集快速入门/连接实例/副本集实例连接说明.md#)。
        -   如需通过公网连接数据库，需要申请公网连接地址，详情请参见[申请公网连接地址](cn.zh-CN/用户指南/管理网络连接/申请公网连接地址.md#)。
        -   如需通过内网地址连接数据库，需要确保ECS实例与MongoDB实例处于同一网络中。
    -   <username\>：连接数据库的账号，默认为`root`。
    -   <database\>：对连接数据库的账号和密码进行认证的数据库，默认为`admin`。
    -   <sslCAFile\_path\>：SSL证书文件路径。
    示例：

    ``` {#codeblock_tq3_qa1_q18}
    mongo --host dds-bpxxxxxxxx-pub.mongodb.rds.aliyuncs.com:3717 -u root -p --authenticationDatabase admin --ssl --sslCAFile /root/sslcafile/ApsaraDB-CA-Chain.pem  --sslAllowInvalidHostnames
    ```

4.  命令行提示`Enter password:`时，输入数据库账号对应的密码。

    **说明：** 

    -   输入密码时，密码字符是不可见的。
    -   如果忘记了root账号的密码，您可以通过[设置密码](cn.zh-CN/副本集快速入门/设置密码.md#)的方式来重置密码。

## 连接MongoDB数据库的常见场景 {#section_is4_512_f49 .section}

-   [如何通过公网连接MongoDB实例](cn.zh-CN/用户指南/连接实例/如何通过公网连接MongoDB实例.md#)
-   [ECS实例与MongoDB实例网络类型不同时如何连接](cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例网络类型不同时如何连接.md#)
-   [ECS实例与MongoDB实例地域不同时如何连接](cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例地域不同时如何连接.md#)
-   [ECS实例与MongoDB实例不在同一阿里云账号时如何连接](cn.zh-CN/用户指南/连接实例/ECS实例与MongoDB实例不在同一阿里云账号时如何连接.md#)

## 更多信息 {#section_hd6_s9s_n1x .section}

不建议在生产环境中直接使用root用户登录数据库。您可以根据业务需求，创建用户并分配权限，详情请参见[使用DMS管理MongoDB数据库用户](cn.zh-CN/用户指南/账号管理/使用DMS管理MongoDB数据库用户.md#)。

**说明：** 关于DMS中MongoDB数据库的更多相关操作介绍请参见[DMS for MongoDB](https://help.aliyun.com/document_detail/47683.html)。

