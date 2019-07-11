# Change the number of nodes in replica set instances {#task_pwm_cfm_qfb .task}

To meet data reading performance requirements in various business scenarios, the number of nodes in a replica set instance can be changed in ApsaraDB for MongoDB. Data can be read from added secondary nodes. This method improves the overall read performance of replica set instances.

To meet the high availability of ApsaraDB for MongoDB, the number of nodes in replica set instances can be changed to 3, 5 and 7.

**Note:** The nodes of standalone instances cannot be changed.

You can add or remove nodes for a replica set instance. The number of nodes must be kept at least three however you change them. The changes to the node result in a change to the instance billing. For more information, see [Billing items and pricing](../../../../intl.en-US/Purchase guide/Billing items and pricing.md#).

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the page, select the region of the instance.
3.  In the left-side navigation pane, click **Replica Set Instances**.
4.  Locate the instance and click the instance ID.
5.  On the Basic Information page, follow these steps based on the billing method of the instance: 
    1.  For pay-as-you-go instances, click **Upgrade** or **Downgrade** in the Basic Information section.
    2.  For subscription-based instances, click **Change Configuration** in the Basic Information section.
6.  On the Change Configuration page, select **Replication Factor**. 

    **Note:** For more information about how to change specifications and storage space, see [Change the configuration](intl.en-US/User Guide/Instance management/Change the configuration.md#section_mdf_jsm_cfb).

7.  Set **Migration Time**. 

    **Note:** 

    -   **Switch Immediately After Data Migration**: After the configuration change process is completed, the instance immediately enters the **Changing Configuration** state. The configuration is successfully changed when the status of the instance changes to the **Running** status.

        During some configuration upgrades, the instance may be disconnected for less than 30s once or twice. You can set the effective time for the configuration change as required to avoid negative effects on your business.

    -   **Migrate at Scheduled Time**: You can set the time for the configuration change within a specified period. For more information, see Specify a maintenance period.

        If the network of an instance is not disconnected during the configuration change, the configuration change can immediately take effect regardless of whether you have set the migration time.

8.  Select **ApsaraDB for MongoDB Agreement of Service** and follow the instructions to complete the payment.

After you add the nodes for the replica set instances, the connection addresses of new nodes \(all displayed as Secondary, only different for role IDs\) appear in the console. The connection string URI for a high availability connection is also updated. You can modify the connection address in an application to achieve high availability and read/write splitting connection and improve the overall performance. For more information, see [Connect to a replica set instance through the mongo shell](../../../../intl.en-US/Quick Start for Replica Set/Connect to an instance/Connect to an replica set instance through the mongo shell.md#).

