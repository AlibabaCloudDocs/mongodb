# Change the retention period of internal endpoints on the classic network of an ApsaraDB for MongoDB instance

This topic describes how to change the retention period of internal endpoints on the classic network of an ApsaraDB for MongoDB instance.

The instance is in hybrid network access mode. For more information, see [Configure a hybrid access solution to switch the network type of an ApsaraDB for MongoDB instance from Classic Network to VPC](/intl.en-US/User Guide/Network connection management/Configure a hybrid access solution to switch the network type of an ApsaraDB for MongoDB instance from Classic Network to VPC.md).

After an internal endpoint on the classic network expires, it is released. You can change the retention period of such an internal endpoint before it expires.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Database Connection**.

6.  In the **Retained Classic Network Address** section, click **Change Expiration Time**.

    ![Change the retention period](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0145298951/p67392.png)

7.  In the Change Expiration Time panel, select a retention period.

    **Note:** You can set the retention period to 14, 30, 60, or 120 days.

8.  Click **OK**.


