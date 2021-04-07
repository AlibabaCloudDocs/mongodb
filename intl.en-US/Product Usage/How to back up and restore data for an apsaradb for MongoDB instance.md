# How do I back up and restore an ApsaraDB for MongoDB instance?

You can back up an ApsaraDB for MongoDB instance in either the automatic or manual mode, and restore it from backup files or to a point in time.

## Backup

ApsaraDB for MongoDB stores its backup files in [Object Storage Service \(OSS\)](~~31817~~) to reduce the storage space usage of its instances. You can perform an automatic or manual backup in the ApsaraDB for MongoDB console. For more information, see [Configure automatic backup for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data backup/Configure automatic backup for an ApsaraDB for MongoDB instance.md) or [Manually back up an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data backup/Manually back up an ApsaraDB for MongoDB instance.md).

**Note:** If you choose automatic backup, only physical backup is supported.

|Instance|Backup method|Impact|
|--------|-------------|------|
|Standalone instances|Snapshot backup **Note:** The status of disk data at a specific point in time is retained.

|Snapshot backup affects the I/O performance of standalone instances.|
|-   Replica set instances
-   Sharded cluster instances

|Physical backup **Note:** Physical data files of an instance are backed up.

|Physical backup runs on a hidden node, which does not affect the read/write performance of the primary and secondary nodes. Backing up a large volume of data may take a long time.|
|Logical backup **Note:** mongodump is used to logically back up each database. |

## Restoration

For more information, see [Restoration solution overview](/intl.en-US/User Guide/Data recovery/Restoration solution overview.md).

