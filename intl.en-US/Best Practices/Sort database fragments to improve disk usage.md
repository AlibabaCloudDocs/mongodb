# Sort database fragments to improve disk usage {#concept_ngj_sxl_sfb .concept}

Fragmentation occurs when you frequently write and delete data on MongDB. These fragments occupy disk space and reduce disk usage. You can rewrite and defragment all the data and indexes in a collection to release unused space, improving disk usage and query performance.

## Precautions {#section_e4r_3bm_sfb .section}

-   We recommend that you back up the database before performing this operation.
-   The database is locked during defragmentation and read/write operations are blocked. We recommend that you perform this operation during off-peak hours.
-   We do not recommend that you frequently perform this operation.

## Operation example of standalone instances or replica set instances {#section_xmg_jbm_sfb .section}

1.  Connect to the primary node of ApsaraDB for MongoDB through the mongo shell. For more information, see [Use the mongo shell to connect to an instance](../../../../intl.en-US/Quick Start for Replica Set/Connect to an instance/Connect to an replica set instance through the mongo shell.md#).
2.  Run the following command to switch to the database where the collection is stored.

    ```
    use <database_name>
    ```

    Command description:

    <database\_name\>: the name of the database.

3.  Run the following command to defragment a collection:

    ```
    db.runCommand({compact:"<collection_name>",force:true})
    ```

    Command description:

    <collection\_name\>: the name of the collection.

    **Note:** The force parameter is optional.

    -   If the value is true, the compact command can be executed on the primary node of a replica set.
    -   If the value is false, the compact command executed on the primary node returns an error.
4.  Wait for the command execution to complete. If `{"OK": 1}` is returned, the command is executed.

    **Note:** The compact operation is not passed to the secondary node. When the instance is a replica set instance, repeat the preceding steps to connect to the secondary node through the mongo shell and run the compact command.


After defragmentation is complete, you can run the `db.stats()` command to view the disk space occupied by the database.

## Operation example of sharded cluster instances {#section_h52_qwz_sfb .section}

1.  Connect to any mongos in the sharded cluster instance through the mongo shell. For more information, see [Connect to an ApsaraDB for MongoDB sharded cluster instance through the mongo shell](../../../../intl.en-US/Quick Start for Cluster/Connect to an instance/Connect to an ApsaraDB for MongoDB instance through the mongo shell.md#).
2.  Run the following command to defragment a collection in the primary node of the shard:

    ```
    db.runCommand({runCommandOnShard:"<Shard ID>","command":{compact:"<collection_name>",force:true}})
    
    ```

    Command description:

    <Shard ID\>: the ID of the shard.

    <collection\_name\>: the name of the collection.

3.  Run the following command to defragment a collection in the secondary node of the shard:

    ```
    db.runCommand({runCommandOnShard:"<Shard ID>","command":{compact:"<collection_name>"},queryOptions: {$readPreference: {mode: 'secondary'}}})
    ```

    Command instructions:

    <Shard ID\>: the ID of the shard.

    <collection\_name\>: the name of the collection.


After the defragmentation is complete, you can run the `db.runCommand({dbstats:1})` command to view the disk space occupied by the database after defragmentation.

