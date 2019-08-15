# 设置数据分片以充分利用Shard性能 {#concept_tbb_vzp_bgb .concept}

您可以对分片集群实例中的集合设置数据分片，以充分利用Shard节点的存储空间和计算性能。

## 背景信息 {#section_yrm_8lw_d08 .section}

如果没有对集合设置数据分片，数据将被集中存放在一个Shard节点中，这将导致其他Shard节点的存储空间和计算性能无法被充分利用。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/78547/156585061233995_zh-CN.png)

## 前提条件 {#section_4o7_elv_6ag .section}

实例类型为分片集群实例。

## 注意事项 {#section_mpp_hxq_bgb .section}

-   片键一经设置，不可修改，不可删除。
-   执行了数据分片操作后，均衡器会对满足条件的数据进行拆分，这将占用实例的资源，请在业务低峰期操作。

    **说明：** 您可以在设置数据分片之前，调整均衡器的活动窗口，指定它在业务低峰期执行均衡操作。详情请参见[设置Balancer的活动窗口](cn.zh-CN/最佳实践/管理MongoDB均衡器Balancer.md#section_t52_8zh_nm2)。

-   片键的选取将影响分片集群实例性能，关于片键选取的案例介绍，请参见[如何选择Shard Key](https://help.aliyun.com/document_detail/64561.html#h2--shard-key-3)。

## 分片策略介绍 {#section_hpb_dbw_wrx .section}

|分片策略|说明|适用场景|
|:---|:-|:---|
|基于范围的分片|MongoDB按照片键的值的范围将数据拆分为不同的块（chunk），每个块包含了一段范围内的数据。 -   优点： mongos可以快速定位请求需要的数据，并将请求转发到相应的Shard节点中。
-   缺点： 可能导致数据在Shard节点上分布不均衡，容易造成读写热点，且不具备写分散性。

 | 片键的值不是单调递增或单调递减、片键的值基数大且重复的频率低、需要范围查询等业务场景。

 |
|基于Hash值的分片|MongoDB计算单个字段的哈希值作为索引值，并以哈希值的范围将数据拆分为不同的块。 -   优点：可以将数据更加均衡地分布在各Shard节点中，具备写分散性。
-   缺点：不适合进行范围查询，进行范围查询时，需要将读请求分发到所有的Shard节点。

 | 片键的值存在单调递增或递减、片键的值基数大且重复的频率低、需要写入的数据随机分发、数据读取随机性较大等业务场景。

 |

除了上述两种分片策略，您还可以配置复合片键，例如由一个低基数的键和一个单调递增的键组成，详情请参见[Shard Key选择案例](https://help.aliyun.com/document_detail/64561.html#h2--shard-key-3)。

## 操作步骤 {#section_g4t_fxq_bgb .section}

本文以mongodbtest数据库，customer集合为例介绍操作流程。

1.  [通过Mongo Shell登录分片集群实例](../../../../cn.zh-CN/分片集群快速入门/连接实例/通过 Mongo Shell 登录MongoDB数据库.md#)。
2.  对集合所在的数据库启用分片功能。

    ``` {#codeblock_2y7_mi7_dqw}
    sh.enableSharding("<database>")
    ```

    **说明：** <database\>：数据库名。

    示例：

    ``` {#codeblock_ts0_1kb_c0f}
    sh.enableSharding("mongodbtest")
    ```

    **说明：** 您可以通过`sh.status()`查看分片状态。

3.  对片键的字段建立索引。

    ``` {#codeblock_oc4_m69_p3w}
    db.<collection>.createIndex(<keyPatterns>,<options>)
    ```

    **说明：** 

    -   <collection\>：集合名。
    -   <keyPatterns\>：包含用于建立索引的字段和索引类型。

        常见的索引类型如下：

        -   1：创建升序索引
        -   -1：创建降序索引
        -   "hashed"：创建哈希索引
    -   <options\>：表示接收可选参数，详情请参见[db.collection.createIndex\(\)](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/)，本操作示例中暂未使用到该字段。
    创建升序索引示例：

    ``` {#codeblock_z5n_n09_qwm}
    db.customer.createIndex({name:1})
    ```

    创建哈希索引示例：

    ``` {#codeblock_y4t_lzi_nni}
    db.customer.createIndex({id:"hashed"})
    ```

4.  对集合设置数据分片。

    ``` {#codeblock_xhb_pb5_k7h}
    sh.shardCollection("<database>.<collection>",{ "<key>":<value> } ) 
    ```

    **说明：** 

    -   <database\>：数据库名。
    -   <collection\>：集合名。
    -   <key\>：分片的键，MongoDB将根据片键的值进行数据分片。
    -   <value\>
        -   1：表示基于范围分片，通常能很好地支持基于片键的范围查询。
        -   “hashed”：表示基于哈希分片，通常能将写入均衡分布到各Shard节点中。
    基于范围分片的配置示例：

    ``` {#codeblock_s9u_zx7_r1p}
    sh.shardCollection("mongodbtest.customer",{"name":1})
    ```

    基于哈希分片的配置示例：

    ``` {#codeblock_ry1_8mq_rat}
    sh.shardCollection("mongodbtest.customer",{"id":"hashed"})
    ```


## 后续操作 {#section_w5t_4jr_bgb .section}

经过一段时间的运行或数据写入后，您可以在Mongo Shell中执行`sh.status()`，查看数据在各Shard节点中的分布信息。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/78547/156585061234049_zh-CN.png)

您也可以通过执行`db.stats()`查看该数据库在各Shard节点的数据存储情况。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/78547/156585061233949_zh-CN.png)

