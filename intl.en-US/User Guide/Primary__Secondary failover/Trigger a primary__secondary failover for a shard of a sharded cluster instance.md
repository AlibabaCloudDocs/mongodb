# Trigger a primary/secondary failover for a shard of a sharded cluster instance {#concept_wcc_cc5_cgb .concept}

Each shard of a sharded cluster instance consists of three nodes by default. If a node is faulty, the high availability system of ApsaraDB for MongoDB automatically triggers a primary/secondary failover to guarantee the availability of the shard. In addition, you can manually trigger a primary/secondary failover for an ApsaraDB for MongoDB instance in scenarios such as routine disaster recovery drills.

## Notes {#section_ind_2c5_cgb .section}

ApsaraDB for MongoDB provides addresses for you to connect to the primary node and a secondary node of a shard. The other secondary node is hidden as a backup to guarantee high availability. After you log on to the ApsaraDB for MongoDB console or call the SwitchDBInstanceHA operation to trigger a primary/secondary failover for a shard of a sharded cluster instance, ApsaraDB for MongoDB interchanges the roles of the primary and secondary nodes.

**Note:** 

-   You can trigger a primary/secondary failover only for replica set and sharded cluster instances, but not for standalone instances due to their single-node architecture.
-   You can trigger a primary/secondary failover only for shards in the normal running status.
-   After you trigger a primary/secondary failover for an instance, the instance may be disconnected for 30s once. We recommend that you perform this operation during off-peak hours and ensure that your applications can automatically re-establish a connection.

## Procedure {#section_qlp_fc5_cgb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Sharding Instances**.
4.  Locate the target instance and click its instance ID.
5.  In the Shard List area, locate the target shard and choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6708/155617836945431_en-US.png)** \> **Failover** in the Operation column.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6741/155617836913849_en-US.png)

    You can trigger a primary/secondary failover separately for each shard. The failover takes effect only for the current node and does not affect other shards of the same sharded cluster instance.

6.  In the Failover dialog box that appears, click **OK**.
7.  The failover takes about 1 minute. You can repeat the preceding procedure to trigger a primary/secondary failover for other shards of the same sharded cluster instance as required.

