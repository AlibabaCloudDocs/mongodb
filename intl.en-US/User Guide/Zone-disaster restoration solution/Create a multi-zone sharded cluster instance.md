# Create a multi-zone sharded cluster instance

This topic describes how to create a multi-zone sharded cluster instance. ApsaraDB for MongoDB provides a zone-disaster recovery solution to ensure the reliability and availability of your sharded cluster instance. This solution deploys the components of a sharded cluster instance across three different zones in one region. The components in these zones exchange data over an internal network. When one of the three zones becomes unavailable due to unexpected events such as a power or network failure, the high-availability \(HA\) system automatically switches over services to another zone.

## Precautions

You can create a multi-zone sharded cluster instance only in some regions. For more information about the supported regions, see the ApsaraDB for MongoDB console.

## Node deployment policies

If you use the single-zone deployment solution, the system deploys all components of the sharded cluster instance to one zone. If you use the multi-zone deployment solution, the system deploys all components to three different zones.

-   The mongos nodes are evenly deployed across all data centers. At least two mongos nodes are deployed at a time, with each to one zone. When you add a third mongos node, the system deploys it to the third zone. Each new mongos node added later is deployed to one of the three zones in turn.
-   The primary, secondary, and hidden shards in each shard are not deployed to the three zones in sequence. The deployment of these shards may change when manual switchover or HA failover between primary and secondary shards is triggered.

![](../images/p46749.png "Deployment policy for the components in a multi-zone sharded cluster instance")

## Procedure

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the left-side navigation pane, click **Sharded Cluster Instances**.

3.  On the **Sharded Cluster Instances** page, click **Create Instance**.

4.  Click **Sharded Cluster \(Subscription\)** or **Sharded Cluster \(Pay-as-you-go\)**.

    **Note:**

    -   Subscription: You must pay for an instance when you create it. This method is more cost-effective than the pay-as-you-go method. We recommend that you select this method for long-term use. A longer subscription period enables a larger discount.
    -   Pay-as-you-go: You are billed on an hourly basis based on the used resources. We recommend that you select this billing method for short-term use. You can reduce costs by releasing your pay-as-you-go instance after you no longer need it.
5.  Set **Region** to **China \(Hangzhou\)**, **China \(Beijing\)**,**China \(Shenzhen\)**, or **Singapore \(Singapore\)** and select a multi-zone.

    ![Select a multi-zone](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0745298951/p46740.png)

6.  Configure other parameters. For more information, see [Create a sharded cluster instance](/intl.en-US/Quick Start/Create an instance/Create a sharded cluster instance.md).

7.  Click **Buy Now** to go to the Confirm Order page.

8.  Read and select Agreement of Service and complete the payment.


## References

You can use the Service Availability function to view the distribution of nodes in a replica set instance across zones. You can also switch the node roles of the instance based on your business deployment. This way, your applications can connect to the nodes closest to them. For more information, see [Switch node roles](/intl.en-US/User Guide/Instance management/Switch node roles.md).

