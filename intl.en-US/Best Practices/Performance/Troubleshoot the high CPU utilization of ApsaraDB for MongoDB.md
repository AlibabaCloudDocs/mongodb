# Troubleshoot the high CPU utilization of ApsaraDB for MongoDB

When you use ApsaraDB for MongoDB, the CPU utilization may become excessively high or even approach 100%. The high CPU utilization slows down data read /write operations and affects normal business operations. This topic describes how to troubleshoot the high CPU utilization of ApsaraDB for MongoDB for your applications.

## Analyze running requests in ApsaraDB for MongoDB

1.  Connect to an ApsaraDB for MongoDB instance through the mongo shell.

    For more information, see [Connect to a standalone ApsaraDB for MongoDB instance by using the mongo shell](/intl.en-US/Quick Start/Connect to an instance/Connect to a standalone ApsaraDB for MongoDB instance by using the mongo shell.md), [Connect to a replica set instance by using the mongo shell](/intl.en-US/Quick Start/Connect to an instance/Connect to a replica set instance by using the mongo shell.md), and [Connect to a sharded cluster instance by using the mongo shell](/intl.en-US/Quick Start/Connect to an instance/Connect to a sharded cluster instance by using the mongo shell.md).

2.  Run the `db.currentOp()` command to check running operations in ApsaraDB for MongoDB.

    Example of the command output:

    ```
    {
            "desc" : "conn632530",
            "threadId" : "140298196924160",
            "connectionId" : 632530,
            "client" : "11.192.159.236:57052",
            "active" : true,
            "opid" : 1008837885,
            "secs_running" : 0,
            "microsecs_running" : NumberLong(70),
            "op" : "update",
            "ns" : "mygame.players",
            "query" : {
                "uid" : NumberLong(31577677)
            },
            "numYields" : 0,
            "locks" : {
                "Global" : "w",
                "Database" : "w",
                "Collection" : "w"
            },
            ....
        },
    ```


The following table describes some fields.

