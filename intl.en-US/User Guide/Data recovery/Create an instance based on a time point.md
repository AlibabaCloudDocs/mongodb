# Create an instance based on a time point {#task342 .task}

ApsaraDB for MongoDB allows you to create an instance based on a running time point of an existing instance. The data of the new instance is recovered from that of the existing instance at the selected time point. This method applies to data recovery or data verification scenarios.

-   The existing instance must be a replica set or sharded cluster instance.

    **Note:** Standalone instances do not support this feature.

-   Currently, you can select a time point only in the last seven days.
-   If you create an instance based on a time point, you need to pay for the created instance. For more information about how to bill an instance, see [Billing items and pricing](../../../../intl.en-US/Purchase guide/Billing items and pricing.md#).
-   To create a Pay-As-You-Go instance, ensure that your account balance is sufficient.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/). 
2.  In the upper-left corner of the home page, select the region where the target instance is located. 
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance. 
4.  Locate the target instance and click its instance ID. 
5.  In the left-side navigation pane, click **Backup and Recovery**. 
6.   On the Backup and Recovery page that appears, click **Create Instance By Time Point**. 
7.  In the **Create Instance By Time Point** dialog box that appears, select the target time point and click **OK**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6724/155618061721489_en-US.png)

8.  On the ApsaraDB for MongoDB instance creation page that appears, select the billing method of the instance to be created. 
9.  Set parameters for the instance as required. 

    **Note:** 

    -   Replica set instance: The storage space of the new instance must be larger than or equal to that of the existing instance.
    -   Sharded cluster instance:
        -   The number of shards for the new instance must be greater than or equal to that for the existing instance.
        -   The storage space of each shard for the new instance must be larger than or equal to that for the existing instance.
10. Click **Buy Now** to go to the Confirm Order page. 
11. Read and select **ApsaraDB for MongoDB Agreement of Service** and follow the instructions to complete the payment process. 

