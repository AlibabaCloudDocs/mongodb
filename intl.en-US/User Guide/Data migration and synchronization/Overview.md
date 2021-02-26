---
keyword: [database migration, MongoDB database migration, data synchronization between Alibaba Cloud databases, database synchronization, database synchronization tool]
---

# Overview

This topic provides an overview of the solutions to migrate and synchronize data to or from an ApsaraDB for MongoDB database in different scenarios.

## Data migration solutions

By using [Data Transmission Service \(DTS\)](Data Transmission Service (DTS)t17063.dita#concept_26592_zh), you can fully or incrementally migrate the data of a MongoDB database. This can achieve smooth data migration from a MongoDB database to the cloud without affecting businesses.

ApsaraDB for MongoDB supports full data migration by using the official mongodump and mongorestore tools.

In addition, ApsaraDB for MongoDB allows you to migrate data from the Cloud to an on-premises database by using a physical or logical backup file.

|Migration scenario|Source database architecture|Documentation|
|:-----------------|:---------------------------|:------------|
|Migrate data from a self-mamanged or on-premises database to Alibaba Cloud|Standalone instance|[Migrate self-managed standalone MongoDB databases to Alibaba Cloud by using DTS](/intl.en-US/Quick Start/Migrate data/Migrate self-managed standalone MongoDB databases to Alibaba Cloud by using DTS.md)|
|[Migrate self-managed MongoDB databases to standalone instances by using tools provided by MongoDB](/intl.en-US/Quick Start/Migrate data/Migrate self-managed MongoDB databases to standalone instances by using tools provided
         by MongoDB.md)|
|Replica set instance|[Migrate the replica set of a user-created MongoDB database to ApsaraDB for MongoDB by using DTS](/intl.en-US/Quick Start/Migrate data/Migrate the replica set of a user-created MongoDB database to ApsaraDB for MongoDB
         by using DTS.md)|
|[Migrate self-managed databases to Alibaba Cloud by using tools provided by MongoDB](/intl.en-US/Quick Start/Migrate data/Migrate self-managed databases to Alibaba Cloud by using tools provided by MongoDB.md)|
|Sharded cluster instance|[Migrate a user-created sharded MongoDB database to ApsaraDB for MongoDB by using DTS](/intl.en-US/Quick Start/Migrate data/Migrate a user-created sharded MongoDB database to ApsaraDB for MongoDB by using DTS.md)|
|[Migrate a self-managed MongoDB database to ApsaraDB for MongoDB by using tools provided by MongoDB](/intl.en-US/Quick Start/Migrate data/Migrate a self-managed MongoDB database to ApsaraDB for MongoDB by using tools provided
         by MongoDB.md)|
|Migrate data from a database on a third-party cloud platform to Alibaba Cloud|N/A|[Migrate data from Amazon DynamoDB to ApsaraDB for MongoDB by using mongoimport](/intl.en-US/User Guide/Data migration and synchronization/Migrate data from a third-party cloud service provider to Alibaba Cloud/Migrate data from Amazon DynamoDB to ApsaraDB for MongoDB by using mongoimport.md)|
|Replica set or sharded cluster instance|-   [Migrate data from MongoDB Atlas to ApsaraDB for MongoDB by using mongodump and mongorestore](/intl.en-US/User Guide/Data migration and synchronization/Migrate data from a third-party cloud service provider to Alibaba Cloud/Migrate data from MongoDB Atlas to ApsaraDB for MongoDB by using mongodump and mongorestore.md)
-   [Migrate data from a MongoDB Atlas database to Alibaba Cloud](/intl.en-US/User Guide/Data migration and synchronization/Migrate data from a third-party cloud service provider to Alibaba Cloud/Migrate data from a MongoDB Atlas database to Alibaba Cloud.md) |
|Migrate data between ApsaraDB for MongoDB instances|Replica set instance|[Migrate data from a replica set MongoDB instance to a sharded cluster instance](/intl.en-US/User Guide/Data migration and synchronization/Migrate data between ApsaraDB for MongoDB instances/Migrate data from a replica set MongoDB instance to a sharded cluster instance.md)|
|Standalone instance|[Migrate data from a standalone instance to a replica set or sharded cluster instance](/intl.en-US/User Guide/Data migration and synchronization/Migrate data between ApsaraDB for MongoDB instances/Migrate data from a standalone instance to a replica set or sharded cluster instance.md)|
|Standalone or replica set instance|[Migrate data between ApsaraDB for MongoDB instances created by different Alibaba Cloud accounts](/intl.en-US/User Guide/Data migration and synchronization/Migrate data between ApsaraDB for MongoDB instances/Migrate data between ApsaraDB for MongoDB instances created by different Alibaba Cloud
         accounts.md)|
|Migrate data from an ApsaraDB for MongoDB instance to a self-managed or on-premises MongoDB database|Replica set instance|[Restore data of an ApsaraDB for MongoDB instance to self-managed MongoDB databases by using logical backup](/intl.en-US/User Guide/Data recovery/Restore data of an ApsaraDB for MongoDB instance to self-managed MongoDB databases
         by using logical backup.md)|
|[Restore data of an ApsaraDB for MongoDB instance to a self-managed MongoDB database by using physical backup](/intl.en-US/User Guide/Data recovery/Recover physical backup data in a user-created MongoDB instance/Restore data of an ApsaraDB for MongoDB instance to a self-managed MongoDB database
         by using physical backup.md)|

## Data synchronization solutions

You can use the MongoShake tool developed by Alibaba Cloud to synchronize data between MongoDB databases.

|Synchronization scenario|Tool|Documentation|
|:-----------------------|:---|:------------|
|Synchronize data to an existing instance|MongoShake|[Use MongoShake to implement one-way synchronization between ApsaraDB for MongoDB replica set instances](/intl.en-US/User Guide/Data migration and synchronization/Data synchronization/Use MongoShake to implement one-way synchronization between ApsaraDB for MongoDB replica
         set instances.md)|

