# ECS实例与MongoDB实例地域不同时如何连接

当ECS实例与MongoDB实例的地域不同时，您可根据本文中的办法快速实现两者之间的连接。

## 方法一：将MongoDB实例迁移至ECS实例所属地域

本方法通过[数据传输服务](/cn.zh-CN/产品简介/什么是数据传输服务DTS.md)DTS（Data Transmission Service）的数据迁移功能，实现迁移MongoDB实例至ECS实例所属地域的目的，例如将MongoDB实例从华北1迁移至华东1。

![迁移MongoDB至其他地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0897549951/p43672.png)

1.  在ECS所属地域创建MongoDB实例，详情请参见[创建实例](/cn.zh-CN/快速入门/创建实例/创建副本集实例.md)，如果已创建可跳过本步骤。
2.  将源地域下的MongoDB数据库迁移至目标MongoDB实例，详情请参见[迁移MongoDB实例至其他地域](/cn.zh-CN/用户指南/数据迁移和同步/MongoDB实例间迁移/迁移MongoDB实例至其他地域.md)。
3.  将ECS实例的IP地址加入目标MongoDB实例的白名单中，详情请参见[设置白名单](/cn.zh-CN/用户指南/数据安全性/设置白名单及安全组.md)。

    **说明：** 关于获取ECS实例IP地址信息，请参见[如何查询ECS实例的IP地址](~~40637~~)。


## 方法二：将ECS实例迁移至MongoDB实例所属地域

下述两种方法分别通过自定义镜像和迁云工具，实现迁移ECS实例数据至MongoDB实例所属地域的目的，例如将ECS实例从华北1迁移至华东1。

![迁移ECS地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7836819951/p43766.png)

-   将ECS实例作为自定义镜像，在MongoDB实例所属地域使用该镜像创建新的ECS实例。（推荐）
    1.  [使用ECS实例创建自定义镜像](~~35109~~)。
    2.  将创建的自定义镜像复制到MongoDB实例所属地域，详情请参见[复制镜像](~~25462~~)。
    3.  [使用自定义镜像创建ECS实例](~~25465~~)。

        **说明：** 在创建ECS实例时，选择与MongoDB实例相同的VPC网络。

    4.  将ECS实例的IP地址加入MongoDB实例的白名单中，详情请参见[设置白名单](/cn.zh-CN/用户指南/数据安全性/设置白名单及安全组.md)。

        **说明：** 关于获取ECS实例IP地址信息，请参见[如何查询ECS实例的IP地址](https://help.aliyun.com/knowledge_detail/40637.html#section-vpl-qbg-qgb)。

-   使用迁云工具迁移ECS实例至MongoDB实例所属地域。
    1.  迁移ECS实例至MongoDB实例所属地域，详情请参见[ECS实例间迁移](~~100988~~)。
    2.  将ECS实例的IP地址加入MongoDB实例的白名单中，详情请参见[设置白名单](/cn.zh-CN/用户指南/数据安全性/设置白名单及安全组.md)。

