# Manage the ApsaraDB for MongoDB balancer {#concept_w2f_kbl_2gb .concept}

ApsaraDB for MongoDB allows you to manage the balancer. In some special business scenarios, you can enable or disable the balancer, set an active window, and perform other operations related to the balancer.

## Precautions {#section_qjg_dwl_2gb .section}

-   The balancer is a feature of the sharded cluster architecture and applies only to sharded cluster instances.
-   Because operations related to the balancer may occupy the resources of an instance, we recommend that you manage the balancer during off-peak hours.

## Disable the balancer {#section_k3j_4wl_2gb .section}

ApsaraDB for MongoDB enables the balancer by default. To disable the balancer in special business scenarios, follow these steps:

1.  [Connect to ApsaraDB for MongoDB through the mongo shell](https://www.alibabacloud.com/help/doc-detail/55248.htm).
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
    -   If the command returns waiting, the balancer is migrating chunks. In this case, you cannot disable the balancer, otherwise data may become inconsistent.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81256/155624447034744_en-US.png)

4.  After confirming that the balancer is not running any tasks, run the following command to disable the balancer:

    ```
    sh.stopBalancer()
    ```


## Enable the balancer {#section_dyr_pcm_2gb .section}

If you have configured sharding, the balancer can immediately start a balancing procedure among shards after being enabled. Because balancing occupies the resources of an instance, we recommend that you perform this operation during off-peak hours.

1.  [Connect to ApsaraDB for MongoDB through the mongo shell](https://www.alibabacloud.com/help/doc-detail/55248.htm).
2.  After connecting to a mongos node, run the following command in the mongo shell to switch to the config database:

    ```
    use config
    ```

3.  Run the following command to enable the balancer:

    ```
    sh.setBalancerState(true)
    ```


## Set an active time window for the balancer {#section_xss_lbl_2gb .section}

To avoid negative impact on your business while the balancer is migrating chunks, you can set an active time window to allow the balancer to migrate chunks only within the specified period of time.

**Note:** Before performing this operation, you must ensure that the balancer is enabled. For more information about how to enable the balancer, see [Enable the balancer](#section_dyr_pcm_2gb).

1.  [Connect to ApsaraDB for MongoDB through the mongo shell](https://www.alibabacloud.com/help/doc-detail/55248.htm).
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

    -   <start-time\>: The start time in HH:MM format, where the value range of HH is 00–23 and that of MM is 00–59.
    -   <stop-time\>: The end time in HH:MM format, where the value range of HH is 00–23 and that of MM is 00–59.
    You can run the `sh.status()` command to check the active time window of the balancer. For example, the following command output shows that the active time window of the balancer is 01:00–03:00.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81256/155624447034738_en-US.png)


You can also perform other related operations. For example, to ensure that the balancer is always running, you can run the following command to clear the active time window settings:

```
db.settings.update({ _id : "balancer" }, { $unset : { activeWindow : true } })
				
```

