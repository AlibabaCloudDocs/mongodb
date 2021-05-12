# Troubleshoot high CPU utilization on an ApsaraDB for MongoDB instance

CPU utilization is a key metric to monitor an ApsaraDB for MongoDB instance. If an ApsaraDB for MongoDB instance experiences high CPU utilization, the instance becomes unavailable. This topic describes how to view the CPU utilization on an ApsaraDB for MongoDB instance and troubleshoot high CPU utilization.

## View CPU utilization on an instance

For a sharded cluster instance, the CPU utilization on each shard node is the same as that on a replica set instance. The Configserver node is immune to most CPU bottlenecks because it only stores configuration metadata. The CPU utilization on mongos nodes is affected by aggregate result sets and the number of concurrent requests.

For a replica set instance, you can use the following methods to view the CPU utilization.

-   View CPU utilization in monitoring charts

    A replica set instance consists of multiple node roles. Each node role can correspond to one or more physical nodes. ApsaraDB for MongoDB allows you to use primary, secondary, and read-only nodes.

    On the **Monitoring Info** page of a replica set instance in the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/), select a node role and view the CPU utilization on the corresponding node in monitoring charts.

    **Note:** CPU utilization is affected by the instance specifications. For example, if an instance is equipped with 8 CPU cores and 16 GB memory and has a CPU utilization of 100%, the 8 CPU cores are exhausted. In this example, the CPU utilization is displayed as 100% instead of 800%.

    Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/). Find the desired instance and click the instance ID. In the left-side navigation pane of the page that appears, choose **CloudDBA** \> **Performance** and view the CPU utilization on an ApsaraDB for MongoDB instance in monitoring charts.

-   View CPU utilization by running commands

    In the ApsaraDB for MongoDB console, you cannot separately view the CPU utilization in the user and kernel states. In some cases, you can roughly identify the possible cause of high CPU utilization in the user and kernel states based on previous common causes.

    -   High CPU utilization in the user state lies on database-level statements in most cases.
    -   High CPU utilization in the kernel state lies on MongoDB in most cases.
    To separately view the CPU utilization on an instance in the user and kernel states, run the `db.serverStatus().systemInfo` command. A response similar to the following one is returned:

    ```
    {
        "user time us":NumberLong(1873234),
        "system time us":NumberLong(0),
        "user cpu usage per 10 thousand":NumberLong(18713),
        "system cpu usage per 10 thousand":NumberLong(0),
        "block direct write operations":NumberLong("114766377048"),
    ......
    }
    ```

