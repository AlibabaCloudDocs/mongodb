# 云数据库MongoDB版如何备份和恢复 {#concept_bps_bcd_lfb .concept}

云数据库MongoDB版支持自动备份和手动备份，您可以基于备份文件或按实例运行的时间点进行数据恢复。

## 备份说明 {#section_769_cse_u3h .section}

您可以根据业务需求，通过控制台[设置自动备份MongoDB数据](../../../../cn.zh-CN/用户指南/数据备份/设置自动备份MongoDB数据.md#)或[手动备份MongoDB数据](../../../../cn.zh-CN/用户指南/数据备份/手动备份MongoDB数据.md#)。

-   云数据库MongoDB版生成的备份文件存储在[阿里云对象存储服务OSS](https://help.aliyun.com/document_detail/31817.html)（Object Storage Service）中，不会占用MongoDB实例的存储空间。
-   单节点实例的备份方式固定为快照备份，备份过程中将占用单节点实例的I/O性能。
-   副本集实例或分片集群实例支持物理备份和逻辑备份。

    **说明：** 

    -   自动备份时，备份方式固定为物理备份。
    -   物理备份和逻辑备份在MongoDB实例的隐藏节点进行，不影响主从节点的读写性能。若数据量较大，花费的时间可能较长，请耐心等待。

## 备份方式 {#section_vji_xxi_oez .section}

-   快照备份：由于单节点实例的架构的特殊性，单节点实例采用快照备份的方式。快照备份可以保留某一时间点的磁盘数据状态。
-   物理备份：通过备份MongoDB实例中，数据库相关的实际物理文件实现备份操作。
-   逻辑备份：通过mongodump工具进行实现，将整个数据库的数据进行逻辑备份。

## 如何恢复 {#section_r9h_ww5_pcd .section}

详情请参见[MongoDB数据恢复方案概览](../../../../cn.zh-CN/用户指南/数据恢复/MongoDB数据恢复方案概览.md#)。

