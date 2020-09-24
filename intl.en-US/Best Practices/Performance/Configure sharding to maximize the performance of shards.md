# Configure sharding to maximize the performance of shards

You can configure sharding for each collection in a sharded cluster instance to make full use of the storage space and maximize the computing performance of shards in the sharded cluster.

## Background

If a collection is not sharded, all its data is stored on the same shard. In this case, you cannot make full use of the storage space and maximize the computing performance of other shards in the sharded cluster.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3230937951/p33995.png)

## Prerequisites

A sharded cluster instance is used.

## Precautions

-   You cannot change or delete the configured shard key after sharding.
-   After you configure sharding, the balancer shards existing data that meets the specified criteria, which consumes the resources of an instance. We recommend that you perform this operation during off-peak hours.

    **Note:** Before configuring sharding, you can set an active time window to limit the effective period of the balancer to off-peak hours. For more information, see [Set an active time window for the balancer](/intl.en-US/Best Practices/Manage the ApsaraDB for MongoDB balancer.md).

-   The choice of a shard key affects the performance of a sharded cluster instance. For more information about how to choose a shard key, see [Shard key selection](https://docs.mongodb.com/manual/core/sharding-shard-key/#sharding-shard-key-selection).

## Sharding strategies

|Sharding strategy|Description|Scenario|
|:----------------|:----------|:-------|
|Ranged sharding|MongoDB divides data into contiguous ranges determined by the shard key values. Each chunk represents a contiguous range of data. -   Advantage: The mongos can quickly locate the data being requested and forward the requests to the target shard.
-   Disadvantage: Data may be distributed unevenly among shards, causing hot shards for reads and writes and an uneven spread of writes.

|The shard key value is not monotonically increasing or decreasing. The shard key has large cardinality and low frequency. Range-based queries are required. |
|Hashed sharding|MongoDB computes the hash value of a single field as the index value and divides data into chunks based on the range of hash values. -   Advantage: Data can be distributed evenly among shards, guaranteeing an even spread of writes.
-   Disadvantage: This strategy is inapplicable to range-based queries because read requests must be distributed across all shards during the queries.

|The shard key value is monotonically increasing or decreasing. The shard key has large cardinality and low frequency. Data writes are randomly distributed to shards. Data is read with high randomness. |

In addition to the preceding two sharding strategies, you can also configure a compound shard key. For example, configure both a key with low cardinality and a monotonically increasing key. For more information, see .

## Procedure

The following procedure uses the database named mongodbtest and the collection named customer as an example.

1.  [Connect to a sharded cluster instance by using the mongo shell](/intl.en-US/Quick Start for Cluster/Connect to an instance/Connect to a sharded cluster instance by using the mongo shell.md).
2.  Enable sharding for the database where the collection to be sharded resides.

    ```
    sh.enableSharding("<database>")
    ```

    **Note:** <database\>: the name of the database.

    Example:

    ```
    sh.enableSharding("mongodbtest")
    ```

    **Note:** You can run the `sh.status()` command to check whether sharding is enabled.

3.  Create an index on the shard key field.

    ```
    db.<collection>.createIndex(<keyPatterns>,<options>)
    ```

    **Note:**

    -   <collection\>: the name of the collection.
    -   <keyPatterns\>: the field used for indexing and the index type.

        Common index types are as follows:

        -   1: an ascending index
        -   -1: a descending index
        -   "hashed": a hashed index
    -   <options\>: the optional parameters. For more information, see [db.collection.createIndex\(\)](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/). This field is not used in this example.
    Sample command for creating an ascending index:

    ```
    db.customer.createIndex({name:1})
    ```

    Sample command for creating a hashed index:

    ```
    db.customer.createIndex({id:"hashed"})
    ```

4.  Configure sharding for the collection.

    ```
    sh.shardCollection("<database>.<collection>",{ "<key>":<value> } ) 
    ```

    **Note:**

    -   <database\>: the name of the database.
    -   <collection\>: the name of the collection.
    -   <key\>: the shard key that MongoDB uses to shard data.
    -   <value\>
        -   1: ranged sharding. This strategy supports efficient range-based queries based on the shard key.
        -   "hashed": hashed sharding. This strategy distributes data evenly among shards.
    Sample command for configuring ranged sharding:

    ```
    sh.shardCollection("mongodbtest.customer",{"name":1})
    ```

    Sample command for configuring hashed sharding:

    ```
    sh.shardCollection("mongodbtest.customer",{"id":"hashed"})
    ```


## What to do next

After the database has been running and data has been written for a while, you can run the `sh.status()` command in the mongo shell to check the chunk information on shards.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4230937951/p34049.png)

You can also run the `db.stats()` command to check the size of data stored on each shard.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4230937951/p33949.png)

