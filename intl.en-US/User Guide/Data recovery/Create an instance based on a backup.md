# Create an instance based on a backup {#task_tll_y3b_kfb .task}

ApsaraDB for MongoDB allows you to create an instance based on a backup of an existing instance. The data of the new instance is recovered from that of the selected backup. This method applies to data recovery or data verification scenarios.

-   The existing instance must be a standalone or replica set instance.

    **Note:** Sharded cluster instances do not support this feature.

-   Currently, you can select a backup only in the last seven days.
-   If you create an instance based on a backup, you need to pay for the created instance. For more information about how to bill an instance, see [Billing items and pricing](../../../../intl.en-US/Purchase guide/Billing items and pricing.md#).
-   To create a Pay-As-You-Go instance, ensure that your account balance is sufficient.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances**.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, click **Backup and Recovery**.
6.  On the Backup and Recovery page that appears, locate the target backup and choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6723/155618027513851_en-US.png)** \> **Create Instance from Backup Point** in the Operation column. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6723/155618027513850_en-US.png)

7.  On the ApsaraDB for MongoDB instance creation page that appears, select the billing method of the instance to be created.
8.  Set parameters for the instance as required. 

    **Note:** The storage space of the new instance must be larger than or equal to that of the existing instance.

9.  Click **Buy Now** to go to the Confirm Order page.
10. Read and select **ApsaraDB for MongoDB Agreement of Service** and follow the instructions to complete the payment process.

