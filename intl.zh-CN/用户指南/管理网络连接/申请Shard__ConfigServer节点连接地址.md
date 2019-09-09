# 申请Shard/ConfigServer节点连接地址 {#task_1941822 .task}

分片集群实例由Mongos节点、Shard节点和ConfigServer节点共同组成，一般业务读写数据只需连接至Mongos节点即可。在某些特定场景下（例如集群间数据同步），需要读取Shard节点的oplog或ConfigServer节点的配置信息，您可以申请相应节点的连接地址，以满足业务需求。

实例为分片集群实例。

## 申请须知 {#section_hz0_msb_3yp .section}

-   申请连接地址后，系统将为每个节点创建两个连接地址，分别对应该节点中的Primary节点和Secondary节点。
-   申请的连接地址的网络类型将与当前Mongos节点的网络类型保持一致。
-   申请Shard节点或ConfigServer节点的连接地址后，暂不支持修改。
-   申请的连接地址仅支持通过内网访问，如需通过公网访问，请[申请公网连接地址](../../../../intl.zh-CN/分片集群快速入门/申请公网连接地址.md#)。

## 分片集群架构及节点介绍 {#section_kvp_cwu_el2 .section}

详情请参见[分片集群架构](../../../../intl.zh-CN/产品简介/系统架构/分片集群架构.md#)。

## 操作步骤 {#section_sd1_w3m_pff .section}

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。
2.  在页面左上角，选择实例所在的地域。
3.  在左侧导航栏，单击**分片集群实例列表**。
4.  找到目标实例，单击实例ID。
5.  在左侧导航栏，单击**数据库连接**。
6.  单击页面右上角的**申请Shard\\ConfigServer地址**。
7.  在弹出的对话框中，为Shard节点或ConfigServer节点申请连接地址。 

    ![申请节点地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1540112/156799919458471_zh-CN.png)

    |配置|说明|
    |--|--|
    |**节点类型**|     -   **shard**：Shard节点。
    -   **cs**：ConfigServer节点。
 |
    |**选择要创建连接地址的ID**|单击对应的复选框，选择需要创建连接地址的节点ID。|
    |**账户名**|账户名以小写字母开头，长度为4~16位，由小写字母、数字或下划线组成。 **说明：** 

    -   仅在首次申请Shard/ConfigServer地址时，需要设置账户名和账户密码。即所有Shard节点和ConfigServer节点都将使用首次申请地址时设置的账户和密码。
    -   该账户的权限固定为只读权限。
 |
    |**账户密码**|     -   密码由大写字母、小写字母、数字、特殊字符中的至少三种组成，特殊字符为!\#$%^&\*\(\)\_+-=
    -   密码长度为8~32位
 **说明：** 如果后续忘记密码，您可以[重置密码](intl.zh-CN/用户指南/账号管理/重置密码.md#)。

 |
    |**确认密码**|再次输入账户密码。|

8.  单击**确定**。
9.  等待实例状态从**正在创建网络连接**转变为**运行中**。

## 节点类型说明 {#section_p8y_gnl_uno .section}

![节点类型](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1540112/156799919458494_zh-CN.png)

申请Shard/ConfigServer节点的连接地址后，您可以在数据库连接页面查看到连接地址的信息，节点类型说明如下：

|节点类型|说明|
|----|--|
|**db**|Shard节点。|
|**cs**|ConfigServer节点。|
|**mongos**|Mongos节点。|

## 选择节点时如何确认节点的角色 {#section_8ib_myo_04o .section}

如您需要连接Shard节点或ConfigServer节点中指定角色的节点（例如连接Shard节点中的Primary节点），您可以在单击左侧导航栏，单击基本信息，在基本信息页面的Shard列表或Configserver列表区域框中可获取节点的角色信息。

![节点角色信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1540112/156799919458686_zh-CN.png)

## 相关文档 {#section_3oy_qhx_tfh .section}

如果不再需要Shard节点或ConfigServer节点的连接地址，您可以[释放Shard/ConfigServer节点连接地址](intl.zh-CN/用户指南/管理网络连接/释放Shard__ConfigServer节点连接地址.md#)。

