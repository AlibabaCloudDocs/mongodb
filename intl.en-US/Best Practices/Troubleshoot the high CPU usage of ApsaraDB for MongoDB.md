# Troubleshoot the high CPU usage of ApsaraDB for MongoDB {#concept_62224_zh .concept}

When you use ApsaraDB for MongoDB, its CPU usage may become excessively high or even close to 100%. The high CPU usage not only slows down data read and write operations, but also affects normal business operations. This topic describes how to troubleshoot the high CPU usage of ApsaraDB for MongoDB for your applications.

## Analyze in-progress requests in ApsaraDB for MongoDB {#section_gdv_ltv_1gb .section}

1.  Connect to an ApsaraDB for MongoDB instance through the mongo shell.
    -   [Connect to a standalone instance through the mongo shell](../../../../intl.en-US/Quick Start for Standalone/Connect to an instance/Connect to ApsaraDB for MongoDB through the mongo shell.md#)
    -   [Connect to a replica set instance through the mongo shell](../../../../intl.en-US/Quick Start for Replica Set/Connect to an instance/Connect to ApsaraDB for MongoDB through the mongo shell.md#)
    -   [Connect to a sharded cluster instance through the mongo shell](https://www.alibabacloud.com/help/doc-detail/55248.htm)
2.  Run the `db.currentOp()` command to check in-progress operations in ApsaraDB for MongoDB.

    The following is an example of the command output:

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


The following table describes the fields that you need to focus on.

|Field|Description|
|:----|:----------|
|client|The client that sent the request.|
|opid|The unique ID of the requested operation. **Note:** If necessary, you can run the `db.killOp(opid)` command to terminate an operation.

 |
|secs\_running|The duration that the operation has been running, in units of seconds. If this field returns a value that exceeds the defined threshold, check whether the request is appropriate.|
|microsecs\_running|The duration that the operation has been running, in units of milliseconds. If this field returns a value that exceeds the defined threshold, check whether the request is appropriate.|
|ns|The target collection of the operation.|
|op|The operation type, which is usually query, insert, update, or delete.|
|locks|The lock-related fields. For more information, see the official MongoDB manual. **Note:** For more information about the db.currentOp\(\) command, see [db.currentOp\(\)](https://docs.mongodb.com/manual/reference/method/db.currentOp/?spm=5176.100239.blogcont73389.12.K1pNOi).

 |

You can run the `db.currentOp()` command to check in-progress operations and analyze whether ApsaraDB for MongoDB is processing any time-consuming requests. For example, the CPU usage is normal for your routine business. When O&M management engineers log on to ApsaraDB for MongoDB to perform some operations that require a collection scan, the CPU usage significantly increases and ApsaraDB for MongoDB responds slowly. In this case, you need to check for long-running operations.

**Note:** If you find any abnormal requests, you can obtain the operation ID \(specified by the opid field\) of such a request and run the `db.killOp(opid)` command to terminate this request.

Assume that the CPU usage of the relevant ApsaraDB for MongoDB instance immediately increases and remains high after your application starts running. If you cannot find any abnormal requests in the output of the `db.currentOp()` command, you can analyze slow requests in ApsaraDB for MongoDB.

## Analyze slow requests in ApsaraDB for MongoDB {#section_n2c_ltv_1gb .section}

ApsaraDB for MongoDB enables slow request profiling by default. It automatically records requested operations that have been running for longer than 100 ms in the system.profile collection of the relevant database.

1.  Connect to an ApsaraDB for MongoDB instance through the mongo shell.

    For more information, see [Connect to a standalone instance through the mongo shell](../../../../intl.en-US/Quick Start for Standalone/Connect to an instance/Connect to ApsaraDB for MongoDB through the mongo shell.md#), [Connect to a replica set instance through the mongo shell](../../../../intl.en-US/Quick Start for Replica Set/Connect to an instance/Connect to ApsaraDB for MongoDB through the mongo shell.md#), or [Connect to a sharded cluster instance through the mongo shell](https://www.alibabacloud.com/help/doc-detail/55248.htm).

2.  Run the `use <database>` command to access a database.

    ```
    use mongodbtest
    ```

3.  Run the following command to check the slow request logs of this database:

    ```
    db.system.profile.find().pretty()
    ```

4.  Analyze the slow request logs to find the cause of high CPU usage in ApsaraDB for MongoDB.

    The following is an example of a slow request log. For this request, ApsaraDB for MongoDB did not query data based on an index, but has run a collection scan and scanned 11,000,000 documents.

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


In slow request logs, you need to focus on the following aspects:

-   Collection scan \(keywords: COLLSCAN and docsExamined\)
    -   COLLSCAN indicates a collection scan.

        A collection scan for a request \(such as a query, update, or delete operation\) can occupy lots of CPU resources. If you find a COLLSCAN keyword in slow request logs, your CPU resources may have been occupied by these slow requests.

        **Note:** If such slow requests are frequently submitted, we recommend that you create an index on queried fields to optimize query performance.

    -   The docsExamined field indicates the number of documents that ApsaraDB for MongoDB has scanned for a request. A larger value of this field indicates greater CPU overhead occupied by this request.
-   Inappropriate index \(keywords: IXSCAN and keysExamined\)

    The keysExamined field indicates the number of index keys that ApsaraDB for MongoDB has scanned for a request that uses an index. A larger value of this field indicates greater CPU overhead occupied by this request.

    If you create an index that is inappropriate or matches a large amount of data, it cannot reduce CPU overhead or shorten the running duration for a request.

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

    To query data \{ x: 1, y: 2 \}, you can create an index. The following example shows four indexes.

    ```
    db.createIndex( { x: 1 } ) // This index is inappropriate because a large amount of data has the same value of the x field.
    db.createIndex( { x: 1, y: 1 } ) // This index is inappropriate because a large amount of data has the same value of the x field.
    db.createIndex( { y: 1 } ) // This index is appropriate because a small amount of data has the same value of the y field.
    db.createIndex( { y: 1, x: 1 } ) // This index is appropriate because a small amount of data has the same value of the y field.
    ```

    For the difference between indexes \{ y: 1 \} and \{ y: 1, x: 1 \}, see [Compound Indexes](https://docs.mongodb.com/manual/core/index-compound/).

-   Sorting of a large amount of data \(keywords: SORT and hasSortStage\)

    The value of the hasSortStage field is true in the system.profile collection when a query cannot use the sort order in the index to return the requested sorted results. In this case, ApsaraDB for MongoDB must sort the query results. Considering that a sort operation consumes plenty of CPU resources, you can create an index on frequently sorted fields to optimize sorting performance.

    **Note:** If you find a SORT keyword in the system.profile collection, you can consider using an index to optimize sorting performance.


Other operations such as index creation and aggregation \(a combination of traverse, query, update, sort, and other operations\) may also consume significant CPU resources. You can also use the preceding troubleshooting methods. For more information about profiling, see [Database Profiler](https://docs.mongodb.com/manual/tutorial/manage-the-database-profiler/).

## Assess the service capability {#section_ytj_4tv_1gb .section}

After you analyze and optimize in-progress requests and slow requests in ApsaraDB for MongoDB, all requests efficiently use indexes and the query performance of ApsaraDB for MongoDB is optimized.

If CPU resources are still fully occupied during business operations, the service capability of your instances may have reached the upper limit. In this case, you need to [view the monitoring information](../../../../intl.en-US/User Guide/Monitoring and alerting/View the monitoring information.md#) to analyze the resource usage of instances. You can also test your ApsaraDB for MongoDB to check whether current instances satisfy the device performance and service capability requirements in your business scenarios.

If you need to upgrade instances, you can follow the instructions in [Change the configuration](../../../../intl.en-US/User Guide/Instance management/Change the configuration.md#).

