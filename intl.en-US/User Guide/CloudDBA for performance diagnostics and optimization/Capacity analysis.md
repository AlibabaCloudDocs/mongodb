---
keyword: [Capacity analysis, Database tablespaces, Data Space, Storage Trend, Tablespaces]
---

# Capacity analysis

ApsaraDB for MongoDB enables the capacity analysis feature. This topic describes how to analyze the storage capacity of your ApsaraDB for MongoDB instances. You can view the information about the **storage overview**, **exceptions**, **storage trend**, **tablespaces**, and **data spaces**. This allows you to detect and resolve storage exceptions in the database to ensure database stability.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, choose **CloudDBA** \> **Storage Analysis**.

    ![Capacity analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6645298951/p70129.png)

6.  In the upper-right corner, click **Re-analyze**. Then, wait until the analysis is complete.

7.  On the **Storage Overview** or **Data Space** tab, view the analysis results.

    ![Storage Overview and Data Space](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2447559951/p70184.png)

    For more information about Storage Overview, see [Storage Overview](#section_3gx_g72_iq3).

    For more information about Data Space, see [Data Space](#section_afx_vbs_aos).


## Storage Overview

On the Storage Overview tab, you can view information in the **Storage**, **Exceptions**, **Storage Trend**, and **Tablespaces** sections.

-   **Storage**

    ![Storage](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2447559951/p70134.png)

    |Item|Description|
    |----|-----------|
    |**Exception**|The number of detected storage exceptions. ApsaraDB for MongoDB can detect the following types of exceptions:     -   More than 90% of the storage capacity is used.
    -   The total physical storage is unavailable in seven days.
    -   The number of indexes in a collection exceeds 10. |
    |**Avg Daily Increase in Last Week**|The average daily increase of storage usage over the last seven days. Formula: \(Storage usage at the time of collection - Storage usage seven days ago\)/7. **Note:**

    -   The increase speed is the average value during the seven days before the collection time.
    -   This parameter is only used as a reference for scenarios in which the traffic remains stable. Abrupt storage changes caused by batch imports, deletion of historical data, instance migration, or instance re-creation affect the accuracy of the data. |
    |**Available Days of Storage**|The estimated number of days during which storage space is available. Formula: Size of available storage space/Average daily increase over the last week. **Note:**

    -   90+ indicates that the storage space is sufficient for more than 90 days of usage.
    -   This parameter is used only as a reference for scenarios in which the traffic remains stable. Abrupt storage changes caused by batch imports, deletion of historical data, instance migration, or instance re-creation affect the accuracy of the data. |
    |**Used Storage**|The size of used storage space in contrast to the total size of storage space.|

-   **Exceptions**

    Information about detected storage exceptions. You can resolve the exceptions based on the information in this section.

    ![Exceptions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2447559951/p70135.png)

-   **Storage Trend**

    Changes in storage usage over the last week, such as changes in the **used storage space**, **data space**, and **log space**.

    ![Storage Trend](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2447559951/p70137.png)

-   **Tablespaces**

    Information about all tables, such as the database name, storage engine, and collection storage.

    ![Tablespaces](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3447559951/p70139.png)

    **Note:** You can click a collection name to view its indexes.


## Data Space

On the Data Space tab, you can view the total storage capacity and tablespace information of each database.

**Note:**

-   You can click the name of a data space to view its tablespace information.
-   You can click a collection name to view its indexes.

![Data Space](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3447559951/p70142.png)

