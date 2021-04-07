# What is the impact of changes made to the storage space on an ApsaraDB for MongoDB instance?

When you change the storage space of an ApsaraDB for MongoDB instance, there is a brief disconnection of about 30 seconds. This brief disconnection does not affect data in the instance.

If the storage space of an ApsaraDB for MongoDB instance is insufficient, you can expand the storage space. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

**Note:** If your application is in a production environment, we recommend that you use a connection string URI to connect to the instance. This way, the read/write operations of your application remain available even if there is a primary/secondary switchover. For more information, see [Overview of replica set instance connections]().

