# 经典网络平滑迁移到VPC的混访方案 {#concept_ysg_ngz_lgb .concept}

为满足日益增多的网络迁移需求，云数据库MongoDB新增了网络混访功能，可实现在无闪断、无访问中断的情况下将经典网络平滑迁移到专有网络VPC（Virtual Private Cloud）上。

## 前提条件 {#section_kvs_c3z_lgb .section}

实例类型为副本集实例或分片集群实例。

## 功能限制 {#section_zlb_rgz_lgb .section}

在混访期间，不支持切换成经典网络。

## 方案介绍 {#section_kmf_qgz_lgb .section}

将MongoDB实例从经典网络切换至VPC时，经典网络的地址会被立即释放，造成1次30秒内的闪断，且经典网络内的云产品（如[ECS](https://www.alibabacloud.com/help/zh/doc-detail/25367.htm)）将无法再连接该MongoDB实例。

混访方案将支持MongoDB实例同时被经典网络和专有网络内的ECS所连接，实现平滑的网络类型切换。在将MongoDB实例从经典网络切换至专有网络时，可选择在生成新的专有网络连接地址的同时，保留当前经典网络地址（最长可保留120天）。使得在实例迁移的过渡期间，该实例可以同时被经典网络和专有网络内的ECS所访问。

在实例混访期间，客户可以逐步将处于经典网络内的ECS和其他云产品切换或迁移至专有网络，直至最终所有产品都使用更为安全的专有网络进行内网连通。

## 网络迁移步骤 {#section_u3z_rgz_lgb .section}

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/#/mongodb/list)。
2.  在页面左上角，选择实例所在的地域。
3.  根据实例类型，在左侧导航栏单击**副本集实例列表**或**分片集群实例列表**。
4.  找到目标实例，单击实例ID。
5.  在左侧导航栏，单击**数据库连接**。
6.  在内网连接 - 经典网络区域框，单击**切换为专有网络**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6717/155617363337277_zh-CN.png)

7.  在弹出的专有网络对话框，设置相关参数。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6718/155617363337314_zh-CN.png)

    1.  选择**专有网络**和**交换机**。

        **说明：** 如您尚未创建专有网络和交换机，请参考[创建专有网络和交换机](https://www.alibabacloud.com/help/zh/doc-detail/65398.htm)。

    2.  打开**保留经典网络**开关。
    3.  选择**过期时间**天数。
8.  单击**确定**。

