# Overview

This topic provides an overview of the solutions to migrate and synchronize data to or from an ApsaraDB for MongoDB database in different scenarios.

## Impacts

To ensures better performance and stability of the instance, the system will upgrade the minor version to the latest version by default If the minor version of your instance expires or is not included in the maintenance list and the instance is [upgraded](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md), [migrated](/intl.en-US/User Guide/Data migration and synchronization/Overview.md), [changed](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md), [Created from a backup](/intl.en-US/User Guide/Data recovery/Create an instance from a backup.md), [Created by point-in-time](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance by point in time.md), or performed [Restore data to a new ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance.md).

## Data migration solutions

You can fully or incrementally migrate the data of a MongoDB database by using Data Transmission Service \(DTS\). For more information, see [What is DTS](https://www.alibabacloud.com/help/zh/doc-detail/26592.htm). The full migration and incremental migration can achieve smooth data migration from a MongoDB database to the cloud without affecting businesses.

ApsaraDB for MongoDB supports full data migration by using the official mongodump and mongorestore tools.

In addition, ApsaraDB for MongoDB allows you to migrate data from the cloud to an on-premises database by using a physical or logical backup file.

|Migration scenario|Source database architecture|Reference|
|:-----------------|:---------------------------|:--------|
|Migrate data from a user-created or on-premises database to Alibaba Cloud|Standalone|[Migrate user-created standalone MongoDB databases to Alibaba Cloud by using DTS](/intl.en-US/Quick Start/Migrate data/Migrate user-created standalone MongoDB databases to Alibaba Cloud by using DTS.md)|
|[Migrate data from a user-created database to Alibaba Cloud by using tools provided by MongoDB](/intl.en-US/Quick Start/Migrate data/Migrate user-created databases to Alibaba Cloud by using tools provided by MongoDB.md)|
|Replica set|[Migrate the replica set of a user-created MongoDB database to ApsaraDB for MongoDB by using DTS](/intl.en-US/Quick Start/Migrate data/Migrate the replica set of a user-created MongoDB database to ApsaraDB for MongoDB
         by using DTS.md)|
|[Use the built-in commands of MongoDB to migrate data](/intl.en-US/Quick Start/Migrate data/Migrate user-created MongoDB databases to Alibaba Cloud by using the built-in commands of MongoDB.md)|
|Sharded cluster|[Migrate a user-created sharded MongoDB database to ApsaraDB for MongoDB by using DTS](/intl.en-US/Quick Start/Migrate data/Migrate a user-created sharded MongoDB database to ApsaraDB for MongoDB by using DTS.md)|
|[Use the built-in commands of MongoDB to migrate data](/intl.en-US/Quick Start/Migrate data/Migrate a user-created MongoDB database to ApsaraDB for MongoDB by using tools provided by MongoDB.md)|
|Migrate data from a database on a third-party cloud platform to Alibaba Cloud|N/A|[Migrate data from Amazon DynamoDB to ApsaraDB for MongoDB by using mongoimport](/intl.en-US/User Guide/Data migration and synchronization/Migrate data from a third-party cloud service provider to Alibaba Cloud/Migrate data from Amazon DynamoDB to ApsaraDB for MongoDB by using mongoimport.md)|
|Replica set or sharded cluster|-   [Migrate data from MongoDB Atlas to ApsaraDB for MongoDB by using mongodump and mongorestore](/intl.en-US/User Guide/Data migration and synchronization/Migrate data from a third-party cloud service provider to Alibaba Cloud/Migrate data from MongoDB Atlas to ApsaraDB for MongoDB by using mongodump and mongorestore.md)
-   [Migrate data from a MongoDB Atlas database to Alibaba Cloud](/intl.en-US/User Guide/Data migration and synchronization/Migrate data from a third-party cloud service provider to Alibaba Cloud/Migrate data from a MongoDB Atlas database to Alibaba Cloud.md) |
|Migrate data between ApsaraDB for MongoDB instances|Replica set|[Migrate data from a replica set MongoDB instance to a sharded cluster instance](/intl.en-US/User Guide/Data migration and synchronization/Migrate data between ApsaraDB for MongoDB instances/Migrate data from a replica set MongoDB instance to a sharded cluster instance.md)|
|Standalone|[Migrate data from a standalone MongoDB instance to a replica set or sharded cluster instance](/intl.en-US/User Guide/Data migration and synchronization/Migrate data between ApsaraDB for MongoDB instances/Migrate data from a standalone MongoDB instance to a replica set or sharded cluster
         instance.md)|
|Standalone or replica set|[Migrate data between ApsaraDB for MongoDB instances created by different Alibaba Cloud accounts](/intl.en-US/User Guide/Data migration and synchronization/Migrate data between ApsaraDB for MongoDB instances/Migrate data between ApsaraDB for MongoDB instances created by different Alibaba Cloud accounts.md)|
|Migrate data from an ApsaraDB for MongoDB instance to a user-created or on-premises MongoDB database|Replica set|[Restore logical backup data in a user-created MongoDB instance](/intl.en-US/User Guide/Data recovery/Restore data of an ApsaraDB for MongoDB instance to user-created MongoDB databases by using logical backup.md)|
|[Restore ApsaraDB for MongoDB physical backup data in a user-created MongoDB instance](/intl.en-US/User Guide/Data recovery/Recover physical backup data in a user-created MongoDB instance/Restore data of an ApsaraDB for MongoDB instance to user-created MongoDB databases by using physical backup.md)|

## Data synchronization solutions

You can use the Alibaba Cloud-developed MongoShake tool to synchronize data between MongoDB databases.

|Synchronization scenario|Tool|Reference|
|:-----------------------|:---|:--------|
|Synchronize data to an existing instance|MongoShake|[Use MongoShake to implement one-way synchronization between ApsaraDB for MongoDB replica set instances](/intl.en-US/User Guide/Data migration and synchronization/Data synchronization/Use MongoShake to implement one-way synchronization between ApsaraDB for MongoDB replica
         set instances.md)|

