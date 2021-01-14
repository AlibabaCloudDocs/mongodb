# How to troubleshoot database connection failures after the number of connections reaches the upper limit

After the number of connections to an ApsaraDB for MongoDB instance reaches the limit, new connection requests cannot be responded. This topic describes how to handle database connection failures after the number of connections reaches the upper limit.

## Symptom

The maximum number of connections varies depending on ApsaraDB for MongoDB instance types. For more information, see [Instance types](/intl.en-US/Product Introduction/Instance types.md).

-   The application fails to connect to the database.
-   The whitelist has been properly set. However, the following error message is displayed when you use the mongo shell to connect to the database:

    ```
    2019-07-10T10:30:43.597+0800 E QUERY    [js] Error: network error while attempting to run command 'isMaster' on host 'dds-bpxxxxxxxx.mongodb.rds.aliyuncs.com:3717'  :
    connect@src/mongo/shell/mongo.js:328:13
    @(connect):1:6
    exception: connect failed
    ```

-   The whitelist has been properly set. However, the following error message is displayed when you use DMS to connect to the database.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0157297751/p51168.png)


## Check whether the number of connections has reached the upper limit

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).

2.  In the upper-left corner of the page, select the resource group and the region of the target instance.

3.  In the left-side navigation pane, click **Sharded Cluster Instances**.

4.  Find the target instance and click its ID.

5.  In the left-side navigation pane, click **Monitoring Info**.

6.  On the **Monitoring Info** page, check the **Connections** information. The following figure shows that the number of connections to the instance is 500.

    **Note:** If the instance is a sharded cluster instance, you must select the **Mongos** node in use in the upper-right corner on the page.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0157297751/p51156.png)

7.  In the left-side navigation pane, click **Basic Information**.

8.  On the **Basic Information** page, query the maximum number of connections corresponding to the current instance specifications. In this example, the number is 500.

    **Note:** Based on the number of current connections, you can confirm that the number of connections has reached the upper limit.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0157297751/p51158.png)


## Solution

You can restart the instance to temporarily release all connections. For more information, see [Restart an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance management/Restart an ApsaraDB for MongoDB instance.md). To prevent this problem from occurring again, we recommend that you perform the following operations after restarting the instance:

**Note:** If you restart the instance, all instance nodes are restarted one by one. Each node has a transient disconnection of about 30 seconds. If there are a large number of collections \(more than 10,000\), the transient disconnections last longer. Before restarting the instance, arrange your business and ensure that your application has a reconnection mechanism.

-   Configure the connection pool. For more information, see [How to query and limit the number of connections](/intl.en-US/Product Usage/Hot issues/How to query and limit the number of connections to an apsaradb for MongoDB instance.md).
-   Analyze the connection sources. For more information, see [Query the source IP addresses of current connections](/intl.en-US/Product Usage/Hot issues/How to query and limit the number of connections to an apsaradb for MongoDB instance.md). If the service uses all the connections, upgrade the instance specifications. For more information, see [t6706.md\#](/intl.en-US/User Guide/Instance management/Changing Instance Configuration/Configuration change overview.md).

