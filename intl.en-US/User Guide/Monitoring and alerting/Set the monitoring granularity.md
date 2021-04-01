# Set the monitoring granularity

ApsaraDB for MongoDB allows you to set the monitoring granularity to 1 second or 300 seconds, that is, collecting monitoring data once every second or 300 seconds, based on your business needs.

## Prerequisites

-   A replica set or sharded cluster instance is used.
-   The database version of the ApsaraDB for MongoDB instance is MongoDB 3.4, 4.0, or 4.2. If the database version is earlier than MongoDB 3.4, you can upgrade the database version. For more information, see [Upgrade MongoDB versions](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md).

## Billing

Currently, ApsaraDB for MongoDB allows you to collect monitoring data at the finest granularity of 1 second free of charge.

## Important notes

The 1 second monitoring granularity is only available in the latest minor version of ApsaraDB for MongoDB version 3.4. The latest minor version of version 3.4 is compatible with all earlier minor versions.

-   An ApsaraDB for MongoDB 3.4 instance created before December 5, 2017 will be automatically upgraded to the latest minor version of version 3.4 available if you have restarted the instance after the specified date. We recommend that you restart your instances during off-peak periods. The monitoring granularity will take effect for all metrics after restart.
-   You can set the monitoring granularity to 1 second for an ApsaraDB for MongoDB 3.4 instance created after December 5, 2017. The monitoring granularity takes effect for all metrics immediately.

## Monitoring granularity available for each metric

|Metric|Once every second|Once every 300 seconds|
|:-----|:----------------|:---------------------|
|Disk space usage|Not supported|Supported by all versions|
|Used disk space|
|CPU usage|Supported by version 4.2, version 4.0, and the latest minor version of version 3.4|
|Memory usage|
|IOPS usage|
|opcounters|
|connections|
|cursors|
|network|
|globalLock|
|wiredTiger|

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Monitoring Info**.

6.  On the **Monitoring Info** page that appears, click **Monitor Granularity Setting**.

7.  In the **Monitor Granularity Setting** pane that appears on the right side, set the monitoring granularity.

8.  Click **OK**.


