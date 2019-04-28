# ECS实例与MongoDB实例不在同一阿里云账号时如何连接 {#concept_tqc_nxm_jhb .concept}

当ECS实例与MongoDB实例不在同一个阿里云账号时，使用本文中的办法可以快速实现实现两者之间的内网连接。

## 方法一 将MongoDB实例迁移至ECS实例所属云账号 {#section_gcp_rxm_jhb .section}

本方法通过[数据传输服务](https://help.aliyun.com/document_detail/26592.html)（Data Transmission Service，简称DTS）的数据迁移功能，将MongoDB数据库迁移至ECS实例所属云账号中。

![跨账号迁移MongoDB](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/156171/155642992544073_zh-CN.png)

**操作步骤**

1.  在ECS所属云账号中创建MongoDB实例，详情请参考[创建实例](../../../../cn.zh-CN/副本集快速入门/创建副本集实例.md#)，如果已经创建可跳过本步骤。

    **说明：** 创建MongoDB实例时，选择与ECS实例相同的**地域**、**可用区**及**专有网络**。

2.  将源云账号中的MongoDB数据库迁移至目标云账号中，详情请参考[使用DTS工具跨阿里云账号迁移MongoDB数据库](cn.zh-CN/用户指南/数据迁移/MongoDB实例间迁移/使用DTS工具跨阿里云账号迁移MongoDB数据库.md#)。
3.  将ECS实例的IP地址加入到目标MongoDB实例的白名单中，详情请参考[设置白名单](cn.zh-CN/用户指南/数据安全性/设置白名单.md#)。

    **说明：** 关于获取ECS实例IP地址信息，请参考[如何查询ECS实例的IP地址](https://help.aliyun.com/knowledge_detail/40637.html#section-vpl-qbg-qgb)。


## 方法二 将ECS实例迁移至MongoDB实例所属云账号 {#section_nh2_xdg_jhb .section}

本方法通过将ECS实例作为自定义镜像共享至MongoDB实例所属云账号的方式，迁移ECS实例数据至MongoDB实例所属云账号中。

**前提条件**

由于不支持跨地域共享镜像，云账号A的ECS实例与云账号B的MongoDB实例必须属于同一地域。

![跨云迁移ECS实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/156171/155642992644127_zh-CN.png)

**操作步骤**

1.  [使用ECS实例创建自定义镜像](https://help.aliyun.com/document_detail/35109.html)。
2.  将创建的自定义镜像共享至MongoDB实例所属云账号，详情请参考[共享镜像](https://help.aliyun.com/document_detail/25463.html)。
3.  [使用自定义镜像创建ECS实例](https://help.aliyun.com/document_detail/25465.html)。

    **说明：** 在创建ECS实例时，选择与MongoDB实例相同的VPC网络。

4.  将ECS实例的IP地址加入MongoDB实例的白名单中，详情请参考[设置白名单](cn.zh-CN/用户指南/数据安全性/设置白名单.md#)。

    **说明：** 关于获取ECS实例IP地址信息，请参考[如何查询ECS实例的IP地址](https://help.aliyun.com/knowledge_detail/40637.html#section-vpl-qbg-qgb)。


## 方法三 ECS实例与MongoDB实例间建立高速通道 {#section_gfv_v1n_jhb .section}

本方法通过[阿里云高速通道](https://help.aliyun.com/document_detail/44848.html)（Express Connect）在不同云账号下的专有网络之间建立连接，实现不同云账号下的ECS实例与MongoDB实例的相互连接。

**说明：** 确保要进行互连的专有网络或交换机的网段不冲突。

![跨云账号ECS与MongoDB建立高速通道](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/156171/155642992644102_zh-CN.png)

**操作步骤**

1.  将MongoDB实例切换为专有网络，详情请参考[切换为专有网络](cn.zh-CN/用户指南/管理网络连接/切换实例网络类型.md#section_tp1_1sl_2fb)，如果已经是专有网络可跳过本步骤。
2.  [将ECS实例迁移至专有网络](https://help.aliyun.com/document_detail/57954.html)，如果已经是专有网络可跳过本步骤。
3.  在ECS实例所属的专有网络与MongoDB所属的专有网络之间建立高速通道，详情请参考[跨账号专有网络互连](https://help.aliyun.com/document_detail/44842.html)。
4.  将ECS实例的IP地址加入MongoDB实例的白名单中，详情请参考[设置白名单](cn.zh-CN/用户指南/数据安全性/设置白名单.md#)。

    **说明：** 关于获取ECS实例IP地址信息，请参考[如何查询ECS实例的IP地址](https://help.aliyun.com/knowledge_detail/40637.html#section-vpl-qbg-qgb)。


## 方法四 ECS实例与MongoDB实例通过云企业网连接 {#section_y3p_rcn_jhb .section}

本方法通过[云企业网](https://help.aliyun.com/document_detail/59870.html)（Cloud Enterprise Network）在不同云账号下的专有网络之间建立连接，实现不同云账号下的ECS实例与MongoDB实例的相互连接。

**说明：** 确保要进行互连的专有网络或交换机的网段不冲突。

![跨云ECS与MongoDB建立云企业网](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/156171/155642992644108_zh-CN.png)

**操作步骤**

1.  将MongoDB实例切换为专有网络，详情请参考[切换为专有网络](cn.zh-CN/用户指南/管理网络连接/切换实例网络类型.md#section_tp1_1sl_2fb)，如果已经是专有网络可跳过本步骤。
2.  [将ECS实例迁移至专有网络](https://help.aliyun.com/document_detail/57954.html)，如果已经是专有网络可跳过本步骤。
3.  根据实际环境选择通过云企业网进行内网互通的方式，详情请参考：
    -   [跨账号同地域互通](https://help.aliyun.com/document_detail/65901.html)。
    -   [跨账号跨地域互通](https://help.aliyun.com/document_detail/65936.html)。
4.  将ECS实例的IP地址加入MongoDB实例的白名单中，详情请参考[设置白名单](cn.zh-CN/用户指南/数据安全性/设置白名单.md#)。

    **说明：** 关于获取ECS实例IP地址信息，请参考[如何查询ECS实例的IP地址](https://help.aliyun.com/knowledge_detail/40637.html#section-vpl-qbg-qgb)。


