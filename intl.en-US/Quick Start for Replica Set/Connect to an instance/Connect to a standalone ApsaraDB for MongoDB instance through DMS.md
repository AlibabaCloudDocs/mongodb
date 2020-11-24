# Connect to a standalone ApsaraDB for MongoDB instance through DMS

Data Management \(DMS\) is an integrated database solution that offers data management, structure management, user authorization, security auditing, data trend analysis, data tracking, BI charts, performance optimization, and server management. You can use DMS to connect to a standalone ApsaraDB for MongoDB instance for easy management.

## Preparations

Add the IP address of the DMS server \(100.104.0.0/16\) to the whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist for a standalone ApsaraDB for MongoDB instance](/intl.en-US/Quick Start for Standalone/Configure a whitelist for a standalone ApsaraDB for MongoDB instance.md).

**Note:** Skip this step if you have added the IP address of the DMS server to the whitelist of the ApsaraDB for MongoDB instance.

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  Click **Log On** and select **Primary** or **Secondary** in the upper-right corner of the Basic Information page . You are redirected to the DMS console.

    **Note:**

    -   Primary: the primary node of the replica set instance. This node has read/write permissions on the database.
    -   Secondary: the secondary node of the replica set instance. This node only has read permissions on the database.
6.  In the DMS console, enter the following information.

    ![Connect to an ApsaraDB for MongoDB instance through DMS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2123797951/p13740.png)

    |Item|Description|
    |----|-----------|
    |**Network address:Port**|The internal connection string of the primary node of the ApsaraDB for MongoDB instance is automatically entered.|
    |**Database Username**|Enter the database account of the MongoDB instance. The initial account is root.|
    |**Database Name**|Enter the name of the database to which the account belongs. **Note:**

    -   If **Database Username** is set to root, the database name is admin.
    -   We do not recommend that you log on to a database as the root user in the production environment. You can create users and grant permissions based on your business needs. For more information, see [Use DMS to manage ApsaraDB for MongoDB users](). |
    |**Password**|The password of the specified account. **Note:** If you forget the password of the root account, you can reset the password by using the method specified in [Set a password](/intl.en-US/Quick Start for Standalone/Set a password for a standalone ApsaraDB for MongoDB instance.md). |

7.  Click **Log On**.


## Common connection scenarios

-   [Connect a local client to an ApsaraDB for MongoDB instance over the Internet](/intl.en-US/User Guide/Instance connection/Connect a local client to an ApsaraDB for MongoDB instance over the Internet.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they do not belong to the same Alibaba Cloud account](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they do not belong to the same Alibaba Cloud account.md)

## FAQ

-   [How to troubleshoot logon issues for the mongo shell](/intl.en-US/Product Usage/Hot issues/The system prompts "Timeout while receiving message" when logging on to apsaradb for MongoDB through the Mongo Shell from a Linux instance.md)
-   [How to troubleshoot database connection failures after the number of connections reaches the upper limit](/intl.en-US/Product Usage/Hot issues/Database connection failures caused by exhausted connections to apsaradb for MongoDB instances.md)
-   [Troubleshoot high CPU utilization of ApsaraDB for MongoDB](/intl.en-US/Best Practices/Performance/Troubleshoot the high CPU usage of ApsaraDB for MongoDB.md)
-   [How to query and limit the number of connections](/intl.en-US/Product Usage/Hot issues/How to query and limit the number of connections to an apsaradb for MongoDB instance.md)

