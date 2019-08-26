# Create a multi-zone sharded cluster instance {#concept_262036 .concept}

ApsaraDB for MongoDB provides a zone-disaster recovery solution for sharded cluster instances. This solution deploys the components of a sharded cluster instance across three different [zones](../../../../intl.en-US/Product Introduction/Glossary.md#ul_icc_njg_hfb) in one region. The components in these zones exchange data through the internal network. If any of the three zones becomes unavailable due to unexpected events such as a power or network failure, the high availability system will automatically switch to another zone to ensure the availability of the entire sharded cluster.

## Precautions {#section_qbs_ng5_xfb .section}

-   Standalone instances do not support this function.
-   You can create only multi-zone sharded cluster instances in **China \(Hangzhou\)**, **China \(Beijing\)**, and **China \(Shenzhen\)**.

## Node deployment policy {#section_wjr_qpj_wgb .section}

When you create a single-zone instance, the system deploys the components of the sharded cluster instance in one zone. When you create a multi-zone instance, the system deploys the components in three different zones.

-   Mongos are evenly deployed across all data centers. At least two mongos are deployed across two zones. When a third mongos is added, it is deployed in the third zone. Each subsequent new mongos is deployed to each of the three zones in turn.
-   The primary, secondary, and hidden nodes of each shard are not deployed to the three zones in sequence. The deployment of these nodes may change based on whether manual switchover or HA failover between primary and secondary nodes is used.

![](images/46749_en-US.png "Deployment policy for the components and nodes in a multi-zone sharded cluster instance")

## Procedure {#section_jrk_v35_xfb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the left-side navigation pane, click **Sharding Instances**.
3.  On the Sharding instances page, click **Create Instance**.
4.  On the Create Instance page, set **Region** to **China \(Hangzhou\)**, **China \(Beijing\)**, or **China \(Shenzhen\)**, and select the zones that you require.

    ![Select a multi-zone to create a sharded cluster instance](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216351/156680398446740_en-US.png)

5.  For more information about other parameters for the instance, see [Create a sharded cluster instance](../../../../intl.en-US/Quick Start for Cluster/Create a sharded cluster instance.md#).
6.  Click **Buy Now**. The Confirm Order page appears.
7.  Read and select **ApsaraDB for MongoDB Agreement of Service**, and make the payment as prompted.

