# Manage user permissions on MongoDB databases

In Data Management \(DMS\), you can manage users for MongoDB databases and grant the users the permissions of different roles. The roles are **Common operation role**, **Administrator action role**, **Instance-level role**, **Cluster administrator role**, **Backup and Recovery roles**, and Super role.

-   A MongoDB database is registered in DMS.
-   You are assigned a required role for the MySQL database instance that is registered in DMS. The role varies based on the control mode of the instance. The following table describes the details.

    |Control mode|Role requirement|
    |------------|----------------|
    |Security Collaboration|You must be a DMS administrator, a database administrator \(DBA\), or the owner of the relevant database instance.|
    |Stable Change|No specific role is required.|
    |Flexible Management|No specific role is required.|


## Create a user

1.  Log on to the [DMS console](https://dms.alibabacloud.com/).

2.  In the search box at the top of the left-side navigation pane, enter the name of the MySQL database whose permissions you want to manage. From the matched result, find the instance to which the database belongs.

3.  Right-click the instance and select **Account Management**.

    ![Account Management](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4629280061/p146079.png)

4.  On the **Account Management** page, select a database from the drop-down list.

    ![Select a database from the drop-down list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8607711061/p166287.png)

5.  Click **Create User** in the upper-left corner.

6.  In the **Create User** dialog box, set relevant parameters.

    ![Create User dialog box](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9607711061/p165556.png)

    1.  Configure user information. Set the parameters as described in the following table.

        |Parameter|Description|
        |:--------|:----------|
        |Target Database|The database for which you want to create the user. **Note:**

        -   If you select a database other than the admin database, the user to be created is a common user.
        -   If you select the **admin** database, the user to be created is a privileged user. |
        |User name|The name of the user.         -   The name cannot contain Chinese characters.
        -   It can contain letters, digits, and special characters.
        -   The name can contain the following special characters:

!\#$%^&\*\(\)\_+-= |
        |Password|The password that the user can use to log on to the database. To ensure data security, the password can be 8 to 32 characters in length and must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters.

The password can contain the following special characters:

!\#$%^&\*\(\)\_+-= |
        |Confirm Password|The password that the user can use to log on to the database. Enter the same password again to confirm the password.|

    2.  Grant permissions to the user.

        **Note:**

        -   Assume that you select the admin database:

            On the **Current library permissions** tab, you can grant permissions of different roles to the user. The roles are **Common operation role**, **Administrator action role**, **Instance-level role**, **Cluster administrator role**, **Backup and Recovery roles**, and **Super role**. For more information, see [Permissions of different roles](#d7e248).

            On the **Other library permissions** tab, you can grant permissions on other databases in the current instance to the user.

        -   Assume that you select a database other than the admin database:

            On the **Current library permissions** tab, you can grant permissions of **Common operation role** and **Administrator action role** to the user. For more information, see [Permissions of different roles](#d7e248).

            You cannot grant permissions on other databases to the user on the **Other library Permissions** tab.

7.  In the Create User dialog box, click **OK**.

    **Note:** If the database instance is in Security Collaboration mode, SQL statements can be generated based on the parameters you set. However, the SQL statements may fail to be executed due to security rules. In this case, you can perform operations as prompted or contact the DBA or DMS administrator.


## Edit a user

1.  Log on to the [DMS console](https://dms.alibabacloud.com/).

2.  In the search box at the top of the left-side navigation pane, enter the name of the MySQL database whose permissions you want to manage. From the matched result, find the instance to which the database belongs.

3.  Right-click the instance and select **Account Management**.

4.  On the **Account Management** page, select a database from the drop-down list.

5.  Find the user whose information you want to edit and click **Edit** in the **Operation** column.

    ![Edit](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9607711061/p166289.png)


## Delete a user

1.  Log on to the [DMS console](https://dms.alibabacloud.com/).

2.  In the search box at the top of the left-side navigation pane, enter the name of the MySQL database whose permissions you want to manage. From the matched result, find the instance to which the database belongs.

3.  Right-click the instance and select **Account Management**.

4.  On the **Account Management** page, select a database from the drop-down list.

5.  Find the user who you want to delete and click **Delete** in the **Operation** column.

6.  In the Prompt message, click **OK**.


## Permissions of different roles

The following table describes the permissions of different roles. For more information, see [MongoDB official website](https://docs.mongodb.com/manual/reference/built-in-roles/).

|Role|Permission|Description|
|----|----------|-----------|
|Common operation role|read|Enables a user to query data in the database.|
|readWrite|Enables a user to insert, delete, update, or query data in the database.|
|Administrator action role

|dbAdmin|Enables a user to manage data in the database, but not to read data from or write data to the database.|
|userAdmin|Enables a user to create users for the database.|
|dbOwner|Enables a user to perform all operations on the database.|
|Instance-level role|readAnyDatabase|Enables a user to query data in all databases of the instance.|
|readWriteAnyDatabase|Enables a user to insert, delete, update, or query data in all databases of the instance.|
|userAdminAnyDatabase|Enables a user to create users for all databases of the instance.|
|dbAdminAnyDatabase|Enables a user to manage data in all databases of the instance, but not to read data from or write data to the databases.|
|Cluster administrator role|hostManager|Enables a user to manage data in the database, but not to read data from or write data to the database.|
|clusterMonitor|Enables a user to query clusters and replication sets.|
|clusterManager|Enables a user to manage and monitor clusters and replication sets.|
|clusterAdmin|Enables a user to perform all operations on clusters.|
|Backup and Recovery roles|backup|Enables a user to query data in all databases of the instance.|
|restore|Enables a user to insert, delete, update, or query data in all databases of the instance.|
|Super role|Root|Enables a user to perform all operations on all resources in an instance.|

