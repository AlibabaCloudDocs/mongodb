# What is the log deletion policy of an ApsaraDB for MongoDB instance?

Logs are automatically deleted when their size reaches a specific threshold.

In emergencies, you can run the `compact` command to delete oplogs. For more information, see [Defragment a disk to improve disk usage](/intl.en-US/Best Practices/Performance/Defragment a disk to improve disk usage.md).

**Note:**

-   You can only run this command on replica set instances.
-   Before running `compact`, you must log on to the local database where the oplog.rs collection is stored.

