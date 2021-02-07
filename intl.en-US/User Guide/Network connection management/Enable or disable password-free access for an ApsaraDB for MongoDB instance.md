# Enable or disable password-free access for an ApsaraDB for MongoDB instance

This topic describes how to enable or disable password-free access over a VPC for an ApsaraDB for MongoDB instance. This makes database connections easy and secure. After password-free access is enabled, the ECS instance that shares the same VPC with the ApsaraDB for MongoDB instance can connect to a database of this ApsaraDB for MongoDB instance without a password. You can still use a database username and its password to connect to this database.

## Prerequisites

-   A replica set or sharded cluster instance is used.
-   The database engine version of the instance is 4.0 \(with the minor version of mongodb\_20190408\_3.0.11 or later\) or 4.2. If your database engine is earlier than the required version, upgrade the instance. For more information, see [Upgrade MongoDB versions](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md) and [Upgrade the minor version of an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade the minor version of an ApsaraDB for MongoDB instance.md).

    **Note:** You can view the database engine version and the minor version on the **Basic Information** page in the ApsaraDB for MongoDB console.

-   The network type of the instance must be VPC. If the network type is classic network, switch it to VPC. For more information, see [Switch from classic network to VPC](/intl.en-US/User Guide/Network connection management/Switch the network type of an ApsaraDB for MongoDB instance.md).

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connection**.

6.  In the upper-right corner of the Intranet Connection - VPC section, click **Enable password-free access** or **Disable password-free access**.

    -   Enable password-free access.

        ![Enable password-free access](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4045298951/p45177.png)

        After password-free access is enabled, the [ECS](~~25367~~) instance that shares the same VPC with the ApsaraDB for MongoDB instance can connect to a database of this ApsaraDB for MongoDB instance without a password. You can still use a database username and its password to connect to this database.

        **Note:** If you want to connect to a database of an ApsaraDB for MongoDB instance without entering a password, add the IP address of your client to a whitelist of this instance. For more information, see [Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).

        The following command provides an example of a password-free connection by using the mongo shell:

        ```
        mongo --host dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717
        ```

    -   Disable password-free access.

        **Note:** After password-free access is disabled, the applications that have established connections with a database of this ApsaraDB for MongoDB instance are disconnected. You must change the database connection mode for your application before you disable password-free access.

        ![Disable password-free access](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4045298951/p45178.png)

7.  In the message that appears, click **OK**.


## References

|API|Description|
|---|-----------|
|[ModifyInstanceVpcAuthMode](/intl.en-US/API Reference/Connection Management/ModifyInstanceVpcAuthMode.md)|Enables or disables password-free access over a VPC for an ApsaraDB for MongoDB instance.|

