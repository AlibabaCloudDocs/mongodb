# View the monitoring information {#concept_sn1_wh5_4fb .concept}

The ApsaraDB for MongoDB console provides a wide range of performance monitoring data for you to conveniently view and understand the running status of your instances.

## Procedure {#section_fs3_zh5_4fb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, click **Monitoring Info**.
6.  On the Monitoring Info page that appears, the monitoring data of the last 24 hours is displayed by default. You can also specify a time range to view the historical monitoring data.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6734/155617643437327_en-US.png)

    **Note:** 

    -   If the target instance is a replica set instance, you can select **Primary** or **Secondary** to view the monitoring information about the primary node or a secondary node.
    -   If the target instance is a sharded cluster instance, you can select **Mongos** or **Shard** to view the monitoring information about the selected node.

## Metrics {#section_pzq_135_4fb .section}

|Metric|Description|
|:-----|:----------|
|CPU Usage|The CPU usage of the instance.|
|Memory Usage|The memory usage of the instance.|
|IOPS Usage|The input/output operations per second \(IOPS\) of the instance, including:-   The IOPS on the data disk.
-   The IOPS on the log disk.

|
|IOPS Usage|The ratio of the IOPS of the instance to the maximum IOPS.|
|Disk Space Usage|The disk space usage of the instance, including:-   The total disk space usage.
-   The disk space usage on the data disk.
-   The disk space usage on the log disk.

|
|Disk Space Usage|The ratio of the total disk space usage of the instance to the maximum available disk space.|
|Opcounters|The queries per second \(QPS\) of operations on the instance, including:-   The number of insert operations.
-   The number of query operations.
-   The number of delete operations.
-   The number of update operations.
-   The number of getmore operations.
-   The number of commands.

|
|Connections|The current number of connections to the instance.|
|Cursors|The current number of cursors used by the instance, including:-   The number of currently opened cursors.
-   The number of timed-out cursors.

|
|Network|The network traffic of the instance, including:-   The inbound traffic.
-   The outbound traffic.
-   The number of processed requests.

|
|GlobalLock|The number of operations that are currently queued and waiting for the global lock, including:-   The number of operations queued waiting for the read lock.
-   The number of operations queued waiting for the write lock.
-   The total number of operations queued waiting for the global lock.

|
|WiredTiger|The statistics on the cache of the WiredTiger storage engine, including:-   The amount of data read into the cache.
-   The amount of data written from the cache.
-   The maximum configured size of the cache.

|

