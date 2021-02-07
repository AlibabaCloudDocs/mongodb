---
keyword: [MongoDB visualizer, MongoDB data management, MongoDB graphics, obtain MongoDB database list, MongoDB database management tool, MongoDB online management, MongoDB client tool, MongoDB remote access, MongoDB client connection, MongoDB connection tool, log on to MongoDB databases by using DMS, MongoDB secure write]
---

# Manage ApsaraDB for MongoDB instances by using DMS

Data Management \(DMS\) can manage relational databases such as MySQL, SQL Server, PostgreSQL, Oracle, and OceanBase, as well as NoSQL databases such as MongoDB. DMS is an integrated data management service that offers data management, schema management, R&D, user management, permission management, and access control. You can use DMS to connect to a standalone ApsaraDB for MongoDB instance for easy management.

DMS provides the following roles:

-   DMS administrator: DMS administrators can use all system management features except for data protection.********

    **Note:** Only DMS administrators can manage users and the IP address whitelist.********

    If you assume the role of DMS administrator, you can register your ApsaraDB for MongoDB instance to DMS for management. For more information, see the [Register an ApsaraDB for MongoDB instance to DMS](#section_n3a_2pg_z11) section.

-   Security administrator: Security administrators can manage operations logs and use the data protection feature.************

    **Note:** Only security administrators can use the data protection feature.****

-   Database administrator \(DBA\): DBAs can manage instances, tasks, security rules, and configurations, and design the schema.************************
-   Common user: Common users cannot use the system management features.****

    If you assume the role of common user, you must first obtain the permission to manage your ApsaraDB for MongoDB instance. For more information, see the [Apply for permissions](#section_3qt_nhe_19z) section.


## Preparations

Add the IP addresses of DMS servers to the whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist for a standalone ApsaraDB for MongoDB instance]().

**Note:** Skip this step if you have added the IP addresses of DMS servers to the whitelist of the ApsaraDB for MongoDB instance.

|Network type of ApsaraDB for MongoDB instance|IP address of DMS server|
|---------------------------------------------|------------------------|
|VPC|100.104.0.0/16|
|Classic network|120.55.177.0/24

121.43.18.0/24

101.37.74.0/24

10.153.176.0/24

10.137.42.0/24

11.193.54.0/24 |

## Register an ApsaraDB for MongoDB instance to DMS

The following example shows how to register an ApsaraDB for MongoDB instance to DMS.

**Note:** The ApsaraDB for MongoDB instance must be registered by a DMS administrator.

1.  Log on to the [Data Management console](https://dms.aliyun.com).

2.  In the upper-left corner of the page, choose **Add instance/Batch entry** \> **Add instance**. The **Add instance** dialog box appears.

3.  On the **Cloud** tab of the Data source step, click **MongoDB**.

4.  In the **Basic Information/Advanced information** step, configure the parameters. The following table describes the parameters.

    |Section|Parameter|Description|
    |-------|---------|-----------|
    |**Basic Information**|**Data source**|The source of the database instance to add. The default value is **Cloud**.|
    |**Database type**|The cagtegory of the instance to be registered. In this example, select **MongoDB** from the drop-down list.|
    |**Instance Area**|The region where the database instance is deployed.|
    |**Entry mode**|The method that you can use to log on to the database instance. You can set this parameter only to **Connection string mode**.|
    |**Connection string address**|The endpoint of the database instance. For more information about how to view the endpoint, see [Connect to an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance connection/Connect to an ApsaraDB for MongoDB instance.md).|
    |**Database Name**|The name of the database. If the account is root, the database name is admin.|
    |**Database account**|The username that you can use to log on to the database.|
    |**Database password**|The password that you can use to log on to the database.|
    |**Control Mode**|The control mode that is used to manage the instance in DMS. For more information, see [Control modes](~~151629~~).|
    |**Advanced information**|**Environment type**|The environment of the database instance.|
    |**Instance Name**|The name of the database instance.|
    |**DBA**|The database administrator \(DBA\) of the database instance. The DBA can grant permissions to users.|
    |**query timeout\(s\)**|The timeout period for the execution of an SQL query statement. If the execution of an SQL query statement lasts longer than the specified timeout period, the execution of the statement is terminated to protect the database.|
    |**export timeout\(s\)**|The timeout interval of the statement that is used to export statistics. When the specified time interval is reached, the target statement executed in the SQL editor is stopped to protect the database security.|

5.  In the Basic Information section, click **Test connection** in the lower-left corner. Wait until the connectivity test is successful.

    **Note:** If the test fails, check the parameter values that you specified.

6.  Click **Submit**.


## Apply for permissions

For more information, see the **Apply for permissions** topic in [Permission management](~~60371~~).

