# Set the monitoring granularity {#concept_wqs_2cz_q2b .concept}

ApsaraDB for MongoDB provides an optional monitoring granularity setting feature for you to set a finer granularity for collecting routine monitoring data and correctly locating O&M problems.

## Notes {#section_al4_pcz_q2b .section}

-   Standalone instances do not support this feature.
-   The database version of ApsaraDB for MongoDB instances must be MongoDB 3.4 \(upgraded to the latest minor database version\) or MongoDB 4.0.

    **Note:** The monitoring granularity of every second depends on the latest minor database version of ApsaraDB for MongoDB 3.4. The latest minor database version is compatible with all earlier minor database versions.

    -   ApsaraDB for MongoDB instances whose database version is MongoDB 3.2 do not support the monitoring granularity of every second. You need to upgrade their database version to MongoDB 3.4 to use this feature. For more information, see [Upgrade the database version](intl.en-US/User Guide/Instance management/Upgrade the database version.md#).
    -   For ApsaraDB for MongoDB instances created **after December 5, 2017** with the database version of MongoDB 3.4, you can directly set the monitoring granularity to every second. All metrics take effect immediately.
    -   For ApsaraDB for MongoDB instances created **before December 5, 2017** with the database version of MongoDB 3.4, if they have been restarted once since December 5, 2017, they can be automatically upgraded to the latest minor database version. If they have never been restarted since December 5, 2017, you need to restart them during off-peak hours. All metrics take effect after their restart.
    -   Currently, ApsaraDB for MongoDB provides the monitoring granularity of every second free of charge.

|Metric|Every second|Every 300s|
|:-----|:-----------|:---------|
|Disk Space Usage|N/A|Supported in MongoDB 3.2, MongoDB 3.4, and MongoDB 4.0.|
|Disk Space Usage|
|CPU Usage|Supported in MongoDB 3.4 \(upgraded to the latest minor database version\) and MongoDB 4.0.|
|Memory Usage|
|IOPS Usage|
|Opcounters|
|Connections|
|Cursors|
|Network|
|GlobalLock|
|WiredTiger|

## Procedure {#section_wvn_scz_q2b .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, click **Monitoring Info**.
6.  On the Monitoring Info page that appears, click **Monitor Granularity Setting**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6735/15561766808599_en-US.png)

7.  In the Monitor Granularity Setting dialog box that appears, select a monitoring granularity.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6735/15561766808600_en-US.png)

8.  Click **OK**.

