# MongoDB versions and storage engines

ApsaraDB for MongoDB supports MongoDB 4.2, 4.0, and 3.4 and the WiredTiger storage engine. You can select the appropriate MongoDB version and storage engine when you create an instance.

## MongoDB versions and descriptions

MongoDB 4.4 overcomes the most obvious problems with previous versions. MongoDB 4.2 uses the two-phase commit method to ensure the ACID feature of sharded cluster transactions and expand business scenarios. MongoDB 4.0 is more applicable to financial and other scenarios that are dependent on transactions and use NoSQL features. Compared with MongoDB 3.2, MongoDB 3.4 provides higher performance and security. The following sections describe different MongoDB versions.

**Note:** MongoDB 3.2 has been unavailable. For more information, see [Notice: ApsaraDB for MongoDB has phased MongoDB 3.2 out and released MongoDB 4.2 since February 4](/intl.en-US/Product Notification/Notice: ApsaraDB for MongoDB has phased MongoDB 3.2 out and released MongoDB 4.2 since
         February 4.md).

MongoDB 4.2

-   Distributed transactions

    The two-phase commit method ensures the ACID feature of sharded cluster transactions, expands business scenarios, and achieves a leap from NoSQL to NewSQL.

-   Repeatable reads

    The repeatable read feature provides the automatic retry capability in a poor-quality network environment. This reduces logic complexity at the service side and ensures continuity of your business.

-   Wildcard indexes

    You can create a wildcard index for nondeterministic fields to overwrite multiple feature fields in a document for flexible management and usage.

-   Field-level encryption

    Field-level encryption is supported at the driver layer and can be used to separately encrypt specified sensitive information such as accounts, passwords, prices, and mobile phone numbers. You can use field-level encryption to make business more flexible and secure without full-database encryption.

-   Materialized views

    Latest materialized views can cache computing results to make computing more efficient and logic less complex.


MongoDB 4.0

-   Cross-document transactions

    As the first NoSQL database that supports cross-document transactions, MongoDB 4.0 combines the speed, flexibility, features, and ACID guarantee of document models.

-   Migration speed increase by 40%

    Concurrent read and write operations enable new shard nodes to migrate data fast and bear service loads.

-   Read performance significantly improved

    The transaction feature ensures that secondary nodes no longer block read requests due to log synchronization. The multi-node scaling feature is supported in all versions to significantly improve reading capabilities.


MongoDB 3.4

-   Faster synchronization between the primary and secondary nodes

    All indexes are created when data is synchronized \(only the \_id index is created in earlier versions\). During data synchronization, the secondary node continuously reads new oplog information to ensure that the local database of the secondary node has enough space to store temporary data.

-   More efficient load balancing

    In earlier versions, Mongos nodes are responsible for load balancing of sharded cluster instances. Multiple Mongos nodes contest a distributed lock. The node that obtains the lock performs load balancing tasks and migrates chunks between shard nodes. In MongoDB 3.4, the primary Configserver node is responsible for load balancing. This greatly improves the concurrency and efficiency of load balancing.

-   More aggregation operations

    Many aggregation operators are added in MongoDB 3.4 to provide more powerful data analysis capabilities. For example, `bucket` can conveniently classify data. `$grahpLookup` supports more complex relational operations than `$lookup` in MongoDB 3.2. `$addFields` enables richer document operations such as summing some fields and saving them as a new field.

-   Sharding zones supported

    The zone concept is introduced for sharded cluster instances to replace the current tag-aware sharding mechanism. The zone feature can allocate data to one or more specified shard nodes. This feature allows you to conveniently deploy sharded cluster instances across data centers.

-   Collation supported

    In earlier versions, strings stored in documents are always compared byte by byte regardless of Chinese, English, uppercase, or lowercase. After collation is introduced, the string content can be interpreted or compared based on the used locale. Case-insensitive comparison is also supported.

-   Read-only views

    MongoDB 3.4 supports read-only views. MongoDB 3.4 virtualizes the data that meets a query condition into a special collection, on which you can perform further queries.


**Note:** You can manually upgrade the MongoDB version while an instance is running. However, you cannot downgrade the MongoDB version. For more information, see [Upgrade MongoDB versions](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md).

## Storage engines

|Storage engine|Description|Application scenario|
|--------------|-----------|--------------------|
|WiredTiger|Data is in the B-tree structure. Compared with the earlier MMAPv1 storage engine, WiredTiger significantly improves performance and reduces storage costs while data compression is supported.|It is the default storage engine and applicable to most business scenarios.|

## Relationship between MongoDB versions and storage engines

The following tables describe the relationship between MongoDB versions and storage engines.

|Storage engine|MongoDB 4.2|MongoDB 4.0|MongoDB 3.4|
|:-------------|:----------|:----------|:----------|
|WiredTiger|Replica set instance

Sharded cluster instance

Serverless instance

|Standalone instance

Replica set instance

Sharded cluster instance

|Standalone instance

Replica set instance

Sharded cluster instance |

