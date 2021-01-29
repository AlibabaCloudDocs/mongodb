# View monitoring information

The ApsaraDB for MongoDB console provides a wide range of performance monitoring information for you to check the running status of instances.

## Precautions

-   When you receive an alert message from Alibaba Cloud, such as a message indicating that the CPU utilization of your instance exceeds 80%, you can view monitoring information about the instance on ApsaraDB for MongoDB console to troubleshoot the issue. You can filter the nodes of the instance to check the status of each node and locate the node where the issue occurs.
-   Monitoring information is retained for up to seven days. You cannot view the monitoring information that was generated seven days ago.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, **Sharded Cluster Instances**, or **Serverless Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Monitoring Info**.

6.  View monitoring information based on instance types:

    **Note:** By default, the Monitoring Info page displays the monitoring information of the last day. You can also select a time range to view historical monitoring information.

    -   Standalone instances: You can only view the monitoring information about primary nodes.
    -   Replica set instances: You can view the monitoring information about primary or secondary nodes by selecting a node from the drop-down list in the upper part of the Monitoring Info page.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4345298951/p67534.png)

    -   Sharded cluster instances: You can view the monitoring information about mongos, shard, or ConfigServer nodes by selecting a node from the drop-down list in the upper part of the Monitoring Info page.

        **Note:** Mongos nodes have IDs prefixed with **s-**. Shard nodes have IDs prefixed with **d-**. ConfigServer nodes have IDs suffixed with **-cs**.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4345298951/p67540.png)


## Performance metrics

|Performance metric|Description|
|:-----------------|:----------|
|CPU Utilization Percentage|cpu\_usage: the CPU utilization of the instance.|
|Memory Usage Percentage|mem\_usage: the memory usage of the instance.|
|IOPS Usage|The input/output operations per second \(IOPS\) of the instance. The following items are included: -   data\_iops: the IOPS of the data disk.
-   log\_iops: the IOPS of the log disk. |
|IOPS Usage Percentage|The percentage of the IOPS used by the instance to the maximum IOPS allowed.|
|Disk Usage|The total disk space used by the instance. The following items are included: -   ins\_size: the total space used.
-   data\_size: the space used by the data disk.
-   log\_size: the space used on the log disk. |
|Disk Usage Percentage|disk\_usage: the ratio of the total disk space used by the instance to the maximum disk space that can be used.|
|Opcounters|The queries per second \(QPS\) of the instance. The following items are included: -   The number of insert operations.
-   The number of query operations.
-   The number of delete operations.
-   The number of update operations.
-   The number of getmore operations.
-   The number of command operations. |
|Connections|The current number of connections to the instance.|
|Cursors|The number of cursors used by the instance. The following items are included: -   total\_open: the number of cursors that are opened.
-   timed\_out: the number of cursors that timed out. |
|Network|The network traffic of the instance. The following items are included: -   bytes\_in: the inbound network traffic.
-   bytes\_out: the outbound network traffic.
-   num\_requests: the number of requests that are processed. |
|Global Lock|The length of the queues that are waiting for global locks for the instance. The following items are included: -   gl\_cq\_readers: the length of the queue that is waiting for global read locks.
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
|IO Latency|iocheck\_cost: the latency of I/O operations, indicating the I/O response performance.|

