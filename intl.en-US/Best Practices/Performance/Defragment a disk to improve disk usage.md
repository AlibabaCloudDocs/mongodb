# Defragment a disk to improve disk usage

Fragments may occur in disks when you frequently write and delete large amounts of data in ApsaraDB for MongoDB databases. Fragments occupy disk space and reduce disk usage. You can rewrite all data and indexes in collections and defragment disks to release idle space. This improves disk usage and query performance.

## Prerequisites

The ApsaraDB for MongoDB instance uses WiredTiger as the storage engine.

## Precautions

-   We recommend that you back up data in ApsaraDB for MongoDB databases before defragmentation. For more information, see [Manually back up an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data backup/Manually back up an ApsaraDB for MongoDB instance.md).
-   During defragmentation, the database where the collection is stored is locked and read and write operations are not allowed in the database. We recommend that you defragment disks during off-peak hours.

    **Note:** The time to defragment a disk by running the compact command depends on multiple factors, such as the data volume of the collection and the system load.


## Background information

![How the disk space is reclaimed](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3004180951/p55162.gif)

If you run the `db.collection.remove({}, {multi: true})` command to delete a document from the B tree, the disk space occupied by the document is not reclaimed. If you run the remove command to delete a large number of documents, but write little data to the disk later, disk usage is reduced. In this case, you can run the compact command to reclaim the idle disk space.

**Note:**

-   If the size of the newly written data is less than or equal to the space of a fragment, the newly written data occupies the space of the fragment. Therefore, you do not need to frequently run the compact command for defragmentation if data is continuously written.
-   If you run the `db.collection.drop()` command to delete a collection, the files in the collection are deleted and the disk space occupied by the files is reclaimed.

## Estimate the disk space to be reclaimed

1.  Connect to the ApsaraDB for MongoDB instance by using the mongo shell. For more information, see the following topics:

    -   [Connect to a standalone instance by using the mongo shell](/intl.en-US/Quick Start/Connect to an instance/Connect to a standalone ApsaraDB for MongoDB instance by using the mongo shell.md)
    -   [Connect to a replica set instance by using the mongo shell](/intl.en-US/Quick Start/Connect to an instance/Connect to a replica set instance by using the mongo shell.md)
    -   [Connect to a sharded cluster instance by using the mongo shell](/intl.en-US/Quick Start/Connect to an instance/Connect to a sharded cluster instance by using the mongo shell.md)
2.  Run the following command to switch to the database where the collection is stored:

    ```
    use <database_name>
    ```

    **Note:** <database\_name\>: the name of the database.

3.  Run the following command to query the disk space that can be reclaimed from the collection:

    ```
    db.<collection_name>.stats().wiredTiger["block-manager"]["file bytes available for reuse"]
    ```

    **Note:** <collection\_name\>: the name of the collection.

    Example:

    ```
    db.customer.stats().wiredTiger["block-manager"]["file bytes available for reuse"]
    ```

    Output:

    ```
    207806464
    ```


## Defragment a standalone instance or a replica set instance

1.  Connect to the primary node of an ApsaraDB for MongoDB instance by using the mongo shell. For more information, see [Connect to a replica set instance by using the mongo shell]().

2.  Run the following command to switch to the database where the collection is stored:

    ```
    use <database_name>
    ```

    **Note:** <database\_name\>: the name of the database.

3.  Run the `db.stats()` command to view the disk space occupied by the database before defragmentation.

4.  Run the following command to defragment a collection:

    ```
    db.runCommand({compact:"<collection_name>",force:true})
    ```

    **Note:**

    -   <collection\_name\>: the name of the collection.
    -   The `force` parameter is optional. To run the compact command on the primary node of a replica set instance, you must set the `force` parameter to true.
5.  Wait until `{"ok":1}` is returned, which indicates that the command is executed.

    **Note:** The compact command executed on the primary node does not affect a secondary node. For a replica set instance, repeat the preceding steps to connect to a secondary node by using the mongo shell and run the compact command.

    After defragmentation is complete, you can run the `db.stats()` command to view the disk space occupied by the database. The following figure shows the storage size before and after defragmentation.

    ![Storage size before and after defragmentation](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4004180951/p55634.gif)


## Defragment a sharded cluster instance

1.  Connect to any mongos node in the sharded cluster instance by using the mongo shell. For more information, see [Connect to a sharded cluster instance by using the mongo shell](/intl.en-US/Quick Start/Connect to an instance/Connect to a sharded cluster instance by using the mongo shell.md).

2.  Run the `db.stats()` command to view the disk space occupied by the database before defragmentation.

3.  Run the following command to defragment a collection on the primary node of a shard:

    ```
    db.runCommand({runCommandOnShard:"<Shard ID>","command":{compact:"<collection_name>",force:true}})
    ```

    **Note:**

    -   <Shard ID\>: the ID of the shard.
    -   <collection\_name\>: the name of the collection.
4.  Run the following command to defragment a collection on a secondary node of a shard:

    ```
    db.runCommand({runCommandOnShard:"<Shard ID>","command":{compact:"<collection_name>"},$queryOptions: {$readPreference: {mode: 'secondary'}}})
    ```

    **Note:**

    -   <Shard ID\>: the ID of the shard.
    -   <collection\_name\>: the name of the collection.
    After defragmentation is complete, you can run the `db.runCommand({dbstats:1})` command to view the disk space occupied by the database.


## 相关问题

[What do I do if my ApsaraDB for MongoDB instance is locked due to exhausted disk space?](/intl.en-US/Product Usage/Hot issues/Write failures caused by disk space exhaustion in MongoDB.md)

