# Connect to a replica set ApsaraDB for MongoDB instance by using DMS

Data Management \(DMS\) is an integrated and visualized database solution that offers data management, structure management, user authorization, security auditing, data trend analysis, data tracking, BI charts, performance optimization, and server management. You can use DMS to connect to a standalone ApsaraDB for MongoDB instance for remote access and online management.

## Preparations

Add the IP address of the DMS server to the whitelist of the ApsaraDB for MongoDB instance based on the network type. For more information, see [Configure a whitelist for an ApsaraDB for MongoDB instance](/intl.en-US/Quick Start/Configure a whitelist for an ApsaraDB for MongoDB instance.md).

**Note:** Skip this step if you have added the IP address of the DMS server to the whitelist of the ApsaraDB for MongoDB instance.

|Network type of ApsaraDB for MongoDB instance|IP address of DMS server|
|:--------------------------------------------|:-----------------------|
|VPC|100.104.0.0/16|
|Classic network|120.55.177.0/24

121.43.18.0/24

101.37.74.0/24

10.153.176.0/24

10.137.42.0/24

11.193.54.0/24

10.152.163.0/24 |

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**.

4.  Find the target instance and click its ID.

5.  In the upper-right corner of the page, click **Log On** and select **Primary** or **Secondary**. You are redirected to the **Data Management** console.

    ![Select a node type](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2123797951/p13329.png)

    **Note:**

    -   Primary: the primary node in the replica set instance. If you connect to this node, you can perform read and write operations on the databases of the replica set instance.
    -   Secondary: the secondary node in the replica set instance. If you connect to this node, you can perform only read operations on the databases of the replica set instance.
6.  In the DMS console, enter the following information.

    ![Connect to an ApsaraDB for MongoDB instance through DMS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2123797951/p13740.png)

    |Item|Description|
    |----|-----------|
    |**Network address:Port**|The internal connection string of the Mongos node of the ApsaraDB for MongoDB instance is automatically entered.|
    |**Database Username**|Enter the database account of the MongoDB instance. The initial account is root.|
    |**Database Name**|Enter the name of the database to which the account belongs. **Note:**

    -   If **Database Username** is set to root, the database name is admin.
    -   We do not recommend that you log on to a database as the root user in the production environment. You can create users and grant permissions based on your business needs. For more information, see [Use DMS to manage ApsaraDB for MongoDB users](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md). |
    |**Password**|The password of the specified account. **Note:** If you forget the password of the root account, you can reset the password by using the method specified in [Set a password](). |

7.  Click **Login**.

    **Note:** If you want your web browser to remember the password, select **Remember password** before you click **Login**.


## Common connection scenarios

-   [Connect a local client to an ApsaraDB for MongoDB instance over the Internet](/intl.en-US/User Guide/Instance connection/Connect a local client to an ApsaraDB for MongoDB instance over the Internet.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they do not belong to the same Alibaba Cloud account](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they do not belong to the same Alibaba Cloud account.md)

## References

-   [How to troubleshoot logon issues for the mongo shell](/intl.en-US/Product Usage/Hot issues/The system prompts "Timeout while receiving message" when logging on to apsaradb for MongoDB through the Mongo Shell from a Linux instance.md)
-   [How to troubleshoot database connection failures after the number of connections reaches the upper limit](/intl.en-US/Product Usage/Hot issues/How to troubleshoot database connection failures after the number of connections reaches
         the upper limit.md)
-   [Troubleshoot the high CPU usage of ApsaraDB for MongoDB](/intl.en-US/Best Practices/Performance/Troubleshoot the high CPU usage of ApsaraDB for MongoDB.md)
-   [How to query and limit the number of connections](/intl.en-US/Product Usage/Hot issues/How to query and limit the number of connections to an apsaradb for MongoDB instance.md)

