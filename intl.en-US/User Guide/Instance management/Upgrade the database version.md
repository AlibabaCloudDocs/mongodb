# Upgrade the database version {#concept_ut5_fp4_fgb .concept}

ApsaraDB for MongoDB supports MongoDB 3.2, MongoDB 3.4, and MongoDB 4.0. You can upgrade the database version for an instance in the ApsaraDB for MongoDB console.

## Database versions {#section_vqd_qs4_fgb .section}

For more information, see [Versions and storage engines](../../../../intl.en-US/Product Introduction/Versions and storage engines.md#).

## Notes {#section_ejg_lp4_fgb .section}

-   Standalone instances support only MongoDB 3.4 and cannot be upgraded to MongoDB 4.0.
-   After upgrading the database version for an instance, you cannot downgrade the upgraded version.
-   An upgrade of the database version can last for some time depending on the data size of the database to be upgraded. You need to set the upgrade time in advance based on business requirements.
-   Because instances are automatically restarted twice or three times in the upgrade process, you need to upgrade the database version during off-peak hours.
-   If you use a connection string URI to connect your applications to an instance, the instance may be disconnected intermittently when it is being restarted. You need to ensure that your applications can automatically re-establish a connection.
-   The balancer of a sharded cluster instance is disabled during an upgrade and enabled again after the upgrade.

## Procedure {#section_ycp_gp4_fgb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the Basic Information area, click **Upgrade Database Version** to select the target database version.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6742/155617086121044_en-US.png)

6.  In the Upgrade Database Version dialog box that appears, click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6742/155617086121045_en-US.png)

    The instance enters the **Upgrading Version** status. The database version is successfully upgraded when the instance status changes to **Running**.


