# 手动备份MongoDB数据 {#concept_e1s_szs_qgb .concept}

您可以通过设置备份策略，调整云数据库MongoDB数据备份周期实现自动备份数据，也可以手动备份MongoDB数据。

## 备份说明 {#section_cbl_mbp_dgb .section}

-   云数据库MongoDB生成的备份文件，存储在[阿里云对象存储服务](https://help.aliyun.com/document_detail/31817.html)（Object Storage Service，简称 OSS）中，不会占用MongoDB实例的存储空间。
-   单节点实例的备份方式固定为快照备份，备份过程中将占用单节点实例的I/O性能。
-   副本集实例或分片集群支持物理备份和逻辑备份。
-   物理备份和逻辑备份在MongoDB实例的隐藏节点进行，不影响主从节点的读写性能。若数据量较大，花费的时间可能较长，请耐心等待。

## 备份方法 {#section_jmr_kcp_dgb .section}

-   快照备份：由于单节点实例的架构的特殊性，单节点实例采用快照备份的方式。快照备份可以保留某一时间点的磁盘数据状态。
-   物理备份：通过备份MongoDB实例中，数据库相关的实际物理文件实现备份操作。
-   逻辑备份：通过mongodump工具进行实现，将整个数据库的数据进行逻辑备份。

## 操作步骤 {#section_w1s_ccp_dgb .section}

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/#/mongodb/list)。
2.  在页面左上角，选择实例所在的地域。
3.  根据实例类型，在左侧导航栏单击**副本集实例列表**或**分片集群实例列表**。
4.  找到目标实例，单击实例ID。
5.  在左侧导航栏，单击**备份与恢复**。
6.  在页面右上角，单击**备份实例**。
7.  在备份实例窗口，选择**备份方法**。

    ![选择备份方法](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6722/15687919797041_zh-CN.png)

8.  单击**确定**。

## 相关文档 {#section_ez9_x8f_vow .section}

[MongoDB数据恢复方案概览](cn.zh-CN/用户指南/数据恢复/MongoDB数据恢复方案概览.md#)

