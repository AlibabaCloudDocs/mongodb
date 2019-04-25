# Modify the connection information {#task_qnc_nk3_bfb .task}

You can log on to the ApsaraDB for MongoDB console to modify the intranet or Internet connection information for an instance.

For a standalone instance, you can modify the intranet or public address for the primary node only.

For a replica set instance, you can modify the intranet or public address for the primary and secondary nodes.

For a sharded cluster instance, you can modify the intranet or public address for all mongos nodes.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/list).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  In the left-side navigation pane, click **Replica Set Instances** or **Sharding Instances** based on the architecture of the target instance.
4.  Locate the target instance and click its instance ID.
5.  In the left-side navigation pane, click **Database Connection**.
6.  In the Intranet Connection or Public IP Connection area, click **Update Connection String**, as shown in the following figure. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21079/155617174611503_en-US.png)

7.  In the Update Connection String dialog box that appears, modify the connection information for the instance. You can modify the intranet or public address of the instance. For more information, see[Table 1](#table_epd_gwj_bfb) 

    |Instance|Network type|Parameter setting|Description|
    |:-------|:-----------|:----------------|:----------|
    |Standalone|Intranet or Internet|Modify the intranet or public address of the primary node.| You can modify only the prefix of the address.

 A connection address starts with a lowercase letter and consists of letters and digits. It contains 8–64 characters.

 |
    |Replica set|Select the primary node or a secondary node and modify its intranet or public address.|
    |Sharded cluster|Select a mongos node and modify its intranet or public address.|

8.  After setting the required parameter, click **OK**.

After modifying the intranet or Internet connection information, you need to use the modified address to connect a terminal or application to the instance.

