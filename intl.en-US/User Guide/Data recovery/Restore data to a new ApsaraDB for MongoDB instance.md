# Restore data to a new ApsaraDB for MongoDB instance

This topic describes how to restore one or more databases of an ApsaraDB for MongoDB instance to a new ApsaraDB for MongoDB instance by using a backup created at a specific point in time. This method is ideal for quick data restoration.

## Background information

Instances created after March 26, 2019 support the restoration of one or more databases. For information about when this feature will be available to instances created before March 26, 2019, follow the official website.

## Prerequisites

-   The instance is created after March 26, 2019.
-   The instance is located in the China \(Qingdao\), China \(Beijing\), China \(Zhangjiakou\), China \(Hohhot\), China \(Hangzhou\), China \(Shanghai\), China \(Shenzhen\), or Singapore \(Singapore\) region.
-   The instance is a replica set instance.
-   The MongoDB version of the instance is 3.4, 4.0, or 4.2.

    **Note:**

    -   If the MongoDB version of the instance is earlier than required versions, you must upgrade the database version. For more information, see [Upgrade MongoDB versions](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md).
    -   After the MongoDB version is upgraded, the backup files of the original version cannot be used to restore data of the new version.
-   The storage engine of the instance is WiredTiger.
-   The backup file list of the instance contains the backup files of the databases you want to restore.

## Precautions

-   You can restore databases only from physical backups.
-   The time required varies based on factors such as the data volume, task queue status, and network conditions. When the status of the new instance changes to **Running**, the restoration is complete.

## Billing

When you restore one or more databases, the system creates an instance and you are charged for the new instance. For more information, see [Billing items and pricing](/intl.en-US/Purchase Guide/Billing items and pricing.md).

**Note:** If you want to restore the databases to a pay-as-you-go instance, make sure that your account has sufficient balance.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Backup and Recovery**.

6.  On the **Backup and Recovery** page, click **Create Instance By Time Point**.

7.  In the Create Instance By Time Point panel, configure the following parameters.

    ![ApsaraDB for MongoDB data restoration from databases](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1545298951/p41591.png)

    |Parameter|Description|
    |:--------|:----------|
    |Select recovery time point|Select a point in time from which you want to restore data. You can select a time point from the last seven days. **Note:** The time you select must be earlier than the current time and later than the time when the source instance was created. |
    |Select databases to recover|    -   **All Databases**: If you select this option, all databases in the source instance are restored.
    -   **Select Databases**: If you select this option, only selected databases are restored.

You can directly select the databases you want to restore, or click **Enter Databases** to enter the names of the databases.

**Note:** If you want to restore more than one database, separate the database names with commas \(,\) when you enter them. |

8.  Click **OK**.

9.  On the instance buy page, select a billing method for the new instance.

    **Note:**

    -   Subscription: You must pay for the subscription when you create an instance. This method is more cost-effective than the pay-as-you-go method. We recommend that you select this method for long-term use. A longer subscription period enables a larger discount.
    -   Pay-as-you-go: You are billed on an hourly basis based on the used resources. We recommend that you select this billing method for short-term use. You can reduce costs by releasing your pay-as-you-go instance if it is no longer needed.
10. Configure the new instance. For more information, see [Create a replica set instance](/intl.en-US/Quick Start/Create an instance/Create a replica set instance.md).

    **Note:**

    -   You cannot change **Region**, **Database Version**, **Storage Engine**, or **Replication Factor** for the new instance.
    -   To make sure that the new instance has sufficient space for restoration, we recommend that you set the storage capacity larger than or equal to that of the source instance.
11. Click **Buy Now**.

12. On the Confirm Order page, read and select **ApsaraDB for MongoDB Agreement of Service**, and complete the payment.


