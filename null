# Connect to an ApsaraDB for MongoDB instance by using the program code

ApsaraDB for MongoDB is compatible with the MongoDB protocol. This topic describes the sample code used to connect to an ApsaraDB for MongoDB instance in different languages.

## Preparations

-   Obtain the connection strings of an ApsaraDB for MongoDB instance based on the instance type. For more information, see the following topics:
    -   [Overview of replica set instance connections]()
    -   [Overview of sharded cluster instance connections]()
-   Download and install the official driver package of your language. For more information, visit Start Developing with MongoDB.

**Note:**

-   The sample code in this topic applies only to internal endpoints of ApsaraDB for MongoDB replica set instances. For other types of instances, replace the relevant content based on actual conditions.
-   To connect to sharded cluster instances, you do not need to specify the replicaSet-related parameters.

## Node.js

Related link: [MongoDB Node.js Driver](https://docs.mongodb.com/drivers/node/current/).

1.  Initialize a project.

    ```
     mkdir node-mongodb-demo
    cd node-mongodb-demo
    npm init 
    ```

2.  Install the driver package and toolkit.

    ```
    npm install mongodb node-uuid sprintf-js -save
    ```

3.  Obtain the information required to connect to an ApsaraDB for MongoDB instance based on the instance type.
4.  Use the following Node.js sample code:

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
    // The officially recommended solution.
    var url = sprintf("mongodb://%s:%d,%s:%d/%s?replicaSet=%s", host1, port1, host2, port2, demoDb, replSetName);
    console.info("url:", url);
    // Obtain the MongoClient.
    mongoClient.connect(url, function (err, db) {
        if (err) {
            console.error("connect err:", err);
            return 1;
        }
        // Authenticate the username and password used to log on to ApsaraDB for MongoDB. The username in this sample code is used to log on to the admin database.
        var adminDb = db.admin();
        adminDb.authenticate(username, password, function (err, result) {
            if (err) {
                console.error("authenticate err:", err);
                return 1;
            }
            // Obtain the collection handle.
            var collection = db.collection(demoColl);
            var demoName = "NODE:" + uuid.v1();
            var doc = { "DEMO": demoName, "MESG": "Hello AliCoudDB For MongoDB" };
            console.info("ready insert document: ", doc);
            // Insert data.
            collection.insertOne(doc, function (err, data) {
                if (err) {
                    console.error("insert err:", err);
                    return 1;
                }
                console.info("insert result:", data["result"]);
                // Read data.
                var filter = { "DEMO": demoName };
                collection.find(filter).toArray(function (err, items) {
                    if (err) {
                        console.error("find err:", err);
                        return 1;
                    }
                    console.info("find document: ", items);
                    // Close the client and release resources.
                    db.close();
                });
            });
        });
    });                   
    ```


## PHP

Related link: [MongoDB PHP Driver](https://docs.mongodb.com/drivers/php/).

1.  Install the driver package and toolkit.

    ```
    $ pecl install mongodb
    $ echo "extension=mongodb.so" >> `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"`
    $ composer require "mongodb/mongodb=^1.0.0" 
    ```

2.  Obtain the information required to connect to an ApsaraDB for MongoDB instance.
3.  Use the following PHP sample code:

    ```
    <?php
    require 'vendor/autoload.php'; // include Composer goodies
    # Specify instance information.
    $demo_seed1 = '**********.mongodb.test.aliyun-inc.com:3717';
    $demo_seed2 = '**********.mongodb.test.aliyun-inc.com:3717';
    $demo_replname = "mgset-**********";
    $demo_user = 'root';
    $demo_password = '**********';
    $demo_db = 'admin';
    # Construct a MongoDB connection string URI based on the instance information.
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


## Java

Related links:

-   Official [Getting Started](http://mongodb.github.io/mongo-java-driver/3.0/driver/getting-started/).
-   JAR package [download](https://repo1.maven.org/maven2/org/mongodb/mongo-java-driver/3.0.4/).

1.  Obtain the information required to connect to an ApsaraDB for MongoDB instance.
2.  Use the following Java sample code:
    -   Maven configurations

        ```
        <dependencies>
            <dependency>
                <groupId>org.mongodb</groupId>
                <artifactId>mongo-java-driver</artifactId>
                <version>4.1.0</version>
            </dependency>
        </dependencies>
        ```

    -   Java sample code

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
                        // Construct a seed list.
                        List<ServerAddress> seedList = new ArrayList<ServerAddress>();
                        seedList.add(seed1);
                        seedList.add(seed2);
                        // Construct authentication information.
                        List<MongoCredential> credentials = new ArrayList<MongoCredential>();
                        credentials.add(MongoCredential.createScramSha1Credential(username, DEFAULT_DB,
                                        password.toCharArray()));
                        // Construct operation options. Configure options other than requiredReplicaSetName based on your actual requirements. The default parameter settings are sufficient in most scenarios.
                        MongoClientOptions options = MongoClientOptions.builder().requiredReplicaSetName(ReplSetName)
                                        .socketTimeout(2000).connectionsPerHost(1).build();
                        return new MongoClient(seedList, credentials, options);
                }
                 public static MongoClient createMongoDBClientWithURI() {
                        // Use a URI to initialize the MongoClient.
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
                                // Obtain the collection handle.
                                MongoDatabase database = client.getDatabase(DEMO_DB);
                                MongoCollection<Document> collection = database.getCollection(DEMO_COLL);
                                // Insert data.
                                Document doc = new Document();
                                String demoname = "JAVA:" + UUID.randomUUID();
                                doc.append("DEMO", demoname);
                                doc.append("MESG", "Hello AliCoudDB For MongoDB");
                                collection.insertOne(doc);
                                System.out.println("insert document: " + doc);
                                // Read data.
                                BsonDocument filter = new BsonDocument();
                                filter.append("DEMO", new BsonString(demoname));
                                MongoCursor<Document> cursor = collection.find(filter).iterator();
                                while (cursor.hasNext()) {
                                        System.out.println("find document: " + cursor.next());
                                }
                        } finally {
                                // Close the client and release resources.
                                client.close();
                        }
                        return;
                }
        }                                                           
        ```


## Python

Related links:

-   [PyMongo download](https://pypi.org/project/pymongo/).
-   [Official documentation](https://pymongo.readthedocs.io/en/stable/).

1.  Install PyMongo.

    ```
    pip install pymongo
    ```

2.  Obtain the information required to connect to an ApsaraDB for MongoDB instance.
3.  Use the following Python sample code:

    ```
    import uuid
    from pymongo import MongoClient
    CONN_ADDR1 = '**********.mongodb.****.******.rdstest.aliyun-inc.com:27017'
    CONN_ADDR2 = '**********.mongodb.****.******.rdstest.aliyun-inc.com:27017'
    REPLICAT_SET = 'mgset-**********'
     username = 'demouser'
    password = '********'
    # Obtain the MongoClient.
    client = MongoClient([CONN_ADDR1, CONN_ADDR2], replicaSet=REPLICAT_SET)
    # Authenticate the username and password used to log on to ApsaraDB for MongoDB. The username in this sample code is used to log on to the admin database.
    client.admin.authenticate(username, password)
    # Insert doc and search for documents based on the demo name. The collection:testColl of the test database is used in the example.
    demo_name = 'python-' + str(uuid.uuid1())
    print 'demo_name:', demo_name
     doc = dict(DEMO=demo_name, MESG="Hello ApsaraDB For MongoDB")
    doc_id = client.test.testColl.insert(doc)
    print 'doc_id:', doc_id
     for d in client.test.testColl.find(dict(DEMO=demo_name)):
        print 'find documents:', d
    ```


## C\#

Related link: [MongoDB C\# Driver](https://docs.mongodb.com/drivers/csharp/).

1.  Install the following driver package:

    ```
    mongocsharpdriver.dll
    ```

2.  Obtain the information required to connect to an ApsaraDB for MongoDB instance.
3.  Use the following C\# sample code:

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
                // Specify instance information.
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
                    Console.WriteLine("connecting...");
                    MongoClientSettings settings = new MongoClientSettings();
                    List<MongoServerAddress> servers = new List<MongoServerAddress>();
                    servers.Add(new MongoServerAddress(host1, port1));
                    servers.Add(new MongoServerAddress(host2, port2));
                    settings.Servers = servers;
                   // Set ReplicaSetName.
                    settings.ReplicaSetName = replicaSetName;
                    // Set ConnectTimeout to 3.
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
                    user.sex = "female";
                    // Insert data user.
                    collection.Insert(user);
                    // Obtain a data entry.
                    User result = collection.FindOne();
                    Console.WriteLine("id:" + result.id + " name:" + result.name + " sex:"+result.sex);
                    Console.WriteLine("connection successful...");
                }
                catch (Exception e)
                {
                    Console.WriteLine("connection failed:"+e.Message);
    
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


## Go

Related link: [MongoDB Go Driver](https://docs.mongodb.com/drivers/go/).

1.  Install the following driver package:

    ```
    go get gopkg.in/mgo.v2
    ```

2.  Obtain the information required to connect to an ApsaraDB for MongoDB instance.
3.  Use the following Go sample code:

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


