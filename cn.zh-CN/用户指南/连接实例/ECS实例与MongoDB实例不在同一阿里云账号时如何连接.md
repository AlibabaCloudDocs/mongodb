# ECS实例与MongoDB实例不在同一阿里云账号时如何连接

当ECS实例与MongoDB实例不在同一个阿里云账号时，使用本文中的办法可以快速实现两者之间的内网连接。

## 方法一：将MongoDB实例迁移至ECS实例所属云账号

本方法通过[数据传输服务](/cn.zh-CN/产品简介/什么是数据传输服务DTS.md)DTS（Data Transmission Service）的数据迁移功能，将MongoDB数据库迁移至ECS实例所属云账号中。

![跨账号迁移MongoDB](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8836819951/p44073.png)

操作步骤

1.  在ECS所属云账号中创建MongoDB实例，详情请参见[创建实例](/cn.zh-CN/快速入门/创建实例/创建副本集实例.md)，如果已经创建可跳过本步骤。

    **说明：** 创建MongoDB实例时，选择与ECS实例相同的**地域**、**可用区**及**专有网络**。

2.  将源云账号中的MongoDB数据库迁移至目标云账号中，详情请参见[跨阿里云账号迁移MongoDB实例](/cn.zh-CN/用户指南/数据迁移和同步/MongoDB实例间迁移/跨阿里云账号迁移MongoDB实例.md)。
3.  将ECS实例的IP地址加入到目标MongoDB实例的白名单中，详情请参见[设置白名单](/cn.zh-CN/用户指南/数据安全性/设置白名单及安全组.md)。

    **说明：** 关于获取ECS实例IP地址信息，请参见[如何查询ECS实例的IP地址](https://help.aliyun.com/knowledge_detail/40637.html#section-vpl-qbg-qgb)。


## 方法二：将ECS实例迁移至MongoDB实例所属云账号

本方法通过将ECS实例作为自定义镜像共享至MongoDB实例所属云账号的方式，迁移ECS实例数据至MongoDB实例所属云账号中。

前提条件

由于不支持跨地域共享镜像，云账号A的ECS实例与云账号B的MongoDB实例必须属于同一地域。

![跨云迁移ECS实例](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8836819951/p44127.png)

操作步骤

1.  [使用ECS实例创建自定义镜像](~~35109~~)。
2.  将创建的自定义镜像共享至MongoDB实例所属云账号，详情请参见[共享镜像](~~25463~~)。
3.  [使用自定义镜像创建ECS实例](~~25465~~)。

    **说明：** 在创建ECS实例时，选择与MongoDB实例相同的VPC网络。

4.  将ECS实例的IP地址加入MongoDB实例的白名单中，详情请参见[设置白名单](/cn.zh-CN/用户指南/数据安全性/设置白名单及安全组.md)。

    **说明：** 关于获取ECS实例IP地址信息，请参见[如何查询ECS实例的IP地址](https://help.aliyun.com/knowledge_detail/40637.html#section-vpl-qbg-qgb)。


## 方法三：ECS实例与MongoDB实例通过云企业网连接

本方法通过[云企业网](~~59870~~)（Cloud Enterprise Network）在不同云账号下的专有网络之间建立连接，实现不同云账号下的ECS实例与MongoDB实例的相互连接。

**说明：** 确保要进行互连的专有网络或交换机的网段不冲突。

![跨云ECS与MongoDB建立云企业网](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8836819951/p44108.png)

操作步骤

1.  将MongoDB实例切换为专有网络，详情请参见[切换为专有网络](/cn.zh-CN/用户指南/管理网络连接/切换实例网络类型.md)，如果已经是专有网络可跳过本步骤。
2.  [将ECS实例迁移至专有网络](~~57954~~)，如果已经是专有网络可跳过本步骤。
3.  根据实际环境选择通过云企业网进行内网互通的方式，详情请参见：
    -   [跨账号同地域互通](~~65901~~)。
    -   [跨账号跨地域互通](~~65936~~)。
4.  将ECS实例的IP地址加入MongoDB实例的白名单中，详情请参见[设置白名单](/cn.zh-CN/用户指南/数据安全性/设置白名单及安全组.md)。

    **说明：** 关于获取ECS实例IP地址信息，请参见[如何查询ECS实例的IP地址](https://help.aliyun.com/knowledge_detail/40637.html#section-vpl-qbg-qgb)。


