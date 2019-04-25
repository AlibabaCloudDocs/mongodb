# Zone-disaster recovery solution {#concept_m1g_yk5_xfb .concept}

ApsaraDB for MongoDB allows you to deploy the three nodes of a three-node replica set instance separately in three different zones \(IDCs\) of the same city. In this case, the three nodes can be interconnected through an intranet to support zone-disaster recovery. If any of the three nodes become disconnected due to a power failure, network disconnection, or other force majeure factors in its zone, the high availability system of ApsaraDB for MongoDB can trigger a failover to ensure the continuous availability of the replica set architecture.

## Notes {#section_qbs_ng5_xfb .section}

-   Only replica set instances support zone-disaster recovery. Standalone and sharded cluster instances do not support this solution.
-   Currently, zone-disaster recovery is supported only in the following regions: China \(Hangzhou\), China \(Shanghai\), China \(Beijing\), and China \(Shenzhen\).

The following figure shows a comparison between the single-zone solution and the multi-zone solution \(which supports zone-disaster recovery\).

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64995/155618238633038_en-US.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64995/155618238639357_en-US.png)

## Create an instance that supports zone-disaster recovery {#section_jrk_v35_xfb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the left-side navigation pane, click **Replica Set Instances**.
3.  On the Replica Set Instances page that appears, click **Create Instance** to go to the instance creation page.
4.  Select China \(Hangzhou\), China \(Shanghai\), China \(Beijing\), or China \(Shenzhen\) for Region. Select a multi-zone in the selected region.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64995/155618238633041_en-US.png)

5.  Specify other instance configuration. For more information, see [Create an instance](../../../../intl.en-US/Quick Start for Replica Set/Create an instance.md#).
6.  Click **Buy Now** to go to the Confirm Order page.
7.  Read and select ApsaraDB for MongoDB Agreement of Service and follow the instructions to complete the payment process.

