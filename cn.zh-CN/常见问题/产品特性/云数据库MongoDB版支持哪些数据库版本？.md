# 云数据库MongoDB版支持哪些数据库版本？

云数据库MongoDB版支持的数据库版本为4.4、4.2、4.0和3.4。建议使用对应数据库版本的客户端来访问，您可以从[官网](https://docs.mongodb.org/ecosystem/drivers/)下载各语言的客户端。

**说明：** 各版本区别请参见[版本及存储引擎](/cn.zh-CN/产品简介/版本及存储引擎.md)。

## 如何查看MongoDB实例使用的数据库版本

1.  通过Mongo Shell连接MongoDB副本集实例。详情请参见[通过Mongo Shell连接MongoDB副本集实例](/cn.zh-CN/快速入门/连接实例/通过Mongo Shell连接MongoDB副本集实例.md)。
2.  执行以下命令查看数据库版本。

    ```
    db.version()
    ```


## 更多信息

[升级数据库版本](/cn.zh-CN/用户指南/实例管理/数据库升级/升级数据库版本.md)

