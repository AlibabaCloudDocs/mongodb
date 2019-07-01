# Create a multi-zone replica set instance {#concept_m1g_yk5_xfb .concept}

ApsaraDB for MongoDB provides a zone-disaster recovery solution for replica set instances. This solution deploys the three nodes of a three-node replica set instance in three different [zones](../../../../intl.en-US/Product Introduction/Glossary.md#ul_icc_njg_hfb) in the same region. The components in these zones exchange data through the internal network. If any of the three zones becomes unavailable due to unexpected events such as a power or network failure, the high availability system will automatically switch to another zone to ensure the availability of the entire replica set.

## Precautions {#section_qbs_ng5_xfb .section}

-   Standalone instances do not support this function.
-   You can create multi-zone sharded cluster instances in China \(Hangzhou\), China \(Beijing\), and China \(Shenzhen\).
-   When you create a multi-zone replica set instance, you must set **Replication Factor** to **Three Nodes Replica set**.

    **Note:** If you need more nodes, you can [reset the node number](intl.en-US/User Guide/Instance management/Change the number of nodes in replica set instances.md#) after you create the instance.


## Node deployment policies of a replica set instance {#section_wjr_qpj_wgb .section}

When you create a single-zone instance, the system deploys the primary, secondary, and hidden nodes in one zone.

![Single-zone deployment](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64995/156197078733038_en-US.png)

When you create a multi-zone instance, the system deploys the primary, secondary, and hidden nodes in three different zones.

![Multi-zone deployment](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64995/156197078739357_en-US.png)

## Procedure {#section_jrk_v35_xfb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the left-side navigation pane, click **Replica Set Instances**.
3.  On the Replica Set Instances page, click **Create Instance**.
4.  On the Create Instance page, set **Region** to **China \(Hangzhou\)**, **China \(Shanghai\)**, **China \(Shenzhen\)**, or **China \(Beijing\)**, and select a multi-zone you need.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64995/156197078833041_en-US.png)

5.  For more information about other parameters for the instance, see [Create an instance](../../../../intl.en-US/Quick Start for Replica Set/Create an instance.md#).
6.  Click **Buy Now**. The Confirm Order page appears.
7.  Read and select **ApsaraDB for MongoDB Agreement of Service**, and make the payment as prompted.

