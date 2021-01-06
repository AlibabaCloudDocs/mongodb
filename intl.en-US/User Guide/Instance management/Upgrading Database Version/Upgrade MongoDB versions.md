# Upgrade MongoDB versions

This topic describes how to upgrade the MongoDB version of an instance in the ApsaraDB for MongoDB console. ApsaraDB for MongoDB supports MongoDB 3.2, 3.4, 4.0, and 4.2.

## MongoDB versions

For more information about the MongoDB versions supported by ApsaraDB for MongoDB, see [Versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).

## MongoDB versions for upgrade

|Instance architecture|Before upgrade|After upgrade|Description|
|:--------------------|:-------------|:------------|:----------|
|Standalone instance|3.4 and 4.0|-

|Upgrade to MongoDB 4.0 is not supported. If you need an ApsaraDB for MongoDB instance with MongoDB 4.0, select the version while you create the instance. For more information, see [Create a standalone instance](/intl.en-US/Quick Start/Create an instance/Create a standalone instance.md).|
|Replica set instance|3.2 \(phased-out\), 3.4, 4.0, and 4.2|3.4, 4.0, and 4.2|N/A|
|Sharded cluster instance|3.2 \(phased-out\), 3.4, 4.0, and 4.2|3.4, 4.0, and 4.2|N/A|

**Note:** For more information about the features in each version, see [MongoDB versions and descriptions](/intl.en-US/Product Introduction/MongoDB versions and storage engines.mdsection_okn_x4c_bfb).

## Precautions

-   The duration of upgrading the MongoDB version of an instance is related to the data volume of databases in this instance. We recommend that you schedule your upgrade task during off-peak hours.
-   You cannot downgrade the MongoDB version an instance after you upgrade it.
-   If the minor version of your instance expires or is not included in the maintenance list and the instance is upgraded, migrated, changed, or cloned, the system will upgrade the minor version to the latest version by default. This ensures better performance and stability of the instance.

## Notes

-   Nodes in an instance are upgraded in turn. An instance is automatically restarted two or three times during an upgrade. We recommend that you perform the upgrade during off-peak hours or make sure that your application is configured to connect to the instance after it is disconnected.

    **Note:** If your application runs in a production environment, we recommend that you use a connection string URI to connect your application to the instance. In this way, the read/write operations of your application remain available even if a node fails as a result of a primary/secondary switchover. For more information, see [Overview of replica set instance connections]() or [Overview of sharded cluster instance connections]().

-   The balancer of a sharded cluster instance is disabled during an upgrade and is enabled after the upgrade.

## Procedure

1.  On the Basic Information page, click **Upgrade Database Version** and select the target version.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6735298951/p21044.png)

2.  In the Upgrade Database Version message that appears, click **OK**.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6735298951/p21045.png)

    The instance status changes to **Upgrading**. When the instance enters the **Running** state, the upgrade is complete.


