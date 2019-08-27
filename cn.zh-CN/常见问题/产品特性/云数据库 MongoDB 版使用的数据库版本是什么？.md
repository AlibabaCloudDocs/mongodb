# 云数据库 MongoDB 版使用的数据库版本是什么？ {#concept_39950_zh .concept}

云数据库 MongoDB 版使用的数据库版本为**3.2.13**、**3.4.6**和**4.0.0**。建议使用支持对应数据库版本的 driver 来访问，您可以从[官网](https://docs.mongodb.org/ecosystem/drivers/)下载各语言的 driver。

**说明：** 各版本区别详见[版本及存储引擎](../../../../intl.zh-CN/产品简介/版本及存储引擎.md#)。

## 如何查看MongoDB实例使用的数据库版本 {#section_hvv_mpt_vgb .section}

1.  [通过Mongo Shell登录实例](../../../../intl.zh-CN/副本集快速入门/连接实例/副本集实例连接说明.md#)。
2.  执行以下命令查看数据库版本。

    ```
    db.version()
    ```

    执行上述命令后查看到使用的数据库版本为4.0.0。

    ```
    mgset-12xxxx:PRIMARY> db.version()
    4.0.0
    ```


## 更多信息 {#section_uhr_4x5_vgb .section}

[升级数据库版本](../../../../intl.zh-CN/用户指南/实例管理/升级数据库版本.md#)

