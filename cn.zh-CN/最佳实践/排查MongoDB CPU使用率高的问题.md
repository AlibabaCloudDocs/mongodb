# 排查MongoDB CPU使用率高的问题 {#concept_62224_zh .concept}

在使用云数据库MongoDB的时候您可能会遇到MongoDB CPU使用率很高或者CPU使用率接近100%的问题，从而导致数据读写处理异常缓慢，影响正常业务。本文主要帮助您从应用的角度排查MongoDB CPU使用率高的问题。

## 分析MongoDB数据库正在执行的请求 {#section_gdv_ltv_1gb .section}

1.  通过Mongo Shell连接实例。
    -   [Mongo Shell连接单节点实例](../../../../cn.zh-CN/单节点快速入门/连接实例/通过Mongo Shell登录MongoDB数据库.md#)
    -   [Mongo Shell连接副本集实例](../../../../cn.zh-CN/副本集快速入门/连接实例/通过Mongo Shell登录MongoDB数据库.md#)
    -   [Mongo Shell连接分片集群实例](../../../../cn.zh-CN/分片集群快速入门/连接实例/通过 Mongo Shell 登录MongoDB数据库.md#)
2.  执行`db.currentOp()`命令，查看数据库当前正在执行的操作。

    该命令的输出示例如下。

    ``` {#codeblock_xkm_g99_vn3}
    {
            "desc" : "conn632530",
            "threadId" : "140298196924160",
            "connectionId" : 632530,
            "client" : "11.192.159.236:57052",
            "active" : true,
            "opid" : 1008837885,
            "secs_running" : 0,
            "microsecs_running" : NumberLong(70),
            "op" : "update",
            "ns" : "mygame.players",
            "query" : {
                "uid" : NumberLong(31577677)
            },
            "numYields" : 0,
            "locks" : {
                "Global" : "w",
                "Database" : "w",
                "Collection" : "w"
            },
            ....
        },
    ```


您需要重点关注以下几个字段。

|字段|返回值说明|
|:-|:----|
|client|该请求是由哪个客户端发起的。|
|opid|操作的唯一标识符。 **说明：** 如果有需要，可以通过`db.killOp(opid)`直接终止该操作。

 |
|secs\_running|表示该操作已经执行的时间，单位为秒。如果该字段返回的值特别大，需要查看请求是否合理。|
|microsecs\_running|表示该操作已经执行的时间，单位为微秒。如果该字段返回的值特别大，需要查看请求是否合理。|
|ns|该操作目标集合。|
|op|表示操作的类型。通常是查询、插入、更新、删除中的一种。|
|locks|跟锁相关的参数，请参考官方文档，本文不做详细介绍。 **说明：** db.currentOp 文档请参见[db.currentOp](https://docs.mongodb.com/manual/reference/method/db.currentOp/?spm=5176.100239.blogcont73389.12.K1pNOi)。

 |

通过`db.currentOp()`查看正在执行的操作，分析是否有不正常耗时的请求正在执行。比如您的业务平时 CPU 使用率不高，运维管理人员连到MongoDB数据库执行了一些需要全表扫描的操作导致 CPU 使用率非常高，业务响应缓慢，此时需要重点关注执行时间非常耗时的操作。

**说明：** 如果发现有异常的请求，您可以找到该请求对应的opid，执行`db.killOp(opid)`终止该请求。

如果您的应用刚刚上线，MongoDB实例的CPU使用率马上处于持续很高的状态，执行`db.currentOp()`，在输出结果中未发现异常请求，您可参考下述小节分析数据库慢请求。

## 分析MongoDB数据库的慢请求 {#section_n2c_ltv_1gb .section}

云数据库MongoDB默认开启了慢请求Profiling ，系统自动地将请求时间超过100ms的执行情况记录到对应数据库下的system.profile集合里。

1.  通过 Mongo Shell 连接实例。

    详情请参考[Mongo Shell连接单节点实例](../../../../cn.zh-CN/单节点快速入门/连接实例/通过Mongo Shell登录MongoDB数据库.md#)、[Mongo Shell连接副本集实例](../../../../cn.zh-CN/副本集快速入门/连接实例/通过Mongo Shell登录MongoDB数据库.md#)、[Mongo Shell连接分片集群实例](../../../../cn.zh-CN/分片集群快速入门/连接实例/通过 Mongo Shell 登录MongoDB数据库.md#)。

2.  通过`use <database>`命令进入指定数据库。

    ``` {#codeblock_3sj_5rv_ubj}
    use mongodbtest
    ```

3.  执行如下命令，查看该数据下的慢请求日志。

    ``` {#codeblock_1xy_iti_9b2}
    db.system.profile.find().pretty()
    ```

4.  分析慢请求日志，查找引起MongoDB CPU使用率升高的原因。

    以下为某个慢请求日志示例，可查看到该请求进行了全表扫描，扫描了11000000个文档，没有通过索引进行查询。

    ``` {#codeblock_yp1_61t_ia6}
    {
            "op" : "query",
            "ns" : "123.testCollection",
            "command" : {
                    "find" : "testCollection",
                    "filter" : {
                            "name" : "zhangsan"
                    },
                    "$db" : "123"
            },
            "keysExamined" : 0,
            "docsExamined" : 11000000,
            "cursorExhausted" : true,
            "numYield" : 85977,
            "nreturned" : 0,
            "locks" : {
                    "Global" : {
                            "acquireCount" : {
                                    "r" : NumberLong(85978)
                            }
                    },
                    "Database" : {
                            "acquireCount" : {
                                    "r" : NumberLong(85978)
                            }
                    },
                    "Collection" : {
                            "acquireCount" : {
                                    "r" : NumberLong(85978)
                            }
                    }
            },
            "responseLength" : 232,
            "protocol" : "op_command",
            "millis" : 19428,
            "planSummary" : "COLLSCAN",
            "execStats" : {
                    "stage" : "COLLSCAN",
                    "filter" : {
                            "name" : {
                                    "$eq" : "zhangsan"
                            }
                    },
                    "nReturned" : 0,
                    "executionTimeMillisEstimate" : 18233,
                    "works" : 11000002,
                    "advanced" : 0,
                    "needTime" : 11000001,
                    "needYield" : 0,
                    "saveState" : 85977,
                    "restoreState" : 85977,
                    "isEOF" : 1,
                    "invalidates" : 0,
                    "direction" : "forward",
    ....in"
                    }
            ],
            "user" : "root@admin"
    }
    ```


通常在慢请求日志中，您需要重点关注以下几点。

-   全表扫描（关键字： COLLSCAN、 docsExamined ）
    -   全集合（表）扫描COLLSCAN 。

        当一个操作请求（如查询、更新、删除等）需要全表扫描时，将非常占用CPU资源。在查看慢请求日志时发现COLLSCAN关键字，很可能是这些查询占用了你的CPU资源。

        **说明：** 如果这种请求比较频繁，建议对查询的字段建立索引的方式来优化。

    -   通过查看docsExamined的值，可以查看到一个查询扫描了多少文档。该值越大，请求所占用的CPU开销越大。
-   不合理的索引（关键字： IXSCAN、keysExamined ）

    **说明：** 

    -   索引不是越多越好，索引过多会影响写入、更新的性能。
    -   如果您的应用偏向于写操作，索引可能会影响性能。
    通过查看keysExamined字段，可以查看到一个使用了索引的查询，扫描了多少条索引。该值越大，CPU开销越大。

    如果索引建立的不太合理，或者是匹配的结果很多。这样即使使用索引，请求开销也不会优化很多，执行的速度也会很慢。

    如下所示，假设某个集合的数据，x字段的取值很少（假设只有1、2），而y字段的取值很丰富。

    ``` {#codeblock_kzi_0q0_18d}
    { x: 1, y: 1 }
    { x: 1, y: 2 }
    { x: 1, y: 3 }
    ......
    { x: 1, y: 100000} 
    { x: 2, y: 1 }
    { x: 2, y: 2 }
    { x: 2, y: 3 }
    ......
    { x: 1, y: 100000}
    ```

    要实现 \{x: 1, y: 2\} 这样的查询。

    ``` {#codeblock_qdv_fjw_pbq}
    db.createIndex( {x: 1} )         效果不好，因为x相同取值太多
    db.createIndex( {x: 1, y: 1} )   效果不好，因为x相同取值太多
    db.createIndex( {y: 1 } )        效果好，因为y相同取值很少
    db.createIndex( {y: 1, x: 1 } )  效果好，因为y相同取值少
    ```

    关于\{y: 1\} 与 \{y: 1, x: 1\} 的区别，可参考[MongoDB索引原理](https://yq.aliyun.com/articles/33726)及[复合索引官方文档](https://docs.mongodb.com/manual/core/index-compound/)。

-   大量数据排序（关键字： SORT、hasSortStage ）

    当查询请求里包含排序的时候， system.profile 集合里的 hasSortStage 字段会为 true 。如果排序无法通过索引满足， MongoDB 会在查询结果中进行排序。而排序这个动作将非常消耗CPU资源，这种情况需要对经常排序的字段建立索引的方式进行优化。

    **说明：** 当您在system.profile集合里发现SORT关键字时，可以考虑通过索引来优化排序。


其他还有诸如建立索引、aggregation（遍历、查询、更新、排序等动作的组合） 等操作也可能非常耗CPU资源，但本质上也是上述几种场景。更多 profiling 的设置请参考[profiling官方文档](https://docs.mongodb.com/manual/tutorial/manage-the-database-profiler/)。

您也可以将MongoDB实例接入至混合云数据库管理HDM（Hybrid Cloud Database Management）。在HDM控制台中，您可以对MongoDB实例的实时性能、实时会话、慢日志、磁盘空间等信息进行监控和管理，详情请参见[HDM操作流程](https://help.aliyun.com/document_detail/64900.html#h2-u64CDu4F5Cu6D41u7A0B3)。

## 服务能力评估 {#section_ytj_4tv_1gb .section}

经过上述分析数据库正在执行的请求和分析数据库慢请求两轮优化之后，整个数据库的查询相对合理，所有的请求都高效地使用了索引。

此时在业务环境使用中还经常遇到CPU资源被占满，那么可能是实例的服务能力已经达到上限了。这种情况下您应当[查看监控信息](../../../../cn.zh-CN/用户指南/监控与报警/查看监控信息.md#)以分析实例资源使用状态；同时对MongoDB数据库进行测试，以便了解在您的业务场景下，当前实例是否满足所需要的设备性能和服务能力。

如您需要升级实例，可以参考[变更配置](../../../../cn.zh-CN/用户指南/实例管理/变更配置.md#)或[变更副本集实例节点数](../../../../cn.zh-CN/用户指南/实例管理/变更副本集实例节点数.md#)进行操作。

