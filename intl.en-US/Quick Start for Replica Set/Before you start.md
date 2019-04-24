# Before you start {#concept_54260_zh .concept}

You can easily migrate data from a user-created MongoDB instance to an ApsaraDB for MongoDB instance. Before using ApsaraDB for MongoDB, you need to pay attention to its constraints, as listed in the following table.

|Operation|Constraints|
|:--------|:----------|
|Restart an instance|You must log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) or call the RestartDBInstance operation to restart an instance.|
|Create a replica set| -   A replica set automatically created by ApsaraDB for MongoDB consists of an operable primary node, a hidden secondary node \(invisible to you\), and the other operable secondary nodes.
-   You can select the number of nodes \(such as three, five, or seven nodes\) based on business requirements to increase or decrease secondary nodes on demand.

 |
|Migrate data| -   We recommend that you use [Data Transmission Service \(DTS\)](intl.en-US/Quick Start for Replica Set/Migrate data/Use DTS to migrate data.md#) to migrate data.
-   You can also use [the built-in commands of MongoDB](intl.en-US/Quick Start for Replica Set/Migrate data/Use the built-in commands of MongoDB to migrate data.md#) to migrate data.

 |
|Select the database version and storage engine|For more information, see [Versions and storage engines](../../../../intl.en-US/Product Introduction/Versions and storage engines.md#).|

