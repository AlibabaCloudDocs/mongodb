# Versions and storage engines {#concept_qg2_xcr_52b .concept}

ApsaraDB for MongoDB supports MongoDB 3.2, 3.4, and 4.0. Compared with MongoDB 3.2, MongoDB 3.4 has been improved in aspects of performance and security. MongoDB 4.0 is more suitable for finance and other scenarios that are dependent on transactions and use NoSQL features.

## Database versions {#section_okn_x4c_bfb .section}

**MongoDB 3.4 has the following advantages:**

-   Faster primary-secondary synchronization

    When a three-node replica set instance of the MongoDB 3.4 version performs a full primary-secondary synchronization, the instance creates indexes for all data. In earlier versions, an ApsaraDB for MongoDB instance creates the ID index first when data is being copied and creates other indexes after data is copied. Oplogs are a capped collection that automatically overwrites its oldest data when it reaches its maximum size. In the process of data copy, the ApsaraDB for MongoDB instance pulls newly generated oplogs from the synchronization source and stores them in a temporary collection of the local database. After the full copy of data, the instance directly reads oplogs from the local temporary collection to improve the efficiency of incremental data synchronization. This also avoids synchronization failures caused by incomplete oplogs to be synchronized in the synchronization source.

-   More efficient sharded clusters: For more information, click [here](http://www.mongoing.com/archives/3889).
-   More powerful features: such as `Readonly View`, `Collation`, and `Decimal type`
-   More aggregation stages: such as `$bucket` and `$graghLookup`

**MongoDB 4.0 has the following advantages:** 

-   Ensures that the speed, flexibility, and features of the document object model comply with Atomicity, Consistency, Isolation, Durability \(ACID\).
-   Uses transaction features to ensure that secondary nodes do not block read requests when they are synchronizing logs.
-   Supports concurrent read and write operations to improve the migration performance of new shards by about 40%, so that they can quickly be ready to bear the business pressure.

**Note:** 

-   You cannot upgrade existing instances to MongoDB 4.0. To use MongoDB 4.0, you need to select **MongoDB 4.0** for **Database Version** when you create an instance.****\[DO NOT TRANSLATE\]
-   You can manually upgrade the database version of an instance from MongoDB 3.2 to MongoDB 3.4 when the instance is running, but cannot downgrade the upgraded version.
-   During the upgrade of the database version, instances are restarted once. The upgrade is completed when instances are being restarted.
-   You can clone ApsaraDB for MongoDB instances only from those of the same database version, but not from those of different database versions.

## Storage engines {#section_rsk_bwc_bfb .section}

To meet as many requirements as possible in various business scenarios, ApsaraDB for MongoDB provides three available storage engines: WiredTiger, RocksDB, and TerarakDB. The following table lists the adaption relationships between storage engines and database versions.

|Storage engine|MongoDB 3.2|MongoDB 3.4|MongoDB 4.0|
|:-------------|:----------|:----------|:----------|
|WiredTiger| Replica set instance

 Sharded cluster instance

 | Standalone instance

 Replica set instance

 Sharded cluster instance

 | Replica set instance

 Sharded cluster instance

 |
|RocksDB|Replica set instance \(supported only when the billing method is subscription\)| Standalone instance

 Replica set instance

 |-|
|TerarkDB|-| Replica set instance

 |-|

