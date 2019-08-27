# Mongo Shell连接时显示Connection reset by peers错误 {#concept_39955_zh .concept}

## 错误提示 {#section_gx7_wmr_0m0 .section}

使用Mongo shell连接实例时，提示类似如下的错误：

```
    2015-12-21T10:20:36.084+0800 I NETWORK  Socket recv() errno:54 Connection reset by peer  1.2.3.4:27017
    2015-12-21T10:20:36.087+0800 I NETWORK  SocketException: remote: 1.2.3.4:27017 error: 9001 socket exception [RECV_ERROR] server [1.2.3.4:27017]
    2015-12-21T10:20:36.087+0800 I NETWORK  DBClientCursor::init call() failed
```

## 可能的原因 {#section_f7b_nk6_1w6 .section}

上述错误信息说明MongoDB实例主动断开了连接，可能该实例的连接数已经达到上限，无法为新的连接请求建立连接。

## 解决方法 {#section_1x6_w49_hmf .section}

**操作步骤**

1.  重启实例来临时释放所有的连接数。
2.  通过Mongo Shell登录数据库。
3.  分析连接来源并限制连接数，详情请参考[如何查询及限制连接数](cn.zh-CN/产品使用问题/如何查询及限制连接数.md#)。

    **说明：** 如果分析连接来源没有异常，可能是实例的性能满足不了当前的业务，您可以升级实例的配置来提升连接数，详情请参考[变更配置](../../../../cn.zh-CN/用户指南/实例管理/变更配置.md#)。


