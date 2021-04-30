# Set collection frequency of monitoring data

The old ApsaraDB for MongoDB console allows you to set the collection frequency of monitoring data to 1 second or 300 seconds based on your business needs. That means monitoring data is collected once every second or every 300 seconds.

## Note

It is normal if the collection frequency of monitoring data is 60 seconds. The reason is that the collection frequency of monitoring data of ApsaraDB for MongoDB has been changed to 60 seconds. This value cannot be modified. For more information, see [Notice on changing the monitoring data collection interval to 60 seconds as November 19, 2020](/intl.en-US/Product Notification/Notice on changing the monitoring data collection interval to 60 seconds as November
         19, 2020.md).

## Prerequisites

-   The old ApsaraDB for MongoDB console is used.
-   A replica set or sharded cluster instance is used.
-   The database version of the ApsaraDB for MongoDB instance is MongoDB 3.4, 4.0, or 4.2. If the database version is earlier than MongoDB 3.4, you can upgrade the database version. For more information, see [Upgrade MongoDB versions](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md).

## Billing

ApsaraDB for MongoDB allows you to collect monitoring data at the finest granularity of 1 second free of charge.

## Precautions

The 1 second collection frequency is only available in the latest minor version of MongoDB 3.4. The latest minor version of MongoDB 3.4 is compatible with all earlier minor versions.

-   A MongoDB 3.4 instance created before December 5, 2017 will be automatically upgraded to the latest minor version of MongoDB 3.4 available if you have restarted the instance after the specified date. We recommend that you restart your instances during off-peak periods. The collection frequency will take effect for all metrics after restart.
-   You can set the collection frequency to 1 second for MongoDB 3.4 created after December 5, 2017. The collection frequency takes effect for all metrics immediately.

## Collection frequency available for each metric

|Metric|Once every second|Once every 300 seconds|
|:-----|:----------------|:---------------------|
|Disk Usage Percentage|Not supported|Supported in all versions|
|Disk Usage|
|CPU Utilization Percentage|Supported in MongoDB 4.2, MongoDB 4.0, and the latest minor version of MongoDB 3.4|
|Memory Usage Percentage|
|IOPS Usage Percentage|
|Opcounters|
|Connections|
|Cursors|
|Network|
|Global Lock|
|WiredTiger|

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Monitoring Data**.

6.  On the **Monitoring Data** page, click **Monitor Granularity Setting**.

7.  In the **Monitor Granularity Setting** pane, set a collection frequency value of monitoring data.

8.  Click **OK**.


