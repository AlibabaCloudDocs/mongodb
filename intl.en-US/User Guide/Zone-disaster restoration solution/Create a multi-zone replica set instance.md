# Create a multi-zone replica set instance

This topic describes how to create a multi-zone replica set instance. ApsaraDB for MongoDB provides a zone-disaster recovery solution to ensure the reliability and availability of your replica set instance. This solution deploys the nodes of a three-node replica set instance to three different zones in one region. The nodes in these zones exchange data over an internal network. When one of the three zones becomes unavailable due to unexpected events such as a power or network failure, the high-availability \(HA\) system automatically switches services over to another zone.

## Notes

-   You can create multi-zone replica set instances only in some regions. For more information about the supported regions, see the ApsaraDB for MongoDB console.
-   When you create a multi-zone replica set instance, you must set **Replication Factor** to **Three Nodes Replica set**.

    **Note:** If you need more nodes, you can change the number of nodes after you create the instance. For more information, see [Change the number of nodes for a replica set instance](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Change the number of nodes for a replica set instance.md).


## Node deployment policies

|Deployment|Description|
|----------|-----------|
|Single-zone deployment|The system deploys the primary, secondary, and hidden nodes in one zone.![Single-zone deployment](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8645298951/p33038.png) |
|Multi-zone cluster|The system deploys the primary, secondary, and hidden nodes in three different zones.![Multi-zone deployment](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8645298951/p39357.png) |

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the left-side navigation pane, click **Replica Set Instances**.

3.  On the **Replica Set Instances** page, click **Create Instance**.

4.  Click **Replica Set \(Subscription\)** or **Replica Set \(Pay-as-you-go\)**.

    **Note:**

    -   Subscription: You must pay for an instance when you create it. This method is more cost-effective than the pay-as-you-go method. We recommend that you select this method for long-term use. A longer subscription period enables a larger discount.
    -   Pay-as-you-go: You are billed on an hourly basis based on the used resources. We recommend that you select this billing method for short-term use. You can reduce costs by releasing your pay-as-you-go instance after you no longer need it.
5.  Set **Region** to **China \(Hangzhou\)**, **China \(Beijing\)**,**China \(Shenzhen\)**, or**Singapore \(Singapore\)**. Then, select a multi-zone configuration from the Zone drop-down list.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8645298951/p33041.png)

6.  Configure other parameters. For more information, see [Create a replica set instance](/intl.en-US/Quick Start/Create an instance/Create a replica set instance.md).

7.  Click **Buy Now** to go to the Confirm Order page.

8.  On the Confirm Order page, read and select ApsaraDB for MongoDB Agreement of Service and complete the payment.


## References

You can use the service availability feature to view the distribution of nodes in a replica set instance across zones. You can also switch the node roles of the instance based on your business deployment. This way, your applications can connect to the nodes closest to them. For more information, see [Switch node roles](/intl.en-US/User Guide/Instance management/Switch node roles.md).

