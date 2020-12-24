# Usage notes

You can migrate data from a self-managed MongoDB database to an ApsaraDB for MongoDB instance, but you must pay close attention to the limits of ApsaraDB for MongoDB.

## Standalone instances

|Operation|Limit|
|:--------|:----|
|Deploy an instance|Standalone instances can be created only in the China \(Hangzhou\), China \(Shanghai\), China \(Qingdao\), China \(Beijing\), and China \(Shenzhen\) regions.|
|Configure the database version|The MongoDB version must be 3.4.|
|Configure the storage engine|The storage engine must be WiredTiger. |
|Connect to an instance by using its public endpoint|It is risky to connect to ApsaraDB for MongoDB instances over the Internet. By default, only an internal endpoint is provided after an instance is activated. If you need to connect to an instance over the Internet, apply for a public endpoint. For more information, see [Apply for a public endpoint for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Network connection management/Public IP Connection/Apply for a public endpoint for an ApsaraDB for MongoDB instance.md).|
|Restart an instance|You must restart an instance by using the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) or by calling the [RestartDBInstance](/intl.en-US/API Reference/Instance management/RestartDBInstance.md) operation.|
|Migrate data|You can use the built-in commands of MongoDB or Data Transmission Service \(DTS\) to migrate data. For more information, see [Migrate user-created databases to Alibaba Cloud by using tools provided by MongoDB](/intl.en-US/Quick Start/Migrate data/Migrate user-created databases to Alibaba Cloud by using tools provided by MongoDB.md) or [Migrate the replica set of a user-created MongoDB database to ApsaraDB for MongoDB by using DTS](/intl.en-US/Quick Start/Migrate data/Migrate the replica set of a user-created MongoDB database to ApsaraDB for MongoDB
         by using DTS.md).|
|Back up data|Standalone instances are backed up in snapshot mode due to their special architecture. **Note:** A snapshot backup retains the status of disk data at a specific point in time. |
|Restore data|You can create instances based only on backup data. For more information, see [Create an instance from a backup](/intl.en-US/User Guide/Data recovery/Create an instance from a backup.md).|
|Modify the parameters of an instance|For security and stability reasons, some parameters cannot be modified. For more information, see [Configure database parameters for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Parameter settings/Configure database parameters for an ApsaraDB for MongoDB instance.md).|

## Replica set instances

|Operation|Limit|
|:--------|:----|
|Deploy an instance|The database version must match the storage engine. For more information, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).|
|Build replica set nodes|-   A replica set instance automatically created by ApsaraDB for MongoDB consists of a primary node, a hidden secondary node \(invisible to you\), and one or more secondary nodes.
-   When a replica set instance is running, you can scale the instance to one that has three, five, or seven nodes. For more information, see [Change the number of nodes for a replica set instance](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Change the number of nodes for a replica set instance.md).

**Note:** You cannot connect to a replica set instance from a secondary node of a self-managed database. If you want to synchronize data from a replica set instance to a self-managed MongoDB database for data testing or analysis, you can use MongoShake. For more information, see [Use MongoShake to implement one-way synchronization between ApsaraDB for MongoDB replica set instances](/intl.en-US/User Guide/Data migration and synchronization/Data synchronization/Use MongoShake to implement one-way synchronization between ApsaraDB for MongoDB replica
         set instances.md). |
|Restart an instance|You must restart an instance by using the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) or by calling the [RestartDBInstance](/intl.en-US/API Reference/Instance management/RestartDBInstance.md) operation.|
|Migrate data|You can use the built-in commands of MongoDB or Data Transmission Service \(DTS\) to migrate data. For more information, see [Migrate the replica set of a user-created MongoDB database to ApsaraDB for MongoDB by using DTS](/intl.en-US/Quick Start/Migrate data/Migrate the replica set of a user-created MongoDB database to ApsaraDB for MongoDB
         by using DTS.md) or [Migrate user-created MongoDB databases to Alibaba Cloud by using the built-in commands of MongoDB](/intl.en-US/Quick Start/Migrate data/Migrate user-created MongoDB databases to Alibaba Cloud by using the built-in commands of MongoDB.md).|
