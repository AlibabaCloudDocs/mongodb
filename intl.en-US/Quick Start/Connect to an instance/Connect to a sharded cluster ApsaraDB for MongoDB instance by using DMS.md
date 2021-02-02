# Connect to a sharded cluster ApsaraDB for MongoDB instance by using DMS

Data Management \(DMS\) is an integrated and visualized database solution that offers data management, structure management, user authorization, security auditing, data trend analysis, data tracking, BI charts, performance optimization, and server management. You can use DMS to connect to a standalone ApsaraDB for MongoDB instance for remote access and online management.

## Preparations

Add the IP address of the DMS server to the whitelist of the ApsaraDB for MongoDB instance based on the network type. For more information, see [Configure a whitelist for a sharded cluster instance]().

**Note:** Skip this step if you have added the IP address of the DMS server to the whitelist of the ApsaraDB for MongoDB instance.

|Network type of ApsaraDB for MongoDB instance|IP address of DMS server|
|:--------------------------------------------|:-----------------------|
|VPC|100.104.0.0/16|
|Classic network|120.55.177.0/24

121.43.18.0/24

101.37.74.0/24

10.153.176.0/24

10.137.42.0/24

11.193.54.0/24 |

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  In the upper-right corner of the page, click **Log On** and select a mongos node ID. You are redirected to the **Data Management** console.

    ![Select a mongos node](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8966916061/p66241.png)

6.  In the **Login instance** dialog box, configure the parameters.

    ![Log on to DMS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2934881161/p181952.png)

    |Parameter|Description|
    |---------|-----------|
    |**Database type**|The database engine of the instance. By default, this parameter is set to the database engine of the instance that you want to access.|
    |**Instance Area**|The region where the instance is deployed. By default, this parameter is set to the region where the current instance is deployed.|
    |**Connection string address**|The endpoint and port number that are used to connect to the instance. By default, this parameter is set to the endpoint and port number of the current instance.|
    |**Database Name**|The name of the database corresponding to the account if authentication is enabled. **Note:**

    -   If **Database account** is set to root, the database name is admin.
    -   We recommend that you do not log on to a database as the root user in the production environment. You can create users and grant permissions to them based on your requirement. For more information, see [Manage MongoDB users by using DMS](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md). |
    |**Database account**|The account that is used to access the database. The initial account is `root`.|
    |**Database password**|The password of the account that is used to access the database. **Note:** If you forget the password of the root account, you can reset the password by using the method specified in [Set a password](). |

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

