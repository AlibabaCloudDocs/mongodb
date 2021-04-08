# MongoDB实例的CPU使用率高问题

MongoDB实例的CPU使⽤率是⼀个⾮常重要的监控指标。如果MongoDB实例的CPU使⽤率过⾼，会导致MonogoDB响应缓慢，甚⾄业务不可⽤。本文介绍查看MongoDB实例CPU使用率的方法，以及导致CPU使用率高的原因和优化策略。

## 查看CPU使用率

分⽚集群架构下，各个Shard的CPU使⽤与副本集保持⼀致；Config Server仅仅存储配置元数据，基本上不会造成CPU瓶颈，⼀般可以忽略；Mongos路由节点的CPU使⽤往往与聚合结果集、并发请求数有关。

副本集架构下，提供有多种查看CPU使⽤的⽅法：

-   监控图查看

    MongoDB副本集由多种⻆⾊组成，⼀个⻆⾊可能对应⼀个或多个物理节点。阿⾥云MongoDB对⽤户暴露主节点（Primary）和从节点（Secondary），另外还提供有只读实例。

    在[MongoDB管理控制台](https://mongodb.console.aliyun.com/)的**监控信息**页面，选择对应的⻆色，查看MongoDB CPU使⽤率的监控情况。

    **说明：** CPU使⽤率与实例规格有关，例如实例规格是8GB/16GB，那么CPU使⽤率显示100%的时候，就表示该实例已经⽤满了8core的CPU，⽽并⾮显示800%。

    ![使用监控图查看CPU使用率](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7137666161/p235638.png)

    在[MongoDB管理控制台](https://mongodb.console.aliyun.com/)的**CloudDBA** \> **性能趋势**页面查看实例的CPU使⽤情况。

    ![使用CloudDBA中的“性能趋势”查看MongoDB实例的CPU使用率](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7137666161/p235642.png)

-   命令⾏查看

    当前的阿⾥云数据库MongoDB暂不⽀持分别查看用户态和内核态的CPU使⽤率，在某些场景下我们可能需要使⽤历史经验对MongoDB实例的CPU占用高问题进行初步判断：

    -   用户态CPU占⽤⾼：一般是数据库的请求语句的问题。
    -   内核态CPU占⽤⾼：一般是 MongoDB软件本身的问题。
    通过命令`db.serverStatus().systemInfo`查看当前MongoDB实例user态和sys态的CPU使⽤情况。返回示例如下所示：

    ```
    {
        "user time us":NumberLong(1873234),
        "system time us":NumberLong(0),
        "user cpu usage per 10 thousand":NumberLong(18713),
        "system cpu usage per 10 thousand":NumberLong(0),
        "block direct write operations"：NumberLong("114766377048"),
    ......
    }
    ```

-   查看和Kill活跃会话

    正常运⾏中的MongoDB实例会话突然飙升⾄100%，绝⼤部分情况是业务侧的变化引起，可能是由于扫描行数过多、数据排序和聚合、业务流量突增等原因导致的。建议您使⽤以下方法查看。

    -   在[MongoDB管理控制台](https://mongodb.console.aliyun.com/)的**CloudDBA** \> **实例会话**页面查看当前执行的活跃会话，分析不符合预期执行时间的查询操作，选择Kill活跃会话或者其他方法解决该问题。

        ![查看当前活跃的业务会话](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7137666161/p235645.png)

    -   通过MongoDB⾃带的命令db.currentOp\(\)查看和分析更加详细的活跃会话执行情况。如果需要，可以通过命令db.killOp\(\)主动Kill⾮预期内的慢查询。详情请参见[db.currentOp\(\)](https://docs.mongodb.com/manual/reference/method/db.currentOp/)和[db.killOp\(\)](https://docs.mongodb.com/manual/reference/method/db.killOp/)。
-   记录慢⽇志和审计⽇志

    MongoDB在profiling上共有3种设置模式：

    -   关闭 profiling，即不记录任何请求。
    -   针对所有请求开启 profiling，即将所有请求的执⾏都记录到system.profile集合。
    -   慢查询 profiling，将超过⼀定阈值的请求，记录到system.profile集合。
    在[MongoDB管理控制台](https://mongodb.console.aliyun.com/)的**参数设置** \> **参数列表**页面，根据业务需求设置合理的operationProfiling.mode（慢查询的模式）和operationProfiling.slowOpThresholdMs（慢查询的阈值）。

    ![设置慢查询模式和阈值](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7137666161/p235653.png)

    设置profiling后，您可以在**日志管理** \> **慢日志**中查看慢⽇志。

    ![查看慢日志](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7137666161/p235654.png)

    更多profiling的信息请参见：[https://docs.mongodb.com/manual/tutorial/manage-the-database-profiler/](https://docs.mongodb.com/manual/tutorial/manage-the-database-profiler/)

    部分情况下排查问题请求需要更为细致的审计，您可以在[MongoDB管理控制台](https://mongodb.console.aliyun.com/)的**数据安全性** \> **审计日志**页面开通审计⽇志。

    ![开通审计日志方法](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7137666161/p235655.png)

    关于审计⽇志的使⽤⽅法和语法参考：[t1936227.dita\#task\_1936227](/intl.zh-CN/数据采集/云产品日志采集/MongoDB日志/开通日志审计功能.md)


## CPU使用率高的常见原因和优化策略

CPU使用率高的常见原因及对应的优化策略如下：

-   扫描⾏数过多

    MongoDB为多线程应⽤，如果存在单个查询扫描⾏数过多，该查询所在线程的CPU占⽤时间会变⻓，当请求堆积或此类查询的并发度⾜够高时，整个MongoDB实例的CPU占用就会过高。从某种意义上说，MongoDB的CPU使⽤率与该实例的总扫描⾏数成正相关的关系。

    索引优化是减少MongoDB单个查询扫描⾏数的最优⽅案，从底层设计上，MongoDB的索引设计原理⼏乎与MySQL保持⼀致（或许种类和功能更丰富⼀些），所以适⽤于MySQL的索引优化策略基本也都适⽤于 MongoDB实例。

    导致查询扫描行数过多的场景有以下几个方面：

    -   全表扫描

        当您在system.profile集合或者运⾏⽇志⽂件发现COLLSCAN关键字时，就表示该查询进行了全表扫描。针对这类查询，您可以通过添加索引的方法优化，如果当前已不能使用该方法，则在业务侧控制该表的数据量和执行频率。

        更多关于查询执⾏计划的解读，请参见：[https://docs.mongodb.com/manual/reference/explain-results/](https://docs.mongodb.com/manual/reference/explain-results/)和[https://docs.mongodb.com/manual/reference/operator/meta/explain/](https://docs.mongodb.com/manual/reference/operator/meta/explain/)。

    -   索引设计和优化

        除了全表扫描以外，当查询的扫描行数关键字docsExamined超过1000且执行频率较高时，我们需要关注该查询。除了全表扫描以外，造成docsExamined过多⼀般有以下情况：

        -   多条件过滤时，未使⽤组合索引或不满⾜最左前缀匹配原则。
        -   未使⽤索引做排序操作。
        -   查询过于复杂，或者存在⼤量的聚合类操作，基本⽆法从索引层⾯做到极致优化，或者导致查询⾛错解析计划。
        -   数据列的数据选择性和运⾏频率的评估错误，未能做到最好的折中。
        针对以上问题的更多信息，请参见以下官⽅⽂档：

        -   组合索引的原理和使⽤⽅法，详情请参见：[https://docs.mongodb.com/manual/core/index-compound/](https://docs.mongodb.com/manual/core/index-compound/)。
        -   使⽤索引排序，详情请参见：[https://docs.mongodb.com/manual/tutorial/sort-results-with-indexes/](https://docs.mongodb.com/manual/tutorial/sort-results-with-indexes/)。
        -   使⽤Hint固化执⾏计划，详情请参考：[https://docs.mongodb.com/manual/reference/operator/meta/hint/](https://docs.mongodb.com/manual/reference/operator/meta/hint/)和[https://docs.mongodb.com/manual/reference/method/cursor.hint/](https://docs.mongodb.com/manual/reference/method/cursor.hint/)。
        -   索引的数据选择性和运⾏频率折中⽅法，详情请参见：[https://docs.mongodb.com/manual/tutorial/create-queries-that-ensure-selectivity/](https://docs.mongodb.com/manual/tutorial/create-queries-that-ensure-selectivity/)。
-   并发过大

    如果确认查询层⾯没有问题，那么引起实例CPU占用高的可能原因为业务并发过⾼。如果是由于业务请求量过⼤，并发过⾼导致了CPU占用高的问题，在云数据库MongoDB中解决思路本质上就是通过添加CPU核数的⽅式解决，⼀般有如下⽅法：

    -   单实例垂直配置升降级，使得单实例能够承载更多的读写量。
    -   配置副本集层⾯的读写分离，或者添加该副本的只读实例。
    -   升级⾄MongoDB分⽚集群，通过数据⽔平拆分的⽅式横向，线性扩展系统性能。
    -   如果是Mongos路由节点CPU占满，则直接添加Mongos节点个数并设置Mongos节点的负载均衡。
    更多内容请参见阿⾥云MongoDB官⽅⽂档：[t1253515.dita\#task\_1580394](/intl.zh-CN/用户指南/实例管理/变更实例配置/变更分片集群实例配置.md)、[t1254246.dita\#task\_1580779](/intl.zh-CN/用户指南/实例管理/变更实例配置/变更单节点或副本集实例配置.md)和[t41229.dita\#task\_pwm\_cfm\_qfb](/intl.zh-CN/用户指南/实例管理/变更实例配置/变更副本集实例节点数.md)。


## 其他可能导致CPU使用率高的场景

-   MongoDB频繁短连接

    MongoDB 3.X后使⽤的默认的身份认证机制是SCRAM-SHA1，需要进⾏⼀些CPU密集型操作⽐如哈希计算等，在⾼并发的短连接场景下，这些哈希计算占⽤的CPU将会被放⼤很多倍，进⽽耗尽整个机器的CPU资源，其中⼀个现象是在运⾏⽇志中可以发现⼤量包含saslStart的报错信息。

    阿⾥云MongoDB建议您尽可能使⽤⻓连接，同时在PHP⾼并发短连接场景做了⼀定程度的优化，通过在内核层⾯优化改写内置的随机函数的⽅式⼤幅降低了MongoDB实例CPU使⽤率。

    在[MongoDB管理控制台](https://mongodb.console.aliyun.com/)的**数据库连接**页面开启私网免密访问。

    ![开启私网免密访问](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7137666161/p235803.png)

-   TTL索引导致从节点（Secondary）CPU使⽤率⾼于主节点（Primary）CPU使用率

    自MongoDB 3.2开始实现了多线程复制，Oplog日志的回放并发度由参数replWriterThreadCount控制，默认为16。所以尽管Secondary节点不承载任何业务读，在部分场景下CPU使⽤率也可能会超过Primary节点。例如在Primary节点上针对某⼀张表设置了TTL过期⾃动删除，在Primary节点上，系统会根据时间列的索引批量删除数据，效率很⾼，同时会将该操作转换成很多单条的Delete操作发送给Secondary节点；在Secondary节点上，回放Oplog日志时效率较低，所以在多线程回放的情况下容易引起该节点CPU升⾼。如果遇到这种情况，建议您直接忽略。


