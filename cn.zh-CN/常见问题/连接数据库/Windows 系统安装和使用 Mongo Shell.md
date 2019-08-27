# Windows 系统安装和使用 Mongo Shell {#concept_39954_zh .concept}

Mongo shell 是连接 MongoDB 数据库的客户端工具，也可以用来连接云数据库 MongoDB。本文将向您介绍在 Windows 系统中，如何安装和使用 Mongo shell 。

## 安装 Mongo Shell {#section_uj5_ntb_wgb .section}

1.  访问[MongoDB下载页面](https://www.mongodb.com/download-center/community)。
2.  在**Version**区域框，下拉选择需要安装的 MongoDB 版本。

    ![MongoDB下载页面](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6825/155626193039183_zh-CN.png)

    **说明：** 为确保访问 MongoDB 实例时能成功认证，请安装 3.0 及以上的版本。

3.  下载完成后，双击安装包开始安装。

    勾选**I accept the terms in the License Agreement**复选框并单击**Next**。

    ![安装Mongo Shell](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6825/155626193039186_zh-CN.png)

4.  单击**Custom**进行自定义安装。

    ![Mongo Shell自定义安装](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6825/155626193039266_zh-CN.png)

5.  在自定义安装时，只选择安装**Client**并单击**Next**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6825/155626193039267_zh-CN.png)

6.  等待应用程序安装完毕。

## 使用 Mongo Shell {#section_tff_c2c_wgb .section}

打开cmd命令窗口，切换至 mongo.exe 应用程序所在的目录。

示例：

```
cd C:\Program Files\MongoDB\Server\4.0\bin
```

**说明：** 切换至 mongo.exe 应用程序的目录后即可使用 Mongo Shell 工具。

## 更多信息 {#section_vzt_mzb_wgb .section}

[通过 Mongo Shell 登录MongoDB数据库](../../../../cn.zh-CN/副本集快速入门/连接实例/通过 Mongo Shell 登录MongoDB数据库.md#)

