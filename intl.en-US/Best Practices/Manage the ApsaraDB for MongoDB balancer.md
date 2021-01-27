# Manage the ApsaraDB for MongoDB balancer

ApsaraDB for MongoDB allows you to manage the balancer. You can enable or disable the balancer and set an active time window for the balancer to meet specific business needs.

## Precautions

-   The balancer is a feature of the sharded cluster architecture and applies only to sharded cluster instances.
-   Operations related to the balancer may occupy the resources of an instance. Therefore, we recommend that you perform these operations during off-peak hours.

## Set an active time window for the balancer

The balancer consumes resources of nodes in an instance to migrate chunks, which may cause imbalanced resource usage on the nodes and affect business operations. To avoid negative impact on your business while the balancer is migrating chunks, you can set an active time window to allow the balancer to migrate chunks only within the specified period of time.

**Note:** Before performing this operation, make sure that the balancer is enabled. For more information about how to enable the balancer, see [Enable the balancer](#section_ikm_sbc_lh7).

1.  [Connect to a sharded cluster instance by using the mongo shell](/intl.en-US/Quick Start/Connect to an instance/Connect to a sharded cluster instance by using the mongo shell.md).
2.  After connecting to a mongos node, run the following command in the mongo shell to switch to the config database:

    ```
    use config
    ```

3.  Run the following command to set an active time window for the balancer:

    ```
    db.settings.update(
       { _id: "balancer" },
       { $set: { activeWindow : { start : "<start-time>", stop : "<stop-time>" } } },
       { upsert: true }
    )
    ```

    **Note:**

    -   <start-time\>: the start time in HH:MM format in UTC time, where the value range of HH is 00 to 23 and that of MM is 00 to 59.
    -   <stop-time\>: the end time in HH:MM format in UTC time, where the value range of HH is 00 to 23 and that of MM is 00 to 59.
    You can run the `sh.status()` command to check the active time window of the balancer. For example, the following command output shows that the active time window of the balancer is 01:00 to 03:00.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4130276951/p34738.png)


You can also perform other related operations. For example, to ensure that the balancer is always running, you can run the following command to clear the active time window settings:

```
db.settings.update({ _id : "balancer" }, { $unset : { activeWindow : true } })                
```

## Enable the balancer

If you have configured sharding, the balancer can immediately start a balancing procedure among shards after being enabled. Balancing occupies the resources of an instance. Therefore, we recommend that you perform this operation during off-peak hours.

1.  [Connect to a sharded cluster instance by using the mongo shell](/intl.en-US/Quick Start/Connect to an instance/Connect to a sharded cluster instance by using the mongo shell.md).
2.  After connecting to a mongos node, run the following command in the mongo shell to switch to the config database:

    ```
    use config
    ```

3.  Run the following command to enable the balancer:

    ```
    sh.setBalancerState(true)
    ```


## Disable the balancer

ApsaraDB for MongoDB enables the balancer by default. To disable the balancer in special business scenarios, follow these steps:

1.  [Connect to a sharded cluster instance by using the mongo shell](/intl.en-US/Quick Start/Connect to an instance/Connect to a sharded cluster instance by using the mongo shell.md).
2.  After connecting to a mongos node, run the following command in the mongo shell to switch to the config database:

    ```
    use config
    ```

3.  Run the following command to check the running status of the balancer:

    ```
    while( sh.isBalancerRunning() ) {
              print("waiting...");
              sleep(1000);
    }
    ```

    -   If the command does not return any values, the balancer is not running any tasks. You can proceed to disable the balancer.
    -   If the command returns `waiting`, the balancer is migrating chunks. In this case, you cannot disable the balancer. Otherwise, data may become inconsistent.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4130276951/p34744.png)

4.  After confirming that the balancer is not running any tasks, run the following command to disable the balancer:

    ```
    sh.stopBalancer()
    ```


