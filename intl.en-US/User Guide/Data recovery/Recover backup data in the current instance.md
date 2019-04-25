# Recover backup data in the current instance {#concept_o3q_r3z_2ez .concept}

Data recovery can help you minimize the loss caused by database misoperations. ApsaraDB for MongoDB provides multiple recovery methods. This topic describes how to recover backup data in the current instance.

## Notes {#section_gn4_43g_yfb .section}

-   Currently, only three-node replica set instances support this feature.
-   If you recover backup data in the current instance, the original data of the current instance is overwritten and cannot be recovered. Therefore, you need to perform this operation with caution.
-   Considering high risks for recovering backup data in the current instance, we recommend that you create an instance based on a time point or backup to recover data. For more information, see [Create an instance based on a time point](intl.en-US/User Guide/Data recovery/Create an instance based on a time point.md#) and [Create an instance based on a backup](intl.en-US/User Guide/Data recovery/Create an instance based on a backup.md#) . After verifying the recovered data, use DTS to migrate data to the current instance.

## Procedure {#section_cp5_r3g_yfb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances**.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, click **Backup and Recovery**.
6.  On the Backup and Recovery page that appears, locate the target backup and choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6723/155618097113851_en-US.png)** \> **Data Recovery** in the Operation column.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6727/155618097213860_en-US.png)
7.  In the Recover Backup Instance dialog box that appears, click **OK**.
8.  The instance enters the **Restoring from Backup** status. You can click **Refresh** to update and check the instance status. The data is successfully recovered when the instance status changes to **Running**.

