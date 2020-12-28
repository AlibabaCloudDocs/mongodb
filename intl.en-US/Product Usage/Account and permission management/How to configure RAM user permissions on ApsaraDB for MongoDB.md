# How to configure RAM user permissions on ApsaraDB for MongoDB

To implement fine-grained access control and improve account security, you can use Resource Access Management \(RAM\) to grant the management permissions on ApsaraDB for MongoDB to RAM users. In this way, RAM users can manage ApsaraDB for MongoDB instances.

## Grant permissions to RAM users

1.  Log on to the [RAM console](https://ram.console.aliyun.com/) by using an Alibaba Cloud account.
2.  [Create a RAM user](/intl.en-US/RAM User Management/Create a RAM user.md).
3.  In the left-side navigation pane, click **Users** under **Identities**.
4.  In the **User Logon Name/Display Name** column, find the target RAM user.
5.  Click **Add Permissions** in the Actions column.

    ![Add permissions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1372147751/p48650.png)

6.  In the Add Permissions dialog box that appears, select permission policies as needed.

    ![Select the required permission policies](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1372147751/p48651.png)

    1.  Enter **mongodb** in the search box to display related permission policies.

        **Note:**

        -   **AliyunMongoDBFullAccess**: grants RAM users full management permissions on ApsaraDB for MongoDB.
        -   **AliyunMongoDBReadOnlyAccess**: grants RAM users the read-only permissions on ApsaraDB for MongoDB.
    2.  Click a policy name to add it to the Selected section.
7.  Click **OK**.
8.  Click **Finished**.

## Customize permission policies in the RAM console

You can use system permission policies to grant RAM users permissions on all ApsaraDB for MongoDB resources. You can also customize permission policies as needed to grant RAM users specific operation permissions on specific instances. For information about the syntax of custom permission policies, see [Policy structure and syntax](~~93739~~).

Use RAM to grant permissions on ApsaraDB for MongoDB resources

You can only use RAM to grant permissions on ApsaraDB for MongoDB instances of the dbinstance type. When granting permissions using RAM, you can describe resources in the `Resource` field of the policy as follows.

|Resource type|Resource description in the permission policy|
|:------------|:--------------------------------------------|
|dbinstance|-   acs:dds:$regionid:$accountid:dbinstance/$dbinstanceid
-   acs:dds:$regionid:$accountid:dbinstance/
-   acs:dds:::dbinstance/ |

Parameter description

|Parameter|Description|
|---------|-----------|
|```
$regionid
```

|The region ID, which can be an asterisk \(`*`\).|
|```
$dbinstanceid
```

|The instance ID, which can be an asterisk \(`*`\).|
|```
$accountid
```

|The ID of your Alibaba Cloud account, which can be an asterisk \(`*`\).|

Actions that you can authorize

In the RAM console, you can authorize RAM users to perform the following actions on a single ApsaraDB for MongoDB resource.

|Action|Description|
|:-----|:----------|
|CreateDBInstance|Creates an instance.|
|ModifyDBInstanceSpec|Modifies instance specifications.|
|DeleteDBInstance|Deletes an instance.|
|DescribeDBInstances|Queries instances.|
|RestartDBInstance|Restarts an instance.|
|DescribeSecurityIps|Queries IP addresses in the whitelist.|
|ModifySecurityIps|Modifies IP addresses in the whitelist.|
|ResetAccountPassword|Resets the password of an account.|
|DescribeBackupPolicy|Queries the backup policy.|
|ModifyBackupPolicy|Modifies the backup policy.|
|CreateBackup|Creates a backup.|
|RestoreDBInstance|Restores an instance.|
|DescribeAccounts|Queries account information.|
|DescribeDBInstancePerformance|Queries the instance status.|
|DescribeReplicaSetRole|Queries the primary/secondary attribute of an instance.|
|ModifyDBInstanceDescription|Modifies the description of an instance.|
|ModifyAccountDescription|Modifies information about an account.|
|DescribeDBInstanceAttribute|Queries attributes of an instance.|
|RenewDBInstance|Renews an instance.|
|ModifyDBInstanceNetworkType|Modifies the network type of an instance.|

