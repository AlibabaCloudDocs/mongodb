# Reset the password for an ApsaraDB for MongoDB instance

This topic describes how to reset the password for an ApsaraDB for MongoDB instance. If you forget your password or did not set the password when you created an instance, you can reset the password for the instance.

## Limits

You can reset the password only for the root account or an account for a shard or Configserver node.

**Note:** If you want to manage database accounts created by running the `db.createUser` command, you can use Data Management \(DMS\) or the mongo shell. For more information, see [Manage user permissions on MongoDB databases](/intl.en-US/User Guide/Account management/Manage user permissions on MongoDB databases.md) or [Connect to a replica set instance by using the mongo shell](/intl.en-US/Quick Start/Connect to an instance/Connect to a replica set instance by using the mongo shell.md).

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Accounts**.

6.  Perform one of the following operations based on your account type:

    -   Reset the password of the root account.

        Find the root account and click **Reset Password** in the **Actions** column.

    -   Reset the password of an account for a shard or Configserver node in a sharded cluster instance.

        **Note:** If no endpoints are obtained for the shard or Configserver node, this operation cannot be performed. For more information about how to obtain the endpoints, see [Apply for a connection string of a shard or Configserver node](/intl.en-US/User Guide/Network connection management/Connection String of a Shard or Configserver Node/Apply for a connection string of a shard or Configserver node.md).

        Find the account created when you apply for an endpoint for a shard or Configserver node, and click **Reset Password** in the **Actions** column. In this example, find shardaccount. For more information, see [Apply for a connection string of a shard or Configserver node](/intl.en-US/User Guide/Network connection management/Connection String of a Shard or Configserver Node/Apply for a connection string of a shard or Configserver node.md).

7.  In the panel that appears, enter the password in the **New Password** field and enter the password again in the **Confirm New Password** field.

    **Note:**

    -   The password must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include

        ! \# $ % ^ & \* \( \) \_ + - =

    -   The password must be 8 to 32 characters in length.
8.  Click **OK**.


