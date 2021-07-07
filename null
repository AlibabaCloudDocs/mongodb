# 通过程序代码连接MongoDB实例

云数据库MongoDB版完全兼容MongoDB协议，本文介绍各类程序连接数据库的相关示例。

## 准备工作

-   根据您的实例类型获取云数据库MongoDB连接地址。更多信息，请参见：
    -   [副本集实例连接说明]()
    -   [分片集群实例连接说明]()
-   根据您使用的语言下载并安装官方驱动程序。更多信息，请参见[MongoDB Drivers](https://docs.mongodb.org/ecosystem/drivers/)。

**说明：**

-   本文连接Demo仅适用于阿里云提供的MongoDB副本集实例内网连接地址，其他类型实例请根据实际情况替换相关内容。
-   连接分片集群实例时，无需指定下列Demo中的replicaSet相关参数。

## Node.js 连接示例

相关链接：[MongoDB Node.js Driver](https://docs.mongodb.com/drivers/node/)。

1.  项目初始化。

    ```
    mkdir node-mongodb-demo
    cd node-mongodb-demo
    npm init
    ```

2.  安装驱动包以及工具包。

    ```
    npm install mongodb node-uuid sprintf-js –save
    ```

3.  根据您的实例类型获取云数据库MongoDB连接信息。
4.  Node.js Demo Code。

    ```
    'use strict';
    var uuid = require('node-uuid');
    var sprintf = require("sprintf-js").sprintf;
    var mongoClient = require('mongodb').MongoClient;
    var host1 = "**********.mongodb.tbc3.newtest.rdstest.aliyun-inc.com";
    var port1 = 27017;
    var host2 = "**********.mongodb.tbc3.newtest.rdstest.aliyun-inc.com";
    var port2 = 27017;
    var username = "demouser";
    var password = "**********";
    var replSetName = "mgset-**********";
    var demoDb = "test";
    var demoColl = "testColl";
    // 官方建议使用的方案
    var url = sprintf("mongodb://%s:%d,%s:%d/%s?replicaSet=%s", host1, port1, host2, port2, demoDb, replSetName);
    console.info("url:", url);
    //获取mongoClient
    mongoClient.connect(url, function (err, db) {
        if (err) {
            console.error("connect err:", err);
            return 1;
        }
        //授权. 这里的username基于admin数据库授权
        var adminDb = db.admin();
        adminDb.authenticate(username, password, function (err, result) {
            if (err) {
                console.error("authenticate err:", err);
                return 1;
            }
            //取得Collecton句柄
            var collection = db.collection(demoColl);
            var demoName = "NODE:" + uuid.v1();
            var doc = { "DEMO": demoName, "MESG": "Hello AliCoudDB For MongoDB" };
            console.info("ready insert document: ", doc);
            // 插入数据
            collection.insertOne(doc, function (err, data) {
                if (err) {
                    console.error("insert err:", err);
                    return 1;
                }
                console.info("insert result:", data["result"]);
                // 读取数据
                var filter = { "DEMO": demoName };
                collection.find(filter).toArray(function (err, items) {
                    if (err) {
                        console.error("find err:", err);
                        return 1;
                    }
                    console.info("find document: ", items);
                    //关闭Client，释放资源
                    db.close();
                });
            });
        });
    });
    ```


## PHP 连接示例

相关链接：[MongoDB PHP Driver](https://docs.mongodb.org/ecosystem/drivers/php/)。

1.  安装驱动包以及工具包。

    ```
    $ pecl install mongodb
    $ echo "extension=mongodb.so" >> `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"`
    $ composer require "mongodb/mongodb=^1.0.0"
    ```

2.  获取云数据库 MongoDB 连接信息。
3.  PHP Demo Code。

    ```
    <?php
    require 'vendor/autoload.php'; // include Composer goodies
    # 实例信息
    $demo_seed1 = '**********.mongodb.test.aliyun-inc.com:3717';
    $demo_seed2 = '**********.mongodb.test.aliyun-inc.com:3717';
    $demo_replname = "mgset-**********";
    $demo_user = 'root';
    $demo_password = '**********';
    $demo_db = 'admin';
    # 根据实例信息构造mongodb connection string
    # mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]
    $demo_uri = 'mongodb://' . $demo_user . ':' . $demo_password . '@' .
        $demo_seed1 . ',' . $demo_seed2 . '/' . $demo_db . '?replicaSet=' . $demo_replname;
    $client = new MongoDB\Client($demo_uri);
    $collection = $client->testDb->testColl;
    $result = $collection->insertOne(['name' => 'ApsaraDB for Mongodb', 'desc' => 'Hello, Mongodb']);
    echo "Inserted with Object ID '{$result->getInsertedId()}'", "\n";
    $result = $collection->find(['name' => 'ApsaraDB for Mongodb']);
    foreach ($result as $entry) {
        echo $entry->_id, ': ', $entry->name, "\n";
    }
    ?>
    ```


## Java 连接示例

相关链接：

-   官方[Quick Start](http://mongodb.github.io/mongo-java-driver/3.0/driver/getting-started/)文档。
-   下载[Jar包](https://oss.sonatype.org/content/repositories/releases/org/mongodb/mongo-java-driver/3.0.4/)。

1.  获取云数据库 MongoDB 连接信息。
2.  Java Demo Code。
    -   Maven配置。

        ```
        <dependencies>
            <dependency>
                <groupId>org.mongodb</groupId>
                <artifactId>mongo-java-driver</artifactId>
                <version>4.1.0</version>
            </dependency>
        </dependencies>
        ```

    -   Java Code。

        ```
        import java.util.ArrayList;
        import java.util.List;
        import java.util.UUID;
        import org.bson.BsonDocument;
        import org.bson.BsonString;
        import org.bson.Document;
        import com.mongodb.MongoClient;
        import com.mongodb.MongoClientOptions;
        import com.mongodb.MongoClientURI;
        import com.mongodb.MongoCredential;
        import com.mongodb.ServerAddress;
        import com.mongodb.client.MongoCollection;
        import com.mongodb.client.MongoCursor;
        import com.mongodb.client.MongoDatabase;
         public class Main {
                public static ServerAddress seed1 = new ServerAddress("**********.mongodb.tbc3.newtest.rdstest.aliyun-inc.com",
                                27017);
                public static ServerAddress seed2 = new ServerAddress("**********.mongodb.tbc3.newtest.rdstest.aliyun-inc.com",
                                27017);
                public static String username = "demouser";
                public static String password = "**********";
                public static String ReplSetName = "mgset-**********";
                public static String DEFAULT_DB = "admin";
                public static String DEMO_DB = "test";
                public static String DEMO_COLL = "testColl";
                 public static MongoClient createMongoDBClient() {
                        // 构建Seed列表
                        List<ServerAddress> seedList = new ArrayList<ServerAddress>();
                        seedList.add(seed1);
                        seedList.add(seed2);
                        // 构建鉴权信息
                        List<MongoCredential> credentials = new ArrayList<MongoCredential>();
                        credentials.add(MongoCredential.createScramSha1Credential(username, DEFAULT_DB,
                                        password.toCharArray()));
                        // 构建操作选项，requiredReplicaSetName属性外的选项根据自己的实际需求配置，默认参数满足大多数场景
                        MongoClientOptions options = MongoClientOptions.builder().requiredReplicaSetName(ReplSetName)
                                        .socketTimeout(2000).connectionsPerHost(1).build();
                        return new MongoClient(seedList, credentials, options);
                }
                 public static MongoClient createMongoDBClientWithURI() {
                        // 另一种通过URI初始化
                        // mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]
                        MongoClientURI connectionString = new MongoClientURI("mongodb://" + username + ":" + password + "@"
                                        + seed1 + "," + seed2 + "/" + DEFAULT_DB + "?replicaSet=" + ReplSetName);
                        return new MongoClient(connectionString);
                }
                 public static void main(String args[]) {
                        MongoClient client = createMongoDBClient();
                        // or
                        // MongoClient client = createMongoDBClientWithURI();
                        try {
                                // 取得Collecton句柄
                                MongoDatabase database = client.getDatabase(DEMO_DB);
                                MongoCollection<Document> collection = database.getCollection(DEMO_COLL);
                                // 插入数据
                                Document doc = new Document();
                                String demoname = "JAVA:" + UUID.randomUUID();
                                doc.append("DEMO", demoname);
                                doc.append("MESG", "Hello AliCoudDB For MongoDB");
                                collection.insertOne(doc);
                                System.out.println("insert document: " + doc);
                                // 读取数据
                                BsonDocument filter = new BsonDocument();
                                filter.append("DEMO", new BsonString(demoname));
                                MongoCursor<Document> cursor = collection.find(filter).iterator();
                                while (cursor.hasNext()) {
                                        System.out.println("find document: " + cursor.next());
                                }
                        } finally {
                                // 关闭Client，释放资源
                                client.close();
                        }
                        return;
                }
        }
        ```


## Python 连接示例

相关链接：

-   [pymongo下载地址](https://pypi.python.org/pypi/pymongo/)。
-   [官方文档](https://pymongo.readthedocs.io/en/stable/)。

1.  安装pymongo。

    ```
    pip install pymongo
    ```

2.  获取云数据库 MongoDB 连接信息。
3.  Python Demo Code。

    ```
    import uuid
    from pymongo import MongoClient
    CONN_ADDR1 = '**********.mongodb.****.******.rdstest.aliyun-inc.com:27017'
    CONN_ADDR2 = '**********.mongodb.****.******.rdstest.aliyun-inc.com:27017'
    REPLICAT_SET = 'mgset-**********'
     username = 'demouser'
    password = '********'
     #获取mongoclient
    client = MongoClient([CONN_ADDR1, CONN_ADDR2], replicaSet=REPLICAT_SET)
     #授权。 这里的user基于admin数据库授权。
    client.admin.authenticate(username, password)
     #使用test数据库的collection:testColl做例子, 插入doc, 然后根据DEMO名查找。
    demo_name = 'python-' + str(uuid.uuid1())
    print 'demo_name:', demo_name
     doc = dict(DEMO=demo_name, MESG="Hello ApsaraDB For MongoDB")
    doc_id = client.test.testColl.insert(doc)
    print 'doc_id:', doc_id
     for d in client.test.testColl.find(dict(DEMO=demo_name)):
        print 'find documents:', d
    ```


## C\# 连接示例

相关链接：[MongoDB C\# Driver](https://docs.mongodb.com/ecosystem/drivers/csharp/)。

1.  安装如下驱动包。

    ```
    mongocsharpdriver.dll
    ```

2.  获取云数据库 MongoDB 连接信息。
3.  C\# Demo Code。

    ```
    using MongoDB.Driver;
    using System;
    using System.Collections.Generic;
    
    namespace Aliyun
    {
        class Program
        {
            static void Main(string[] args)
            {
                //Mongo 实例信息
                const string host1 = "dds-t4n**************.mongodb.singapore.rds.aliyuncs.com";
                const int port1 = 3717;
                const string host2 = "dds-t4n**************.mongodb.singapore.rds.aliyuncs.com";
                const int port2 = 3717;
                const string replicaSetName = "mgset-300******";
                const string admin = "admin";
                const string userName = "root";
                const string passwd = "********";
    
                try
                {
                    Console.WriteLine("开始连接.......");
                    MongoClientSettings settings = new MongoClientSettings();
                    List<MongoServerAddress> servers = new List<MongoServerAddress>();
                    servers.Add(new MongoServerAddress(host1, port1));
                    servers.Add(new MongoServerAddress(host2, port2));
                    settings.Servers = servers;
                    //设置副本集名称
                    settings.ReplicaSetName = replicaSetName;
                    //设置超时时间为3秒
                    settings.ConnectTimeout = new TimeSpan(0, 0, 0, 3, 0);
                    MongoCredential credentials = MongoCredential.CreateCredential(admin, userName, passwd);
                    settings.Credential = credentials;
                    MongoClient client = new MongoClient(settings);
                    var server = client.GetServer();
                    MongoDatabase database = server.GetDatabase("test");
                    var collection = database.GetCollection<User>("test_collection");
                    User user = new User();
                    user.id = "1";
                    user.name = "mongo_test";
                    user.sex = "女";
                    //插入数据user
                    collection.Insert(user);
                    //获取一条数据
                    User result = collection.FindOne();
                    Console.WriteLine("id:" + result.id + " name:" + result.name + " sex:"+result.sex);
                    Console.WriteLine("连接成功.........");
                }
                catch (Exception e)
                {
                    Console.WriteLine("连接异常:"+e.Message);
    
                }
            }
        }
        class User
        {
            public string id { set; get; }
            public string name { set; get; }
            public string sex { set; get; }
    
        }
    }
    ```


## Go 连接示例

相关链接：[MongoDB Go Driver](https://docs.mongodb.com/drivers/go)。

1.  安装如下驱动包。

    ```
    go get gopkg.in/mgo.v2
    ```

2.  获取云数据库 MongoDB 连接信息。
3.  Go Demo Code。

    ```
    package main
    import (
    "fmt"
    "log"
    "time""gopkg.in/mgo.v2"
    "gopkg.in/mgo.v2/bson"
    )
    type Person struct {
    Name  string
    Phone string
    }
    func main() {
    fmt.Println("hello world")
    dialInfo := &mgo.DialInfo{
    Addrs:     []string{"dds-bp1***********-pub.mongodb.rds.aliyuncs.com:3717", "dds-bp1***********-pub.mongodb.rds.aliyuncs.com:3717"},
    Direct:    false,
    Timeout:   time.Second * 1,
    Database:  "admin",
    Source:    "admin",
    Username:  "root",
    Password:  "********", 
    }
    session, err := mgo.DialWithInfo(dialInfo)
    if err != nil {
    fmt.Printf("dial failed: %v",err)
    return
    }
    defer session.Close()
    
    session.SetMode(mgo.Monotonic, true)
    
    c := session.DB("test").C("test_collection")
    err = c.Insert(&Person{"Ale", "+55 53 8116 9639"},
        &Person{"Cla", "+55 53 8402 8510"})
    if err != nil {
        log.Fatal(err)
    }
    
    result := Person{}
    err = c.Find(bson.M{"name": "Ale"}).One(&result)
    if err != nil {
        log.Fatal(err)
    }
    
    fmt.Println("Phone:", result.Phone)
    }
    ```


