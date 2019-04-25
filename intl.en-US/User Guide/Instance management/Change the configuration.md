# Change the configuration {#concept_yzz_dgl_j2b .concept}

If the configuration of an instance cannot meet the performance requirements of your applications or is higher than required, you can change the configuration for this instance.

## Constraints {#section_f2z_5k1_wfb .section}

Due to the differences among the standalone, replica set, and sharded cluster architectures, you cannot change the architecture of an instance.

## Fees {#section_hzx_dml_cfb .section}

You can upgrade or downgrade the configuration for all ApsaraDB for MongoDB instances. The fees of an instance may change if its configuration is changed. For more information, see [Billing items and pricing](../intl.en-US/Purchase guide/Billing items and pricing.md#).

## Effective time {#section_mdf_jsm_cfb .section}

-   **Standalone or replica set instance**: When changing the configuration, you can set the effective time for the new configuration.
    -   **Immediately after data migration**: After a configuration change process, the instance immediately enters the **Changing Configuration** status. The configuration is successfully changed when the instance status changes to **Running**.

        During some configuration upgrades, the target instance may be disconnected for less than 30s once or twice. You can set the effective time for the configuration change as required to avoid an impact on business.

    -   **During the maintenance period**: You can set the effective time for the configuration change within a specified period. For more information, see [Specify a maintenance period](intl.en-US/User Guide/Instance management/Specify a maintenance period.md#).

        **Note:** If an instance is not disconnected during the configuration change, the configuration change can immediately take effect regardless of whether you have set the effective time.

-   **Sharded cluster instance**: You cannot set the effective time for the configuration change. After a configuration change process, the instance immediately enters the **Changing Configuration** status. The configuration is successfully changed when the instance status changes to **Running**.

**Note:** When an instance is in the **Changing Configuration** status, you cannot perform most database, account, and network operations for this instance. The completion time of the configuration change depends on various factors such as the network, task queue, and data amount. We recommend that you change the configuration of an instance during off-peak hours or ensure that your applications can automatically re-establish a connection.

## Change the configuration of a standalone or replica set instance {#section_in1_njl_j2b .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  If the target instance is a Pay-As-You-Go instance:

    Choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6660/155616887313206_en-US.png)** \> **Change Configuration** in the Operation column corresponding to the target instance.

    You can also click the target instance ID or choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6660/155616887313206_en-US.png)** \> **Manage** in the Operation column corresponding to the target instance. On the Basic Information page that appears, click **Change Configuration**.

4.  If the target instance is a subscription-based instance:
    1.  Click the target instance ID or choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6660/155616887313206_en-US.png)** \> **Manage** in the Operation column corresponding to the target instance.
    2.  On the Basic Information page that appears, click **Upgrade** or **Downgrade**.

        You can also choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6660/155616887313206_en-US.png)** \> **Upgrade** in the Operation column corresponding to the target instance.

5.  On the Update page, specify **Specification** and **Storage Space** for the target instance.

    **Note:** 

    -   You cannot downgrade the **storage space** for a standalone instance whose billing method is Pay-As-You-Go.
    -   You cannot downgrade the **storage space** for a standalone or replica set instance whose billing method is subscription.
    For more information about the specifications and storage space for instances, see [Instance specifications](../intl.en-US/Product Introduction/Instance specifications.md#).

    On the Update page, you can also set the effective time for the configuration change.

6.  Select **ApsaraDB for MongoDB Agreement of Service** and follow the instructions to complete the configuration change process.

## Add nodes to change the configuration of a sharded cluster instance {#section_lzh_wn4_1fb .section}

When adding a mongos node for a sharded cluster instance, you can specify **Specification** for the mongos node to change the configuration of the instance.

When adding a shard for a sharded cluster instance, you can specify **Specification** and **Storage Space** for the shard to change the configuration of the instance.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  Click the target sharded cluster instance ID.

    You can also choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6660/155616887313206_en-US.png)** \> **Manage** in the Operation column corresponding to the target instance.

4.  To add a mongos node, click **Add Mongos** on the Basic Information page.
5.  On the Add Mongos page that appears, specify **Specification** for the new mongos node.
6.  To add a shard, click **Add Shard** on the Basic Information page.
7.  On the Add Shard page that appears, specify **Specification** and **Storage Space** for the new shard.

    For more information about the specifications and storage space for instances, see [Instance specifications](../intl.en-US/Product Introduction/Instance specifications.md#).

8.  Select **ApsaraDB for MongoDB Agreement of Service** and follow the instructions to complete the configuration change process.

## Change the configuration of existing nodes to change the configuration of a sharded cluster instance {#section_vnm_yrl_cfb .section}

You can change the specifications of existing mongos nodes or the specifications and storage space of existing shards to change the configuration of a sharded cluster instance.

**Note:** When changing the configuration of a sharded cluster instance, you can only add nodes or change the specifications and storage space of existing nodes. You cannot delete nodes or change configuration items other than the specifications and storage space of existing nodes.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  Click the target sharded cluster instance ID.

    You can also choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6660/155616887313206_en-US.png)** \> **Manage** in the Operation column corresponding to the target instance.

4.  To change the configuration of an existing mongos node, do as follows: In the Mongos List area of the Basic Information page, choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6660/155616887313206_en-US.png)** \> **Change Configuration** in the Operation column corresponding to the target mongos node.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6706/155616887421057_en-US.png)

5.  On the Change Configuration Mongos page that appears, specify **Specification** for the mongos node.
6.  To change the configuration of an existing shard, do as follows: In the Shard List area of the Basic Information page, choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6660/155616887313206_en-US.png)** \> **Change Configuration** in the Operation column corresponding to the target shard.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6706/155616887421056_en-US.png)

7.  On the Change Configuration Shard page that appears, specify **Specification** and **Storage Space** for the shard.

    **Note:** When changing the configuration of an existing shard for a sharded cluster instance whose billing method is subscription, you cannot downgrade the storage space of the shard.

    For more information about the specifications and storage space for instances, see [Instance specifications](../intl.en-US/Product Introduction/Instance specifications.md#)

8.  Select **ApsaraDB for MongoDB Agreement of Service** and follow the instructions to complete the configuration change process.