|Field|Description|
|:----|:----------|
|client|The client that sent the request.|
|opid|The unique ID of the operation. **Note:** If necessary, you can run the `db.killOp(opid)` command to terminate an operation. |
|secs\_running|The duration that the operation has been running, in seconds. If this field returns a value that exceeds the defined threshold, check whether the request is appropriate.|
|microsecs\_running|The duration that the operation has been running, in microseconds. If this field returns a value that exceeds the defined threshold, check whether the request is appropriate.|
|ns|The collection of the operation.|
|op|The operation type, which is query, insert, update, or delete.|
|locks|The lock-related fields. For more information, see [Concurrency](https://docs.mongodb.com/manual/faq/concurrency/index.html). **Note:** For more information about the db.currentOp\(\) command, see [db.currentOp](https://docs.mongodb.com/manual/reference/method/db.currentOp/?spm=5176.100239.blogcont73389.12.K1pNOi). |

You can run the `db.currentOp()` command to check in-progress operations and analyze whether ApsaraDB for MongoDB is processing time-consuming requests. The CPU utilization is normal for your routine business. When O&M personnel log on to ApsaraDB for MongoDB to perform some operations that require a collection scan, the CPU utilization significantly increases and ApsaraDB for MongoDB responds slowly. In this case, you must check for long-running operations.

**Note:** If you find an abnormal request, you can obtain the operation ID \(specified by the opid field\) of such a request and run the `db.killOp(opid)` command to terminate this request.

For example, the CPU utilization of the relevant ApsaraDB for MongoDB instance immediately increases and remains high after your application starts running. If you cannot find any abnormal requests in the output of the `db.currentOp()` command, you can analyze slow requests in ApsaraDB for MongoDB.

## Analyze slow requests in ApsaraDB for MongoDB

ApsaraDB for MongoDB enables slow request profiling by default. ApsaraDB for MongoDB automatically records requested operations that have been running for longer than 100 ms in the system.profile collection of the relevant database.

1.  Connect to an ApsaraDB for MongoDB instance through the mongo shell.

    For more information, see [Connect to a standalone ApsaraDB for MongoDB instance by using the mongo shell](/intl.en-US/Quick Start/Connect to an instance/Connect to a standalone ApsaraDB for MongoDB instance by using the mongo shell.md), [Connect to a replica set instance by using the mongo shell](/intl.en-US/Quick Start/Connect to an instance/Connect to a replica set instance by using the mongo shell.md), and [Connect to a sharded cluster instance by using the mongo shell](/intl.en-US/Quick Start/Connect to an instance/Connect to a sharded cluster instance by using the mongo shell.md).

2.  Run the `use <database>` command to access a database.

    ```
    use mongodbtest
    ```

3.  Run the following command to check the slow request logs of the database:

    ```
    db.system.profile.find().pretty()
    ```

4.  Analyze the slow request logs to discover the cause of high CPU utilization in ApsaraDB for MongoDB.

    The following example shows a slow request log. For this request, ApsaraDB for MongoDB did not query data based on an index, but has run a collection scan and scanned 11,000,000 documents.

    ```
    {
            "op" : "query",
            "ns" : "123.testCollection",
            "command" : {
                    "find" : "testCollection",
                    "filter" : {
                            "name" : "zhangsan"
                    },
                    "$db" : "123"
            },
            "keysExamined" : 0,
            "docsExamined" : 11000000,
            "cursorExhausted" : true,
            "numYield" : 85977,
            "nreturned" : 0,
            "locks" : {
                    "Global" : {
                            "acquireCount" : {
                                    "r" : NumberLong(85978)
                            }
                    },
                    "Database" : {
                            "acquireCount" : {
                                    "r" : NumberLong(85978)
                            }
                    },
                    "Collection" : {
                            "acquireCount" : {
                                    "r" : NumberLong(85978)
                            }
                    }
            },
            "responseLength" : 232,
            "protocol" : "op_command",
            "millis" : 19428,
            "planSummary" : "COLLSCAN",
            "execStats" : {
                    "stage" : "COLLSCAN",
                    "filter" : {
                            "name" : {
                                    "$eq" : "zhangsan"
                            }
                    },
                    "nReturned" : 0,
                    "executionTimeMillisEstimate" : 18233,
                    "works" : 11000002,
                    "advanced" : 0,
                    "needTime" : 11000001,
                    "needYield" : 0,
                    "saveState" : 85977,
                    "restoreState" : 85977,
                    "isEOF" : 1,
                    "invalidates" : 0,
                    "direction" : "forward",
    ....in"
                    }
            ],
            "user" : "root@admin"
    }
    ```


For slow request logs, you must take note of the following items:

-   Collection scan \(keywords: COLLSCAN and docsExamined\)
    -   COLLSCAN indicates a collection scan.

        A collection scan for a request \(such as a query, update, or delete operation\) can cause a high CPU utilization. If you find a COLLSCAN keyword in slow request logs, your CPU resources may have been occupied by these slow requests.

        **Note:** If such slow requests are frequently submitted, we recommend that you create an index on queried fields to optimize query performance.

    -   The docsExamined field indicates the number of documents that ApsaraDB for MongoDB has scanned for a request. A larger value of this field indicates higher CPU overheads occupied by this request.
-   Inappropriate indexes \(keywords: IXSCAN and keysExamined\)

    **Note:**

    -   If you have too many indexes, the write and update performance is affected.
    -   If your application contains too many write operations, inappropriate indexes may affect the application performance.
    The keysExamined field indicates the number of index keys that ApsaraDB for MongoDB has scanned for a request that uses an index. A larger value of this field indicates higher CPU overheads occupied by this request.

    If you create an index that is inappropriate or matches a large amount of data, the index cannot reduce CPU overheads or accelerate the execution of a request.

    For example, for the data in a collection, the x field can be set only to 1 or 2, whereas the y field has a wider value range.

    ```
    { x: 1, y: 1 }
    { x: 1, y: 2 }
    { x: 1, y: 3 }
    ......
    { x: 1, y: 100000} 
    { x: 2, y: 1 }
    { x: 2, y: 2 }
    { x: 2, y: 3 }
    ......
    { x: 1, y: 100000}
    ```

    To query data \{ x: 1, y: 2 \}, you can create an index.

    ```
    db.createIndex( {x: 1} ) // This index is inappropriate because a large amount of data has the same value of the x field.
    db.createIndex( {x: 1, y: 1} ) // This index is inappropriate because a large amount of data has the same value of the x field.
    db.createIndex( {y: 1 } ) // This index is appropriate because a small amount of data has the same value of the y field.
    db.createIndex( {y: 1, x: 1 } ) // This index is appropriate because a small amount of data has the same value of the y field.
    ```

    For the difference between indexes \{y: 1\} and \{y: 1, x: 1\}, see [Design Principles of MongoDB Indexes](https://yq.aliyun.com/articles/33726) and [Compound Indexes](https://docs.mongodb.com/manual/core/index-compound/).

-   Sorting of a large amount of data \(keywords: SORT and hasSortStage\)

    The value of the hasSortStage field is true in the system.profile collection when a query cannot use the sort order in the index to return the requested sorted results. In this case, ApsaraDB for MongoDB must sort the query results. Considering that a sort operation causes a high CPU utilization, you can create an index on frequently sorted fields to optimize sorting performance.

    **Note:** If you find the SORT keyword in the system.profile collection, you can use an index to optimize sorting performance.


Other operations such as index creation and aggregation \(a combination of traverse, query, update, and sort\) may also cause a high CPU utilization. You can also use the preceding troubleshooting methods. For more information about profiling, see [Database Profiler](https://docs.mongodb.com/manual/tutorial/manage-the-database-profiler/).

## Assess service capabilities

After you analyze and optimize running requests and slow requests in ApsaraDB for MongoDB, all requests efficiently use indexes and the query performance of ApsaraDB for MongoDB is optimized.

If CPU resources are still fully occupied during business operations, the maximum capabilities of your instances may have reached. In this case, you can view the monitoring information to analyze the resource usage of instances. You can also check whether current instances satisfy the performance and capability requirements in your business scenarios. For more information, see [View monitoring information](/intl.en-US/User Guide/Monitoring and alerting/View monitoring information.md).

To upgrade instances, you can follow the instructions in [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md) or [Change the number of nodes for a replica set instance](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Change the number of nodes for a replica set instance.md).

