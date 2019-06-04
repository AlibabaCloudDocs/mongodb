# ECS实例与MongoDB实例地域不同时如何连接 {#concept_zmx_c1g_jhb .concept}

当ECS实例与MongoDB实例的地域不同时，您可根据本文中的办法快速实现两者之间的连接。

## 方法一 ECS实例与MongoDB实例间建立高速通道 {#section_pbh_c2g_jhb .section}

本方法将ECS实例和MongoDB实例切换为专有网络，再通过[阿里云高速通道](https://help.aliyun.com/document_detail/44848.html)（Express Connect）实现不同地域下的专有网络互通，例如在华北1下ECS实例的专有网络与华东1下MongoDB实例的专有网络之间建立高速通道。

**说明：** 确保要进行互连的专有网络或交换机的网段不冲突。

![ECS与MongoDB跨地域建立高速通道](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/155344/155963283643754_zh-CN.png)

1.  将MongoDB实例切换为专有网络，详情请参考[切换为专有网络](cn.zh-CN/用户指南/管理网络连接/切换实例网络类型.md#section_tp1_1sl_2fb)，如果已经是专有网络可跳过本步骤。
2.  [将ECS实例迁移至专有网络](https://help.aliyun.com/document_detail/57954.html)，如果已经是专有网络可跳过本步骤。
3.  在ECS实例所属的专有网络与MongoDB所属的专有网络之间建立高速通道，详情请参考[同账号专有网络互连](https://help.aliyun.com/document_detail/44843.html)。
4.  将ECS实例的IP地址加入MongoDB实例的白名单中，详情请参考[设置白名单](cn.zh-CN/用户指南/数据安全性/设置白名单.md#)。

    **说明：** 关于获取ECS实例IP地址信息，请参考[如何查询ECS实例的IP地址](https://help.aliyun.com/knowledge_detail/40637.html#section-vpl-qbg-qgb)。


## 方法二 将MongoDB实例迁移至ECS实例所属地域 {#section_efv_hcg_jhb .section}

本方法通过[数据传输服务](https://help.aliyun.com/document_detail/26592.html)（Data Transmission Service，简称DTS）的数据迁移功能，实现迁移MongoDB实例至ECS实例所属地域的目的，例如将MongoDB实例从华北1迁移至华东1。

1.  在ECS所属地域创建MongoDB实例，详情请参考[创建实例](../../../../cn.zh-CN/副本集快速入门/创建副本集实例.md#)，如果已创建可跳过本步骤。
2.  将源地域下的MongoDB数据库迁移至目标MongoDB实例，详情请参考[使用DTS工具迁移MongoDB数据库至其他地域](cn.zh-CN/用户指南/数据迁移/MongoDB实例间迁移/使用DTS工具迁移MongoDB数据库至其他地域.md#)。
3.  将ECS实例的IP地址加入目标MongoDB实例的白名单中，详情请参考[设置白名单](cn.zh-CN/用户指南/数据安全性/设置白名单.md#)。

    **说明：** 关于获取ECS实例IP地址信息，请参考[如何查询ECS实例的IP地址](https://help.aliyun.com/knowledge_detail/40637.html#section-vpl-qbg-qgb)。


![迁移MongoDB至其他地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/155400/155963283643672_zh-CN.png)

## 方法三 将ECS实例迁移至MongoDB实例所属地域 {#section_nh2_xdg_jhb .section}

下述两种方法分别通过自定义镜像和迁云工具，实现迁移ECS实例数据至MongoDB实例所属地域的目的，例如将ECS实例从华北1迁移至华东1。

![迁移ECS地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/155344/155963283643766_zh-CN.png)

-   将ECS实例作为自定义镜像，在MongoDB实例所属地域使用该镜像创建新的ECS实例。（推荐）
    1.  [使用ECS实例创建自定义镜像](https://help.aliyun.com/document_detail/35109.html)。
    2.  将创建的自定义镜像复制到MongoDB实例所属地域，详情请参考[复制镜像](https://help.aliyun.com/document_detail/25462.html)。
    3.  [使用自定义镜像创建ECS实例](https://help.aliyun.com/document_detail/25465.html)。

        **说明：** 在创建ECS实例时，选择与MongoDB实例相同的VPC网络。

    4.  将ECS实例的IP地址加入MongoDB实例的白名单中，详情请参考[设置白名单](cn.zh-CN/用户指南/数据安全性/设置白名单.md#)。

        **说明：** 关于获取ECS实例IP地址信息，请参考[如何查询ECS实例的IP地址](https://help.aliyun.com/knowledge_detail/40637.html#section-vpl-qbg-qgb)。

-   使用迁云工具迁移ECS实例至MongoDB实例所属地域。
    1.  迁移ECS实例至MongoDB实例所属地域，详情请参考[ECS实例间迁移](https://help.aliyun.com/document_detail/100988.html)。
    2.  将ECS实例的IP地址加入MongoDB实例的白名单中，详情请参考[设置白名单](cn.zh-CN/用户指南/数据安全性/设置白名单.md#)。

        **说明：** 关于获取ECS实例IP地址信息，请参考[如何查询ECS实例的IP地址](https://help.aliyun.com/knowledge_detail/40637.html#section-vpl-qbg-qgb)。