|Back up data|Automatic backup supports only physical backup. Manual backup supports both physical and logical backup. For more information, see [Configure automatic backup for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data backup/Configure automatic backup for an ApsaraDB for MongoDB instance.md) and [Manually back up an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data backup/Manually back up an ApsaraDB for MongoDB instance.md). **Note:** If the database version of an instance is 3.2 or 3.4, the number of collections and indexes in the instance cannot exceed 10,000. Otherwise, physical backup may fail. If you want to increase this limit, we recommend that you upgrade the database version to 4.0 or 4.2. For more information, see [Upgrade MongoDB versions](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade the database version of an ApsaraDB for MongoDB instance.md). Alternatively, you can set the database version to 4.0 or 4.2 when you create an instance. |
|Restore data|-   You can restore data from a point in time or a backup set. For more information, see [Create an instance from a backup](/intl.en-US/User Guide/Data recovery/Create an instance from a backup.md) and [Restore data to a new ApsaraDB for MongoDB instance by point in time](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance by point in time.md).
-   You can restore data to your current replica set instance only if it has three nodes. For more information, see [Restore data to the current ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data recovery/Restore data to the current ApsaraDB for MongoDB instance.md). |
|Modify the parameters of an instance|For security and stability reasons, some parameters cannot be modified. For more information, see [Configure database parameters for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Parameter settings/Configure database parameters for an ApsaraDB for MongoDB instance.md).|

## Sharded cluster instances

|Operation|Limit|
|:--------|:----|
|Deploy an instance|The database version must match the storage engine. For more information, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).|
|Build cluster components|-   When you create a sharded cluster instance, you can specify the specifications and numbers of mongos and shards.
-   While the instance is running, you can add mongos and shards, but you cannot remove them. For more information, see [Configuration change overview](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md). |
|Restart an instance|You must restart an instance by using the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) or by calling the [RestartDBInstance](/intl.en-US/API Reference/Instance management/RestartDBInstance.md) operation.|
|Migrate data|You can use the built-in commands of MongoDB or Data Transmission Service \(DTS\) to migrate data. For more information, see [Migrate user-created databases to Alibaba Cloud by using tools provided by MongoDB](/intl.en-US/Quick Start/Migrate data/Migrate a user-created MongoDB database to ApsaraDB for MongoDB by using tools provided by MongoDB.md) or [Migrate the replica set of a user-created MongoDB database to ApsaraDB for MongoDB by using DTS](/intl.en-US/Quick Start/Migrate data/Migrate a user-created sharded MongoDB database to ApsaraDB for MongoDB by using DTS.md). |
|Back up data|Automatic backup supports only physical backup. Manual backup supports both physical and logical backup. For more information, see [Configure automatic backup for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data backup/Configure automatic backup for an ApsaraDB for MongoDB instance.md) and [Manually back up an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data backup/Manually back up an ApsaraDB for MongoDB instance.md). **Note:** If the database version of an instance is 3.2 or 3.4, the number of collections and indexes in the instance cannot exceed 10,000. Otherwise, physical backup may fail. If you want to increase this limit, we recommend that you upgrade the database version to 4.0. For more information, see [Upgrade MongoDB versions](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade the database version of an ApsaraDB for MongoDB instance.md).Alternatively, you can set the database version to 4.0 when you create an instance. |
|Restore data|You can restore data only by point in time. For more information, see [Restore data to a new ApsaraDB for MongoDB instance by point in time](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance by point in time.md).|
|Modify the parameters of an instance|For security and stability reasons, some parameters cannot be modified.|
|Read and write data|You can only read data from the admin database of a sharded cluster instance, and you cannot write data to the admin database.|

