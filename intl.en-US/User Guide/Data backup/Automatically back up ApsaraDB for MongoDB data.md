# Automatically back up ApsaraDB for MongoDB data {#concept_gs1_qrp_dgb .concept}

ApsaraDB for MongoDB automatically backs up data according to the default backup policy. You can also set a backup policy based on business requirements to automatically back up data for your ApsaraDB for MongoDB instances as required.

## Notes {#section_qzv_nsp_dgb .section}

-   ApsaraDB for MongoDB stores its generated backup files in [OSS](https://www.alibabacloud.com/help/doc-detail/31817.htm) to free up the storage space of ApsaraDB for MongoDB instances.
-   The backup method for standalone instances is fixed to [snapshot backup](intl.en-US/User Guide/Data backup/Manually back up ApsaraDB for MongoDB data.md#ul_iw5_lcp_dgb), which affects their I/O performance in the backup process.
-   The backup method for replica set and sharded cluster instances is [physical backup](intl.en-US/User Guide/Data backup/Manually back up ApsaraDB for MongoDB data.md#ul_iw5_lcp_dgb).

    **Note:** A physical backup is carried out on the hidden secondary node of an ApsaraDB for MongoDB instance. Therefore, it does not affect the I/O performance of the primary and secondary nodes. It may take a long time to back up a large amount of data. You need to wait patiently.


## Set an automatic backup policy {#section_msc_bsp_dgb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, click **Backup and Recovery**.
6.  Click **Backup Settings**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6721/155617973637422_en-US.png)

7.  In the Backup Settings dialog box that appears, set related parameters.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6721/155617973634383_en-US.png)

    |Parameter|Description|
    |:--------|:----------|
    |**Retention Days**|The number of days for keeping backup data. It is fixed to seven days.|
    |**Backup Time**|The backup time in units of hours. You can set any time as required. We recommend that you back up data during off-peak hours.|
    |**Day of Week**|The backup cycle. You can select one or more days in a week.|

8.  After setting the preceding parameters, click **OK**.

