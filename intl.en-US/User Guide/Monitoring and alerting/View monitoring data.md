# View monitoring data

The ApsaraDB for MongoDB console provides a wide range of performance monitoring data for you to check the running status of instances.

## Note

Take note of the following points about the monitoring data feature of ApsaraDB for MongoDB:

-   The monitoring data feature differs in the old and new ApsaraDB for MongoDB consoles. We recommend that you use the new ApsaraDB for MongoDB console to experience more features.
-   It is normal if you are using the new ApsaraDB for MongoDB console, but the collection frequency of monitoring data is 1 second or 300 seconds.
    -   Some existing instances inherit the original collection frequency value of monitoring data.
    -   A collection frequency value of monitoring data has been specified for the instance in the old MongoDB management console. For more information, see [Set the monitoring granularity](/intl.en-US/User Guide/Monitoring and alerting/Set the monitoring granularity.md).
-   It is normal if you are using the old ApsaraDB for MongoDB console, but the collection frequency of monitoring data is 60 seconds. This indicates that this instance was created after the global collection frequency of monitoring data changed to 60 seconds. For more information, see [Notice on changing the monitoring data collection interval to 60 seconds as November 19, 2020](/intl.en-US/Product Notification/Notice on changing the monitoring data collection interval to 60 seconds as November
         19, 2020.md).

## Precautions

-   When you receive an alert message from Alibaba Cloud, such as a message indicating that the CPU utilization of your instance exceeds 80%, you can view monitoring data of the instance on ApsaraDB for MongoDB console to troubleshoot the issue. You can filter the nodes of the instance to check the status of each node and locate the node where the issue occurs.
-   Monitoring data is retained for up to seven days. You cannot view the monitoring data that was generated seven days ago.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, **Sharded Cluster Instances**, or **Serverless Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Monitoring Data**.

6.  View monitoring data based on instance types:

    **Note:** By default, the Monitoring Data page displays the monitoring data of the last day. You can also select a time range to view historical monitoring data.

    -   Standalone instances: You can only view the monitoring data of primary nodes.
    -   Replica set instances: You can view the monitoring data about primary or secondary nodes by selecting a node from the drop-down list in the upper part of the Monitoring Data page.

        ![Monitoring data of a replica set instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4345298951/p67534.png)

    -   Sharded cluster instances: You can view the monitoring data about mongos, shard, or Configserver nodes by selecting a node from the drop-down list in the upper part of the Monitoring Data page.

        **Note:** Mongos nodes have IDs prefixed with **s-**. Shard nodes have IDs prefixed with **d-**. ConfigServer nodes have IDs suffixed with **-cs**.

        ![Monitoring data of a sharded cluster instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4345298951/p67540.png)


## Metrics

|Metric|Description|
|:-----|:----------|
|CPU Utilization Percentage|cpu\_usage: the CPU utilization of the instance.|
|Memory Usage Percentage|mem\_usage: the memory usage of the instance.|
|IOPS Usage|The input/output operations per second \(IOPS\) of the instance. The following items are included: -   data\_iops: the IOPS of the data disk.
-   log\_iops: the IOPS of the log disk. |
|IOPS Usage Percentage|The percentage of the IOPS used by the instance to the maximum IOPS allowed.|
|Disk Usage|The total disk space used by the instance. The following items are included: -   ins\_size: the total space used.
-   data\_size: the space used on the data disk.
-   log\_size: the space used on the log disk. |
|Disk Usage Percentage|disk\_usage: the ratio of the total disk space used by the instance to the maximum disk space that can be used|
|Operation QPS|The queries per second \(QPS\) of the instance. The following items are included: -   The number of insert operations.
-   The number of query operations.
-   The number of delete operations.
-   The number of update operations.
-   The number of getmore operations.
-   The number of command operations. |
|Connections|current\_conn: the number of current connections to the instance.|
|cursors|The number of cursors used by the instance. The following items are included: -   total\_open: the number of cursors that are opened.
-   timed\_out: the number of cursors that timed out. |
|Network Traffic|The network traffic of the instance. The following items are included: -   bytes\_in: the inbound network traffic.
-   bytes\_out: the outbound network traffic.
-   num\_requests: the number of requests that are processed. |
|Global Lock Waiting Queues|The length of the queues that are waiting for global locks for the instance. The following items are included: -   gl\_cq\_readers: the length of the queue that is waiting for global read locks.
-   gl\_cq\_writers: the length of the queue that is waiting for global write locks.
-   gl\_cq\_total: the length of the queue that is waiting for both global read and write locks. |
|WiredTiger|The cache metrics of the WiredTiger engine used by the instance. The following items are included: -   bytes\_read\_into\_cache: the amount of data that is read into the cache.
-   bytes\_written\_from\_cache: the amount of data that is written from the cache to the disk.
-   maximum\_bytes\_configured: the size of the maximum available disk space that is configured. |
|Primary/Secondary Replication Latency|repl\_lag: the latency in data synchronization between the primary node and secondary nodes of the instance.|
|WT Request Queues|The number of concurrent requests that are being handled and the remaining number of concurrent requests that can be handled. The following items are included: -   write\_concurrent\_trans\_out: the number of concurrent write requests that are being handled.
-   read\_concurrent\_trans\_out: the number of concurrent read requests that are being handled.
-   write\_concurrent\_trans\_available: the remaining number of concurrent write requests that can be handled.
-   read\_concurrent\_trans\_available: the remaining number of concurrent read requests that can be handled. |
|IO Latency|iocheck\_cost: the latency of I/O operations, indicating the I/O response performance. **Note:** This metric is applicable only to replica set instances. |

