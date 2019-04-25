# Optimize indexes {#concept_h14_ntz_xfb .concept}

During the use of ApsaraDB for MongoDB, query statements may run slowly or time out if you miss indexes or use incorrect indexes. In this case, the high CPU usage affects business. ApsaraDB for MongoDB provides an index optimization feature to detect slow queries caused by missing or incorrect indexes. This feature also chooses the optimal indexes for these slow queries to improve the performance of ApsaraDB for MongoDB.

## Constraints {#section_i2d_y3z_xfb .section}

-   Standalone instances do not support this feature.
-   Currently, you can enable index optimization only in the following regions: China \(Hangzhou\), China \(Shanghai\), China \(Shenzhen\), China \(Qingdao\), and China \(Beijing\).
-   Before enabling index optimization for an instance, you must enable [log auditing](intl.en-US/User Guide/Data security/Configure log auditing.md#).

## Rules for generating index optimization reports {#section_ach_fjz_xfb .section}

-   ApsaraDB for MongoDB automatically generates index optimization reports every day covering 0:00 to 24:00.

    **Note:** Index optimization reports are kept for seven days and automatically deleted after seven days.

-   You can specify a time range in the last seven days to analyze slow queries within the selected time range and generate index optimization reports as required.
-   Query statements whose execution time exceeds 100 ms are considered as slow queries.

## Procedure {#section_udg_jqz_xfb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, choose **CloudDBA** \> **Index Optimization**.
6.  Click **Custom Analysis**. The Custom Analysis dialog box appears.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65050/155617902333108_en-US.png)

    You can specify **Select Time Range** to view index optimization reports of the selected time range.

7.  On the list, click **View Detail** in the Operation column corresponding to an index optimization report to view the details of index diagnosis.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65050/155617902533109_en-US.png)

8.  In the Index Optimization Detail dialog box that appears, you can view the detailed information such as **Index Optimization** and **Merge Index Recommendations**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65050/155617902533110_en-US.png)


