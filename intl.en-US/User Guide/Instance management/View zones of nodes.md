# View zones of nodes

ApsaraDB for MongoDB provides the zone distribution of nodes. You can view the zone distribution information in the console.

## Prerequisites

Replica set or sharded cluster instances are created.

## Deployment tips

ApsaraDB for MongoDB provides a zone-disaster recovery solution for replica set instances to meet the high reliability and data security requirements in business scenarios. This solution deploys the nodes of a replica set instance or the components of a sharded cluster instance in three different [zones](https://www.alibabacloud.com/help/zh/doc-detail/26559.htm). When one of the three zones loses communication due to force majeure factors such as power failure or network failure, the high-availability system automatically triggers a switchover. This ensures the continuous availability and data security of the entire instance. For more information, see [Create a multi-zone replica set instance](/intl.en-US/User Guide/Zone-disaster restoration solution/Create a multi-zone replica set instance.md) and [Create a multi-zone sharded cluster instance](/intl.en-US/User Guide/Zone-disaster restoration solution/Create a multi-zone sharded cluster instance.md).

**Note:** For more information about comparison of node deployment policies for single and multiple zones, see [Node deployment policies](/intl.en-US/User Guide/Zone-disaster restoration solution/Create a multi-zone replica set instance.md) and [Create a multi-zone sharded cluster instance](/intl.en-US/User Guide/Zone-disaster restoration solution/Create a multi-zone sharded cluster instance.mdsection_wjr_qpj_wgb).

## View zones of nodes

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Replica Set Instances**, or **Sharded Cluster Instances** based on the instance type.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Service Availability** to view the current zone distribution.

    -   Replica set instances

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9735298951/p50550.png)

    -   Sharded cluster instances

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9735298951/p50551.png)


## References

-   [Migrate an ApsaraDB for MongoDB instance across zones in the same region](/intl.en-US/User Guide/Instance management/Migrate an ApsaraDB for MongoDB instance across zones in the same region.md)

    Migrate instances to other zones within the same region. For example, you can migrate instances from a single zone to multiple zones. After instances are migrated to other zones, the attributes, specifications, and connection strings of the instances remain unchanged.

-   [Switch node roles](/intl.en-US/User Guide/Instance management/Switch node roles.md)

    You can switch the node roles of an ApsaraDB for MongoDB instance based on your business deployment. This allows your applications to connect to the nearest nodes.


