# 设置自动备份MongoDB数据 {#concept_gs1_qrp_dgb .concept}

云数据库MongoDB会按照默认的备份策略自动备份MongoDB数据。您也可以根据业务需求配置备份策略，实例将按照您设置的备份策略自动备份MongoDB数据。

## 自动备份说明 {#section_qzv_nsp_dgb .section}

-   云数据库MongoDB生成的备份文件存储在[阿里云对象存储服务](https://www.alibabacloud.com/help/zh/doc-detail/31817.htm)（Object Storage Service，简称 OSS）中，不会占用MongoDB实例的存储空间。
-   单节点实例的备份方式固定为[快照备份](intl.zh-CN/用户指南/数据备份/手动备份实例.md#ul_iw5_lcp_dgb)，备份过程中将占用单节点实例的I/O性能。
-   副本集实例和分片集群实例的备份方式为[物理备份](intl.zh-CN/用户指南/数据备份/手动备份实例.md#ul_iw5_lcp_dgb)。

    **说明：** 物理备份在MongoDB实例的隐藏节点进行，不影响主从节点的读写性能。若数据量较大，花费的时间可能较长，请耐心等待。


## 设置自动备份策略 {#section_msc_bsp_dgb .section}

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/#/mongodb/list)。
2.  在页面左上角，选择实例所在的地域。
3.  根据实例类型，在左侧导航栏单击**副本集实例列表**或**分片集群实例列表**。
4.  找到目标实例，单击实例ID。
5.  在左侧导航栏，单击**备份与恢复**。
6.  单击**备份设置**。

    ![MongoDB备份与恢复列表](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6721/155012826937422_zh-CN.png)

7.  在备份设置对话框，按照页面提示进行设置参数。

    ![MongoDB设置自动备份策略](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6721/155012827034383_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**保留天数**|数据保留天数固定为7天。|
    |**备份时间**|可以设置为任意时段，以小时为单位，建议设置的备份时间为业务低峰期的时间。|
    |**备份周期**|可以设置为一星期中的某一天或者某几天。|

8.  完成上述参数配置后，单击**确定**。

