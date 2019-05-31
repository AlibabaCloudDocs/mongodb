# Before you start {#concept_pvf_myr_ngb .concept}

You can migrate data from a user-created MongoDB database to an ApsaraDB for MongoDB instance. You must take note of the limits of ApsaraDB for MongoDB, as shown in the following table.

|Operation|Limit|
|:--------|:----|
|Data version and storage engine|For more information, see [Data versions and storage engines](../../../../intl.en-US/Product Introduction/Versions and storage engines.md#).|
|Public IP address|Access to an instance through a public IP address may incur security risks. No public IP address is configured when an instance is created. If you need to access a MongoDB database from the Internet, you can [Apply for a public IP address](../../../../intl.en-US/User Guide/Network connection management/Apply for a public address.md#).|
|Create an instance| -   When creating a sharded cluster instance, you can select the specifications and numbers of both mongos and shards.
-   You can add mongos or shards when the instance is running. For more information, see [Change the configuration](../../../../intl.en-US/User Guide/Instance management/Change the configuration.md#).

 |
|Restart an instance|You can only restart instances from the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/) or through the API.|
|Migrate data| [Use the built-in commands of MongoDB to migrate data](intl.en-US/Quick Start for Cluster/Migrate data/Use the built-in commands of MongoDB to migrate data.md#) or [Use DTS to migrate data](intl.en-US/Quick Start for Cluster/Migrate data/Use DTS to migrate data.md#).

 |
|Back up data|[Automatic backups](../../../../intl.en-US/User Guide/Data backup/Automatically back up ApsaraDB for MongoDB data.md#) must use the physical backup method. You can select the physical or logical backup method to [Manually back up ApsaraDB for MongoDB data](../../../../intl.en-US/User Guide/Data backup/Manually back up ApsaraDB for MongoDB data.md#).|
|Restore data|If you want to restore data, you must [Create an instance based on a time point](../../../../intl.en-US/User Guide/Data recovery/Create an instance based on a time point.md#).|

