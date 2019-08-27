# Before you start {#concept_66101_zh .concept}

You can migrate data from a user-created MongoDB instance to an ApsaraDB for MongoDB instance. Before using ApsaraDB for MongoDB, you need to pay attention to its constraints, as listed in the following table.

|Operation|Constraints|
|:--------|:----------|
|Restart an instance|You must log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) or call the RestartDBInstance operation to restart an instance.|
|Select the database version|Currently, standalone instances support only MongoDB 3.4.|
|Select the storage engine| -   You can select WiredTiger or RocksDB.
-   Standalone instances do not support TerarkDB.

 |
|Select the region|Standalone instances are supported in China \(Hangzhou\), China \(Shanghai\), China \(Qingdao\), China \(Beijing\), and China \(Shenzhen\).|

