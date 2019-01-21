# 使用 Connection String URI 连接分片集群实例 {#concept_51059_zh .concept}

MongoDB分片集群实例提供各个 mongos 节点的连接地址，通过连接 mongos 节点，您可以连接至分片集群实例的数据库。需要注意的是，您需要使用正确的方法连接分片集群实例来实现负载均衡及高可用。

## 背景信息 {#section_n22_mpv_mgb .section}

![分片集群架构](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6750/154803515337678_zh-CN.png)

MongoDB分片集群（Sharded Cluster）通过将数据分散存储到多个分片（Shard）中，以实现高可扩展性。实现分片集群时，MongoDB 引入 Config Server 来存储集群的元数据，引入 mongos 作为应用访问的入口，mongos 从 Config Server 读取路由信息，并将请求路由到后端对应的 Shard 上。

-   用户访问 mongos 跟访问单个 mongod 类似。
-   所有 mongos 是对等关系，用户访问分片集群可通过任意一个或多个 mongos 。
-   mongos 本身是无状态的，可任意扩展，集群的服务能力为“Shard服务能力之和”与“mongos服务能力之和”的最小值。
-   访问分片集群时，最好将应用负载均匀地分散到多个 mongos 上。

## Connection String URI 连接说明 { .section}

要正确连接分片集群实例，您需要先了解下MongoDB的[Connection String URI](https://docs.mongodb.com/manual/reference/connection-string/)，所有官方的[driver](https://docs.mongodb.com/manual/applications/drivers/)都支持以 Connection String URI 的方式来连接MongoDB数据库。

Connection String URI 示例：

```
mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]
```

**说明：** 

-    `mongodb://` 前缀，代表这是一个Connection String URI 。
-    `username:password@` 登录数据库的用户和密码信息。
-    `hostX:portX`多个 mongos 的地址列表。
-    `/database`鉴权时，用户帐号所属的数据库。
-    `?options` 指定额外的连接选项。

## 如何正确地连接分片集群实例 {#section_tm2_lqv_mgb .section}

云数据库MongoDB提供了 Connection String URI 连接方式。使用 Connection String URI 连接方式进行连接，可实现负载均衡及高可用。

1.  获取分片集群实例的 Connection String URI 连接信息，详情请参考[分片集群实例连接说明](../../../../../intl.zh-CN/分片集群快速入门/连接实例/分片集群实例连接说明.md#)。

    ![Connection String URI连接信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6750/154803515337679_zh-CN.png)

2.  应用程序中设置使用 Connection String URI 来连接实例，详情请参考[程序代码连接](../../../../../intl.zh-CN/分片集群快速入门/连接实例/程序代码连接.md#)。

    通过 java 来连接的示例代码如下所示。

    ```language-java
    MongoClientURI connectionString = new MongoClientURI("mongodb://:****@s-m5e80a9241323604.mongodb.rds.aliyuncs.com:3717,s-m5e053215007f404.mongodb.rds.aliyuncs.com:3717/admin"); // ****替换为root密码
    MongoClient client = new MongoClient(connectionString);
    MongoDatabase database = client.getDatabase("mydb");
    MongoCollection<Document> collection = database.getCollection("mycoll");
    ```

    **说明：** 

    通过上述方式连接分片集群时，客户端会自动将请求分散到多个 mongos 上，以实现负载均衡。同时，当 URI 里 mongos 数量在2个及以上时，当有 mongos 故障时，客户端能自动进行切换，将请求都分散到状态正常的 mongos 上。


当 mongos 数量很多时，您可以按应用将 mongos 进行分组。例如有2个应用 A、B，实例有4个 mongos，可以让应用 A 访问 mongos 1-2（URI 里只指定 mongos 1-2 的地址）， 应用 B 来访问 mongos 3-4（URI 里只指定 mongos 3-4 的地址）。根据这种方法来实现应用间的访问隔离。

**说明：** 应用访问的 mongos 彼此隔离，但后端 Shard 仍然是共享的。

## 常用连接参数 { .section}

-   如何实现读写分离

    在 Connection String URI 的**options**里添加`readPreference=secondaryPreferred`，设置读请求为Secondary节点优先。

    示例

    ```
    mongodb://root:xxxxxxxx@dds-xxxxxxxxxxxx:3717,xxxxxxxxxxxx:3717/admin?replicaSet=mgset-xxxxxx&readPreference=secondaryPreferred
    ```

-   如何限制连接数

    在 Connection String URI 的**options**里添加 `maxPoolSize=xx` ，即可将客户端连接池中的连接数限制在xx以内。

-   如何保证数据写入到大多数节点后才返回

    在 Connection String URI 的**options**里添加 `w= majority` ，即可保证写请求成功写入大多数节点才向客户端确认。


