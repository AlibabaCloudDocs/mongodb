# What do I do if my ApsaraDB for MongoDB instance is locked due to exhausted disk space?

If the disk space of an ApsaraDB for MongoDB instance is exhausted, the instance is locked and you cannot write data to or delete data from it.

## Symptoms

-   You can read but cannot write data in the instance.
-   The administrator enters the following command in the mongo shell, and `not authorized on xxxx to execute command` is returned.

    ```
    db.customer.insert({"name":"zhangsan"})
    WriteCommandError({
            "operationTime" : Timestamp(1563437183, 1),
            "ok" : 0,
            "errmsg" : "not authorized on db1 to execute command { insert: \"customer\", ordered: true, lsid: { id: UUID(\"8d43461c-5c51-49ef-b9b3-9xxxxxxxxf\") }, $clusterTime: { clusterTime: Timestamp(1563437183, 1), signature: { hash: BinData(0, 0C3FAAE747xxxxxx), keyId: 668293399xxxxxx } }, $db: \"db1\" }",
            "code" : 13,
            "codeName" : "Unauthorized",
            "$clusterTime" : {
                    "clusterTime" : Timestamp(1563437183, 1),
                    "signature" : {
                            "hash" : BinData(0,"DD+q50dPTuIQKTzytT5SiTPYX4Q="),
                            "keyId" : NumberLong("66xxxxxxxx")
                    }
            }
    })
    ```

-   The administrator finds that the instance status is **Locked** in the ApsaraDB for MongoDB console.

    **Note:** Sharded cluster instances are a special case. When the disk space of a sharded cluster instance is exhausted, the instance does not enter the **Locked** state.


## Check whether disk space is exhausted

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  Check whether disk space is exhausted.

    **Note:** The system collects data on disk space usage at intervals of five minutes.

    -   Standalone or replica set instances

        On the **Basic Information** page, view the instance status and its disk space usage. In this example, the instance status is **Locked**, and the disk space usage of the instance exceeds 100%, which indicates that the disk space is exhausted.

        ![View disk space usage](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4266845951/p51781.png)

    -   Sharded cluster instances
        1.  In the left-side navigation pane, click **Monitoring Info**.
        2.  On the **Monitoring Info** page that appears, select the target shard.

            ![Select a shard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4266845951/p51878.png)

            **Note:** If an ID starts with the letter `d`, it indicates a shard. If an ID starts with the letter `s`, it indicates a mongos.

        3.  View disk space usage. In this example, the disk space usage of the shard exceeds 100%, which indicates that the disk space is exhausted.

            ![View disk space usage](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4266845951/p51879.png)


## Solutions

-   Expand the disk space of the instance. For more information, see [t6706.md\#](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

    **Note:** Maximum disk space varies with instance types. For more information, see [Instance types](/intl.en-US/Product Introduction/Instance types.md).

-   A replica set instance supports up to 3,000 GB of disk space. If you need greater disk space, we recommend that you deploy a [sharded cluster instance](/intl.en-US/Product Introduction/System architecture/Architecture of sharded cluster instances.md) where you can add shards to expand the disk space up to 96,000 GB.

    **Note:** You can use Data Transmission Service \(DTS\) to migrate data from a source instance to a new sharded cluster instance. For more information, see [Migrate data from a replica set MongoDB instance to a sharded cluster instance](/intl.en-US/User Guide/Data migration and synchronization/Migrate data between ApsaraDB for MongoDB instances/Migrate data from a replica set MongoDB instance to a sharded cluster instance.md).


## Suggestions

If you have executed the `db.collection.remove` command to delete a large volume of data or you have not defragmented your disk, you can still increase disk space by performing defragmentation. For more information, see [Defragment a disk to improve disk usage](/intl.en-US/Best Practices/Performance/Defragment a disk to improve disk usage.md).

