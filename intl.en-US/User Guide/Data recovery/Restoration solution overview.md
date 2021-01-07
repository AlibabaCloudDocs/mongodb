# Restoration solution overview

The data restoration feature of ApsaraDB for MongoDB can minimize any losses caused by incorrect operations on databases. ApsaraDB for MongoDB provides many data restoration solutions to meet requirements in different scenarios.

## Restore data to ApsaraDB for MongoDB instances

|Method|Instance type|Scenario|Remarks|
|:-----|:------------|--------|:------|
|[Create an instance from a backup](/intl.en-US/User Guide/Data recovery/Create an instance from a backup.md)|Standalone or replica set instance|Applicable to the scenarios where the entire instance is restored and data timeliness is not a key requirement.|A new instance is created based on the backup data and data is restored to the new instance. **Note:**

-   The created instance will be billed. For more information, see [Billing items and pricing](~~54285~~).
-   To ensures better performance and stability of the instance, the system will upgrade the minor version to the latest version by default If the minor version of your instance expires or is not included in the maintenance list and the instance is [upgraded](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md), [migrated](/intl.en-US/User Guide/Data migration and synchronization/Overview.md), [changed](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md), [Created from a backup](/intl.en-US/User Guide/Data recovery/Create an instance from a backup.md), [Created by point-in-time](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance by point in time.md), or performed [Restore data to a new ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance.md). |
|[Create an instance based on a point in time](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance by point in time.md)|Replica set or sharded cluster instance|Applicable to the scenarios where multiple databases or the entire instance is restored. The data at a specified point in time will be restored.|
|[Restore data to a new ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance.md)|Replica set instance|Applicable to the scenarios where one or more databases are quickly restored. For example, a data set or document is deleted by mistake.|
|[Restore backup data to the current instance](/intl.en-US/User Guide/Data recovery/Restore data to the current ApsaraDB for MongoDB instance.md)|Replica set instance \(three-node\)|N/A|Restoring data directly to the current instance poses high risks. We recommend that you restore the data by using the following feature: [Restore data to a new ApsaraDB for MongoDB instance by point in time](/intl.en-US/User Guide/Data recovery/Restore data to a new ApsaraDB for MongoDB instance by point in time.md) or [Create an instance from a backup](/intl.en-US/User Guide/Data recovery/Create an instance from a backup.md). After the data is validated, migrate the data back to the original instance through DTS.|

## Restore data to user-created databases

You can download backup files of ApsaraDB for MongoDB to your server and recover the data to a user-created database. This feature is applicable to scenarios such as business testing or data analysis.

|Method|Instance type|
|:-----|:------------|
|[Restore logical backup files of ApsaraDB for MongoDB to user-created databases](/intl.en-US/User Guide/Data recovery/Restore data of an ApsaraDB for MongoDB instance to user-created MongoDB databases by using logical backup.md)|Replica set instance|
|[Restore physical backup files of ApsaraDB for MongoDB to user-created databases](/intl.en-US/User Guide/Data recovery/Recover physical backup data in a user-created MongoDB instance/Restore data of an ApsaraDB for MongoDB instance to user-created MongoDB databases by using physical backup.md)|Replica set instance|

