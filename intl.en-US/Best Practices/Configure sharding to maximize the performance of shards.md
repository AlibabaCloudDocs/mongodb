# Configure sharding to maximize the performance of shards {#concept_tbb_vzp_bgb .concept}

You can configure sharding at the collection level for databases in a sharded cluster instance to make full use of the storage space and maximize the computing performance of shards in the sharded cluster.

## Precautions {#section_mpp_hxq_bgb .section}

-   This operation applies only to sharded cluster instances.
-   After you configure sharding, the balancer shards existing data that meets the specified criteria. Because sharding affects the performance of an instance, we recommend that you perform this operation during off-peak hours.
-   You cannot change the configured shard key after sharding.
-   The choice of a shard key affects the performance of a sharded cluster instance. For more information about how to choose a shard key, see [Shard Keys](https://docs.mongodb.com/manual/core/sharding-shard-key/#sharding-shard-key-selection).
-   If you do not configure sharding, data is written to the primary shard. In this case, you cannot make full use of the storage space and maximize the computing performance of other shards in the same sharded cluster.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/78547/155624401233995_en-US.png)


## Procedure {#section_g4t_fxq_bgb .section}

The following procedure uses the database named mongodbtest and the collection named customer as an example.

1.  [Connect to a sharded cluster instance through the mongo shell](https://www.alibabacloud.com/help/doc-detail/55248.htm).
2.  Enable sharding for the database where the collection to be sharded is located.

    ```
    sh.enableSharding("<database>")
    ```

    In the preceding command, <database\> indicates the database name.

    Example:

    ```
    sh.enableSharding("mongodbtest")
    ```

    **Note:** You can run the `sh.status()` command to check the sharding status.

3.  Create an index on a field in the collection.

    ```
    db.<collection>.createIndex(<keys>,<options>)
    ```

    Notes:

    -   <collection\>: The collection name.
    -   <keys\>: The field and value pair where the field is the index key and the value describes the sort order for this field.

        A value of 1 indicates an ascending index on the field. A value of -1 indicates a descending index on the field.

    -   <options\>: The additional options. For more information, see [db.collection.createIndex\(\)](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/). This parameter is not used in this example.
    Example:

    ```
    db.customer.createIndex({"name":1})
    ```

4.  Configure sharding for the collection.

    ```
    sh.shardCollection("<database>.<collection>",{ "<key>":<value> } ) 
    ```

    Notes:

    -   <database\>: The database name.
    -   <collection\>: The collection name.
    -   <key\>: The shard key, based on which ApsaraDB for MongoDB shards data.
    -   <value\>:

        -   1: indicates an ascending index on the shard key, which can properly support range queries based on the shard key.
        -   -1: indicates a descending index on the shard key, which can properly support range queries based on the shard key.
        -   hashed: indicates a hashed shard key, which can be used to write data evenly to various shards.
        \[DO NOT TRANSLATE\]

    Example:

    ```
    sh.shardCollection("mongodbtest.customer",{"name":1})
    ```


If this collection contains data in the database, the backend balancer can automatically shard data after your configuration. The sharding process is transparent to you.

## Subsequent operations {#section_w5t_4jr_bgb .section}

After the database has been running and data has been written for a while, you can run the `sh.status()` command in the mongo shell to check the sharding configuration and the chunk information on shards.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/78547/155624401234049_en-US.png)

You can also run the `db.stats()` command to check the data storage of this database on various shards.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/78547/155624401333949_en-US.png)

