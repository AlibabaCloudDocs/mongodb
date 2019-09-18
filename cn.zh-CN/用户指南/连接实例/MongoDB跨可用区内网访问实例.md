# MongoDB跨可用区内网访问实例 {#concept_57139_zh .concept}

阿里云当前内网类型分为经典网络和专有网络两种，在同一地域内的云产品（如ECS与MongoDB产品之间）即使跨可用区也可以通过内网进行连接。

MongoDB跨可用区通过内网连接ECS实例分为以下两种情况。

## 新购MongoDB实例与ECS实例连接 {#section_mw3_b5w_fgb .section}

-   如果ECS实例为专有网络，则在同一地域的其他可用区新购MongoDB实例时，需确保MongoDB实例与待连接的ECS实例同为一个专有网络ID，并在MongoDB所在可用区新建一个交换机，即可确保两个实例间通过内网进行正常的连接访问。
-   如果ECS实例为经典网络，则在同一个地域的其他可用区新购MongoDB实例时，需确保所购MongoDB实例与ECS实例均属同一个地域内的经典网络，即可实现两个实例间跨可用区连接。

## 已有MongoDB实例与ECS实例连接 {#section_v2b_25w_fgb .section}

需要ECS实例与MongoDB实例在同一地域。

-   若ECS实例与MongoDB实例网络类型一致，则两个实例间即可进行内网连接。

    **说明：** 两者均为经典网络或者专有网络。如果是专有网络，ECS实例与MongoDB实例必须为同一个VPCID。

-   若ECS实例与MongoDB实例网络类型不一致，则可通过MongoDB提供的[网络类型切换功能](cn.zh-CN/用户指南/管理网络连接/切换实例网络类型.md#)，将网络类型切换为一致，再进行连接。

    **说明：** 单节点实例不支持网络类型切换功能。


