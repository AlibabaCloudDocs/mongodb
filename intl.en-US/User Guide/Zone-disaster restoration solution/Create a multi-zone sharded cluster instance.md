# Create a multi-zone sharded cluster instance

This topic describes how to create a multi-zone sharded cluster instance. ApsaraDB for MongoDB provides a zone-disaster recovery solution to ensure the reliability and availability of your sharded cluster instance. This solution deploys the components of a sharded cluster instance across three different zones within one region. The components in these zones exchange data over an internal network. When one of the three zones becomes unavailable due to unexpected events such as a power or network failure, the high availability \(HA\) system automatically switches services over to another zone.

## Precautions

You can create multi-zone sharded cluster instances only in some regions. The actually supported regions are displayed in the console.

![Multi-zone sharded cluster instance 2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5962854161/p232868.png)

**Note:** On the instance buy page, you can select a **region** and view all the zones that support multi-zone deployment within the region in the **Zone** drop-down list. The name of such a zone contains multiple uppercase letters, as shown in the preceding figure.

## Node deployment policies

If you use the single-zone deployment solution, the system deploys all components of the sharded cluster instance to one zone. If you use the multi-zone deployment solution, the system deploys all components to three different zones.

-   mongos is evenly deployed across all data centers. At least two mongos are deployed at a time, with each to one zone. When you add a third mongos, the system deploys it to the third zone. Each new mongos added later is deployed to one of the three zones in turn.
-   The primary, secondary, and hidden shards in each shard are not deployed to the three zones in sequence. The deployment of these shards may change when manual switchover or HA failover between primary and secondary shards is triggered.

![](../images/p46749.png "Deployment policy for the components in a multi-zone sharded cluster instance")

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the left-side navigation pane, click **Sharded Cluster Instances**.

3.  On the **Sharded Cluster Instances** page, click **Create Instance**.

4.  Click **Sharded Cluster \(Pay-as-you-go\)** or **Sharded Cluster \(Subscription\)**.

    **Note:**

    -   Subscription: You must pay for an instance when you create it. This method is more cost-effective than the pay-as-you-go method. We recommend that you select this method for long-term use. A longer subscription period enables a larger discount.
    -   Pay-as-you-go: You are billed on an hourly basis based on the used resources. We recommend that you select this billing method for short-term use. You can reduce costs by releasing your pay-as-you-go instance after you no longer need it.
5.  Select a **region** that supports multi-zone deployment and select a zone.

6.  Configure other parameters. For more information, see [Create a sharded cluster instance](/intl.en-US/Quick Start/Create an instance/Create a sharded cluster instance.md).

7.  Click **Buy Now** to go to the Confirm Order page.

8.  On the Confirm Order page, read and select ApsaraDB for MongoDB Agreement of Service and complete the payment.


## References

You can use the Service Availability feature to view the distribution of nodes in a sharded cluster instance across zones. You can also switch the node roles of the instance based on your business deployment. This way, your applications can connect to the closest nodes. For more information, see [Switch node roles](/intl.en-US/User Guide/Instance management/Switch node roles.md).

