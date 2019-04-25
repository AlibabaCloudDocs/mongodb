# Manually back up ApsaraDB for MongoDB data {#concept_e1s_szs_qgb .concept}

You can set a backup policy to adjust the default backup settings of ApsaraDB for MongoDB to [automatically back up data](intl.en-US/User Guide/Data backup/Automatically back up ApsaraDB for MongoDB data.md#). Alternatively, you can manually back up ApsaraDB for MongoDB data.

## Notes {#section_cbl_mbp_dgb .section}

-   ApsaraDB for MongoDB stores its generated backup files in [OSS](https://www.alibabacloud.com/help/zh/doc-detail/31817.htm) to free up the storage space of ApsaraDB for MongoDB instances.
-   The backup method for standalone instances is fixed to snapshot backup, which affects their I/O performance in the backup process.
-   Replica set and sharded cluster instances support physical backup and logical backup.
-   A physical backup or logical backup is carried out on the hidden secondary node of an ApsaraDB for MongoDB instance. Therefore, it does not affect the I/O performance of the primary and secondary nodes. It may take a long time to back up a large amount of data. You need to wait patiently.

## Backup methods {#section_jmr_kcp_dgb .section}

-   Snapshot backup: Due to the special single-node architecture, the data of standalone instances is backed up in snapshots. A snapshot backup can keep the status of disk data at a specific time point.
-   Physical backup: Physical database files are backed up for ApsaraDB for MongoDB instances.
-   Logical backup: You can run a mongodump command to logically back up ApsaraDB for MongoDB data.

## Procedure {#section_w1s_ccp_dgb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, click Backup and Recovery. In the upper-right corner of the page that appears, click **Backup Instance**.
6.  In the Backup Instance dialog box that appears, select a backup method for **Backup Method**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6722/15561796677041_en-US.png)

7.  Click **OK**.

