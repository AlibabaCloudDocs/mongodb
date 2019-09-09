# 授权HDM管理MongoDB实例 {#task_2022253 .task}

混合云数据库管理HDM（Hybrid Cloud Database Management）支持多环境统一管理、快速弹性、容灾切换等功能。为帮助用户更便捷地运维，云数据库MongoDB版集成了HDM部分功能，当您首次使用CloudDBA中的实时性能、实例会话和空间分析功能时，您需要授权HDM管理MongoDB实例。

## 操作步骤 {#section_2oa_iu1_s1t .section}

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。
2.  在页面左上角，选择实例所在的地域。
3.  根据实例类型，在左侧导航栏单击**副本集实例列表**或**分片集群实例列表**。
4.  找到目标实例，单击实例ID。
5.  在左侧导航栏，选择**CloudDBA** \> **实时性能**。
6.  填写数据库账号数据库密码并授权。 使用已存在的数据库账号，请参考下述步骤操作：

    1.  输入数据库账号和密码信息。
    2.  单击**授权**。
    3.  单击**完成**。 

        ![完成授权](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1605566/156801652258837_zh-CN.png)

    创建一个新的数据库账号，请参考下述步骤操作：

    1.  输入待创建的数据库账号和密码信息。 

        **说明：** 

        -   账户名以小写字母开头，长度为4~16位，由小写字母、数字或下划线组成
        -   密码由大写字母、小写字母、数字、特殊字符中的至少三种组成，长度为6~32位，特殊字符为!\#$%^&\*\(\)\_+-=
    2.  单击**生成授权命令**。
    3.  使用mongo shell登录数据库，详情请参见[登录单节点实例](../../../../cn.zh-CN/单节点快速入门/连接实例/通过Mongo Shell登录MongoDB数据库.md#)、[登录副本集实例](../../../../cn.zh-CN/副本集快速入门/连接实例/通过Mongo Shell登录MongoDB数据库.md#)或[登录分片集群实例](../../../../cn.zh-CN/分片集群快速入门/连接实例/通过 Mongo Shell 登录MongoDB数据库.md#)。
    4.  返回实时性能页面，单击**点击复制到剪切板**复制生成的命令。 

        ![复制授权命令](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1605566/156801652258832_zh-CN.png)

    5.  在mongo shell中粘贴该命令并执行，命令行返回`Successfully`即代表成功创建数据库账号。 

        ![执行授权命令](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1605566/156801652258834_zh-CN.png)

    6.  返回实时性能页面，单击**授权**。
    7.  单击**完成**。

页面将自动刷新，可正常使用实时性能、实例会话和空间分析功能，不再提示需要授权。

