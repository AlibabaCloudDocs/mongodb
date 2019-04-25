# Restart an instance {#concept_yzz_dgl_j2b .concept}

If the connections to an instance exceed the upper limit or the instance encounters any performance problems, you can manually restart the instance.

For a standalone instance or three-node replica set instance, you can log on to the ApsaraDB for MongoDB console to restart the instance.

For a sharded cluster instance, you can restart the instance or restart a node of the instance. When a node is being restarted, this node cannot be accessed. During the restart of a node, you can also restart another node.

**Note:** An instance may be disconnected during a restart. You need to restart it with caution and make arrangements for business interruption.

## Restart a standalone or replica set instance {#section_xjq_ggn_cfb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  Choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6708/155617001645431_en-US.png)** \> **Restart** in the Operation column corresponding to the target instance.

    You can also click the target instance ID or choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6708/155617001645431_en-US.png)** \> **Manage** in the Operation column corresponding to the target instance. On the Basic Information page that appears, click **Restart Instance**.

4.  In the Restart Instance dialog box that appears, click **OK**.

    The instance immediately enters the **Rebooting** status. The instance is successfully restarted when its status changes to **Running**.


## Restart a sharded cluster instance {#section_q52_thn_cfb .section}

**Restart a sharded cluster instance**: The procedure for restarting a sharded cluster instance is the same as that for restarting a standalone or replica set instance. For more information, see [Restart a standalone or replica set instance](#section_xjq_ggn_cfb).

**Restart a node of a sharded cluster instance**

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  Click the target instance ID or choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6708/155617001645431_en-US.png)** \> **Manage** in the Operation column corresponding to the target instance.
4.  To restart a mongos node, do as follows: In the Mongos List area of the Basic Information page, choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6708/155617001645431_en-US.png)** \> **Restart** in the Operation column corresponding to the target mongos node.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6709/155617001611719_en-US.png)

    **Note:** When a node is being restarted, this node cannot be accessed.

5.  To restart a shard, do as follows: In the Shard List area of the Basic Information page, choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6709/155617001611718_en-US.png)** \> **Restart** in the Operation column corresponding to the target shard.
6.  In the Restart Node dialog box that appears, click **OK**.

    The instance immediately enters the **Rebooting** status. The node is successfully restarted when the instance status changes to **Running**.