-   View and terminate active sessions

    The surging sessions of an instance in the Running state may consume 100% CPU resources. In this case, high CPU utilization is possibly caused by the changes of business traffic. Possible causes include scans involving large numbers of documents, data sorting and aggregation, and surges in business traffic. You can use one of the following methods to view the active sessions:

    -   In the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/), click the ID of an instance. In the left-side navigation pane, choose **CloudDBA** \> **Session**. On the page that appears, view current active sessions and analyze the query operations that are not completed within the expected execution period.
    -   To view and analyze details of active sessions, run the db.currentOp\(\) command provided by MongoDB. If necessary, run the db.killOp\(\) command to actively terminate slow queries that are not completed within the expected execution period. For more information, see [db.currentOp\(\)](https://docs.mongodb.com/manual/reference/method/db.currentOp/) and [db.killOp\(\)](https://docs.mongodb.com/manual/reference/method/db.killOp/).
-   Record slow query logs and audit logs

    ApsaraDB for MongoDB allows you to use the following profiling levels:

    -   Profiling is disabled and no data is collected.
    -   Profiling is enabled for all requests. The execution data of all requests is recorded in the system.profile collection.
    -   Profiling is enabled for slow queries. Queries that take longer than the specified threshold are recorded in the system.profile collection.
    In the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/), find the desired instance and click the instance ID. In the left-side navigation pane of the page that appears, choose **Parameters** \> **Parameter List**. Click Modify Parameter and set the operationProfiling.mode and operationProfiling.slowOpThresholdMs parameters. The operationProfiling.mode parameter specifies the profiling level. The operationProfiling.slowOpThresholdMs parameter specifies the threshold of slow queries.

    Choose **Logs** \> **Slow Query Logs**. On the page that appears, you can view slow query logs after profiling is enabled.

    For more information about profiling, visit [https://docs.mongodb.com/manual/tutorial/manage-the-database-profiler/](https://docs.mongodb.com/manual/tutorial/manage-the-database-profiler/).

    If you require more detailed auditing to troubleshoot problematic requests, you can enable audit logs in the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/). In the left-side navigation pane, choose **Data Security** \> **Audit Logs**. On the page that appears, click Enable Audit Logs.

    For more information, see [Enable the log audit feature](https://help.aliyun.com/document_detail/180836.html?spm=a2c4g.11186623.6.729.58173958efqDsi).


## Possible causes of high CPU utilization and optimization strategies

This section describes the common causes of high CPU utilization on an instance and the corresponding optimization policies.

-   Queries that need to scan large numbers of documents

    ApsaraDB for MongoDB supports multi-threading. If a single query requires to scan large numbers of documents, the thread in which the query is executed occupies CPU resources for a longer period of time. If the pending requests or the queries that require to scan large numbers of documents are in high concurrency, high CPU utilization occurs on the instance on which the queries are executed. The CPU utilization on an instance is positively related to the total number of scanned documents that the instance requires.

    Index optimization is the best solution to reduce the number of documents that a single query needs to scan. In the underlying architecture, MongoDB uses an index design similar to MySQL and provides richer categories and features over MySQL. Therefore, most index optimization policies that apply to MySQL also apply to MongoDB.

    Queries that often need to scan large numbers of documents are common in the following scenarios:

    -   Full table scan

        If the COLLSCAN keyword exists in the system.profile collection or runtime logs, a query results in a full table scan. You can optimize this query by adding indexes. If this method is unavailable, you must control the data volume of the table and the query execution frequency.

        For more information about query plans, visit [https://docs.mongodb.com/manual/reference/explain-results/](https://docs.mongodb.com/manual/reference/explain-results/) and [https://docs.mongodb.com/manual/reference/operator/meta/explain/](https://docs.mongodb.com/manual/reference/operator/meta/explain/).

    -   Index design and optimization

        In addition to full table scan, you must also focus on queries that are frequently executed and have a docsExamined parameter value greater than 1000. The docsExamined parameter indicates the number of documents that MongoDB examines. In addition to full table scan, the large number of examined documents may be caused by the following reasons:

        -   When multiple filter conditions are used, a compound index is not used or the principle of leftmost prefix matching is not satisfied.
        -   Indexes are not used for sorting.
        -   The query is complex or involves large numbers of aggregate operations, which can result in invalid parsing policies or indexes that cannot be optimized.
        -   The data selectivity of a data field is unbalanced with the selection frequency.
        For more information, see the following links:

        -   For information about the principles and usage of compound indexes, visit [https://docs.mongodb.com/manual/core/index-compound/](https://docs.mongodb.com/manual/core/index-compound/).
        -   For information about how to use indexes for sorting, visit [https://docs.mongodb.com/manual/tutorial/sort-results-with-indexes/](https://docs.mongodb.com/manual/tutorial/sort-results-with-indexes/).
        -   For more information about the Hint operator, visit [https://docs.mongodb.com/manual/reference/operator/meta/hint/](https://docs.mongodb.com/manual/reference/operator/meta/hint/) and [https://docs.mongodb.com/manual/reference/operator/meta/hint/](https://docs.mongodb.com/manual/reference/method/cursor.hint/).
        -   For information about how to ensure selectivity, visit [https://docs.mongodb.com/manual/tutorial/create-queries-that-ensure-selectivity/](https://docs.mongodb.com/manual/tutorial/create-queries-that-ensure-selectivity/).
-   Excessive concurrency

    In addition to query causes, high CPU utilization may be caused by excessive business concurrency. If the number of business requests is large and concurrency is high, you can use the following methods to add CPU cores:

    -   Scale up a single instance for more read and write workloads.
    -   Configure read/write splitting for replica sets or add read-only instances for the replica sets.
    -   Upgrade the problematic instance to a sharded cluster instance for linear scale-out.
    -   If mongos nodes consume all CPU resources, add mongos nodes and configure load balancing for mongos nodes.
    For more information, see [Change the configuration of a sharded cluster instance](https://help.aliyun.com/document_detail/128782.html), [Change the configuration of a standalone or replica set instance](https://help.aliyun.com/document_detail/129161.html), and [Change the number of nodes for a replica set instance](https://help.aliyun.com/document_detail/95286.html).


## Other possible causes

-   Frequent short-lived connections of MongoDB

    In versions later than MongoDB 3.X, the default identity authentication mechanism is SCRAM-SHA1 that requires CPU-intensive operations such as hash calculation. If short-lived connections are in high concurrency, hash calculation consumes multifold CPU resources and even exhausts CPU resources. In this case, runtime logs contain a large number of saslStart error messages.

    We recommend that you use persistent connections. To optimize PHP short-lived connections in high concurrency scenarios, ApsaraDB for MongoDB optimizes the method to rewrite built-in random functions at the kernel layer. This helps reduce the CPU utilization on an instance.

    On the **Database Connection** page of an instance in the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/), enable password-free access.

-   Time-to-live \(TTL\) indexes cause higher CPU utilization on a secondary node than the primary node.

    Since MongoDB 3.2, multi-threaded replication is supported. The rollback concurrency of oplogs is determined by the replWriterThreadCount parameter. The default value is 16. Secondary nodes do not handle business-critical read workloads. However, the CPU utilization on a secondary node may be higher than that on the primary node. For example, if you use TTL to delete data in a table when the data expires, the system can efficiently delete large amounts of data at a time based on the indexes on the time column. The system transforms the delete operation into multiple delete operations and then sends them to a secondary node. On the secondary node, the rollback of oplogs is less efficient. Multi-threaded rollback of oplogs may increase CPU utilization on the node. In this case, we recommend that you ignore high CPU utilization on the node.


