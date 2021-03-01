# 管理MongoDB均衡器Balancer

云数据库支持均衡器Balancer管理操作。在一些特殊的业务场景下，您可以启用或关闭Balancer功能并设置活动窗口。

## 注意事项

-   Balancer属于分片集群架构中的功能，该操作仅适用于分片集群实例。
-   Balancer的相关操作可能会占用实例的资源，请在业务低峰期操作。

## 设置Balancer的活动窗口

均衡器在执行块迁移操作时将占用实例中节点的资源，可能造成节点的资源使用率不均衡，影响业务使用。为避免块迁移给您的业务带来影响，您可以通过设置均衡器的活动窗口，让其在指定的时间段工作。

**说明：** 执行该操作须确保Balancer功能处于开启状态。如未开启，请参见[开启Balancer功能](#section_ikm_sbc_lh7)。

1.  [通过Mongo Shell连接MongoDB分片集群实例](/intl.zh-CN/快速入门/连接实例/通过Mongo Shell连接MongoDB分片集群实例.md)。
2.  在mongos节点命令窗口中，切换至config数据库。

    ```
    use config
    ```

3.  执行如下命令设置Balancer的活动窗口。

    ```
    db.settings.update(
       { _id: "balancer" },
       { $set: { activeWindow : { start : "<start-time>", stop : "<stop-time>" } } },
       { upsert: true }
    )
    ```

    **说明：**

    -   <start-time\>：开始时间，时间格式为HH:MM（实例所在地域的当地时间），HH取值范围为00 - 23，MM取值范围为00 - 59。
    -   <stop-time\>：结束时间，时间格式为HH:MM（实例所在地域的当地时间），HH取值范围为00 - 23，MM取值范围为00 - 59。
    您可以通过执行`sh.status()`命令查看Balancer的活动窗口。如下示例中，活动窗口被设置为01:00- 03:00。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6130276951/p34738.png)


相关操作：如您需要Balancer始终处于运行状态，您可以使用如下命令去除活动窗口的设置。

```
db.settings.update({ _id : "balancer" }, { $unset : { activeWindow : true } })                
```

## 开启Balancer功能

如果您设置了数据分片，开启Balancer功能后可能会立即触发均衡任务。这将占用实例的资源，请在业务低峰期执行该操作。

1.  [通过Mongo Shell连接MongoDB分片集群实例](/intl.zh-CN/快速入门/连接实例/通过Mongo Shell连接MongoDB分片集群实例.md)。
2.  在mongos节点命令窗口中，切换至config数据库。

    ```
    use config
    ```

3.  执行如下命令开启Balancer功能。

    ```
    sh.setBalancerState(true)
    ```


## 关闭Balancer功能

云数据库MongoDB的Balancer功能默认是开启状态。如果在某些特殊业务场景下需要临时关闭，请参见下述步骤进行操作。

1.  [通过Mongo Shell连接MongoDB分片集群实例](/intl.zh-CN/快速入门/连接实例/通过Mongo Shell连接MongoDB分片集群实例.md)。
2.  在mongos节点命令窗口中，切换至 config 数据库。

    ```
    use config
    ```

3.  执行如下命令查看Balancer运行状态，如返回值为空。

    ```
    while( sh.isBalancerRunning() ) {
              print("waiting...");
              sleep(1000);
    }
    ```

    -   返回值为空，表示Balancer没有处于执行任务的状态，此时可执行下一步的操作，关闭Balancer 。
    -   返回值为`waiting`，表示Balancer正在执行块迁移，此时不能执行关闭Balancer的命令，否则可能引起数据不一致。

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6130276951/p34744.png)

4.  确认执行第3步的命令后返回的值为空，可执行关闭Balancer命令。

    ```
    sh.stopBalancer()
    ```


