# Release a public address {#concept_ln2_gyr_gfb .concept}

After using a public address to connect to an ApsaraDB for MongoDB instance through the Internet, you can log on to the ApsaraDB for MongoDB console or call the ReleasePublicNetworkAddress operation to release this public address.

## Notes {#section_g4s_2wz_lgb .section}

-   For a sharded cluster instance, you can release the public address for one or more mongos nodes. You can still use a public address that is not released to connect to the corresponding mongos node.
-   After the public address of an instance or mongos node is released, you cannot use this public address to connect to the instance or mongos node.
-   After the public address of an instance is released, if you no longer use a public IP address to connect to this instance, we recommend that you delete this public IP address from the whitelist to guarantee data security. For more information, see [Configure a whitelist](../../../../intl.en-US/Quick Start for Replica Set/Configure a whitelist.md#).

## Release the public address for a standalone or replica set instance {#section_t3c_r1s_gfb .section}

To release the public address for a replica set instance, you release the public addresses of the primary and secondary nodes.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances**.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, click **Database Connection**.
6.  In the Public IP Connection area, click **Release Public IP Address**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21696/155617420037322_en-US.png)

7.  In the Release Public IP Address dialog box that appears, click **OK**.

## Release the public address for a sharded cluster instance {#section_xvm_whs_gfb .section}

You can release the public address for one or more mongos nodes of a sharded cluster instance. Then, you can still use a public address that is not released to connect to the corresponding mongos node.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Sharding Instances**.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, click **Database Connection**.
6.  In the Public IP Connection area, locate the target mongos node whose public address needs to be released.
7.  In the **Operation** column corresponding to the target mongos node, click **Release**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21696/155617420013376_en-US.png)

    **Note:** You can repeat this step to release the public addresses for other mongos nodes based on business requirements. To release the public address for another mongos node of this instance, you need to wait until the last public address is released.

8.  In the Release Public IP Address dialog box that appears, click **OK**.

