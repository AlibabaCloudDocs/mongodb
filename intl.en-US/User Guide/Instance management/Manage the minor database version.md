# Manage the minor database version {#concept_dqn_qnr_l2b .concept}

When ApsaraDB for MongoDB publishes a minor database version, you can log on to the ApsaraDB for MongoDB console to upgrade your ApsaraDB for MongoDB to the latest minor database version.

## Before you start {#section_nyg_smg_1fb .section}

During an upgrade of the minor database version, the system automatically fixes bugs in the old version. In addition, the latest minor database version also provides you with more new features. You can check the update content in [View the publish logs of the latest minor database version](#section_pxn_wrf_1fb).

Currently, only replica set and sharded cluster instances support an upgrade of the minor database version. Standalone instances do not support this upgrade.

During the upgrade of the minor database version, instances are restarted once. The upgrade is completed when instances are being restarted. We recommend that you upgrade the minor database version for instances during off-peak hours.

**Note:** If an instance has been upgraded to the latest minor database version, the console does not display **Upgrade** in the Specification Information area for the instance.

## View the minor database version {#section_xsz_mmf_1fb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the Specification Information area, view the current minor database version of the target instance.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/20146/155617049311187_en-US.png)


## Upgrade the minor database version {#section_uqf_2nf_1fb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the Specification Information area, click **Upgrade** to the right of the current minor database version.
6.  In the **Upgrade Minor Version** dialog box that appears, click **OK** to upgrade the current database to the latest minor database version.

## View the publish logs of the latest minor database version {#section_pxn_wrf_1fb .section}

During the upgrade of the minor database version, you can view the update content of the latest minor database version.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the Specification Information area, click **View Publish Log** to the right of the current minor database version to view the update content of the latest minor database version.

    **Note:** If an instance has been upgraded to the latest minor database version, the console does not display **View Publish Log** in the Specification Information area for the instance.


