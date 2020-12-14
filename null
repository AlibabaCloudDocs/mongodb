# Connect to an ApsaraDB for MongoDB instance through the program code

## Related links

-   [MongoDB Drivers](https://docs.mongodb.org/ecosystem/drivers/)
-   [Connection String URI Format](https://docs.mongodb.org/manual/reference/connection-string/)

    **Note:** The connection sample code in this topic applies when you use internal IP addresses provided by Alibaba Cloud to connect to ApsaraDB for MongoDB.

-   For more information about how to obtain connection strings of ApsaraDB for MongoDB, see [Connect to an ApsaraDB for MongoDB instance](https://www.alibabacloud.com/help/zh/doc-detail/55188.htm).

## Node.js

Related links: [MongoDB Node.js Driver](https://docs.mongodb.org/getting-started/node/client/)

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

3.  Obtain connection strings of ApsaraDB for MongoDB instances.
4.  Use the following Node.js sample code.

    ```
        'use strict';
        var uuid = require('node-uuid');
        var sprintf = require("sprintf-js").sprintf;
        var mongoClient = require('mongodb').MongoClient;
        var host1 = "demotest-1.mongodb.tbc3.newtest.rdstest.aliyun-inc.com";
        var port1 = 27017;
        var host2 = "demotest-2.mongodb.tbc3.newtest.rdstest.aliyun-inc.com";
        var port2 = 27017;
        var username = "demouser";
        var password = "123456";
        var replSetName = "mgset-1441984991";
        var demoDb = "test";
        var demoColl = "testColl";
        // The officially recommended solution.
        var url = sprintf("mongodb://%s:%d,%s:%d/%s? replicaSet=%s", host1, port1, host2, port2, demoDb, replSetName);
        console.info("url:", url);
        // Obtain the MongoClient.
        mongoClient.connect(url, function(err, db) {
            if(err) {
                console.error("connect err:", err);
                return 1;
            }
            // Authenticate. Here, the username is for authentication of the admin database.
            var adminDb = db.admin();
            adminDb.authenticate(username, password, function(err, result) {
                if(err) {
                    console.error("authenticate err:", err);
                    return 1;
                }
                // Obtain the collection handle.
                var collection = db.collection(demoColl);
                var demoName = "NODE:" + uuid.v1();
                var doc = {"DEMO": demoName, "MESG": "Hello AliCoudDB For MongoDB"};
                console.info("ready insert document: ", doc);
                // Insert data.
                collection.insertOne(doc, function(err, data) {
                    if(err) {
                        console.error("insert err:", err);
                        return 1;
                    }
                    console.info("insert result:", data["result"]);
                    // Read data.
                    var filter = {"DEMO": demoName};
                    collection.find(filter).toArray(function(err, items) {
                        if(err) {
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

Related links:

[Mongodb php driver](https://docs.mongodb.org/ecosystem/drivers/php/)

1.  Install the driver package and toolkit.

    ```
        $ pecl install mongodb
        $ echo "extension=mongodb.so" >> `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"` 
        $ composer require "mongodb/mongodb=^1.0.0"
    ```

2.  Obtain connection strings of ApsaraDB for MongoDB instances.
3.  Use the following PHP sample code.

    ```
        <? php
        require 'vendor/autoload.php'; // include Composer goodies
            # Instance information
            $demo_seed1 = 'demotest-1.mongodb.test.aliyun-inc.com:3717';
            $demo_seed2 = 'demotest-2.mongodb.test.aliyun-inc.com:3717';
            $demo_replname = "mgset-1441984463";
            $demo_user = 'root';
            $demo_password = '123456';
            $demo_db = 'admin';
            # Construct the mongodb connection string based on the instance information.
            # mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][? options]]
            $demo_uri = 'mongodb://' . $demo_user . ':' . $demo_password . '@' .
              $demo_seed1 . ',' . $demo_seed2 . '/' . $demo_db . '? replicaSet=' . $demo_replname;
            $client = new MongoDB\Client($demo_uri);
            $collection = $client->testDb->testColl;
            $result = $collection->insertOne( [ 'name' => 'ApsaraDB for Mongodb', 'desc' => 'Hello, Mongodb'  ] );
            echo "Inserted with Object ID '{$result->getInsertedId()}'", "\n";
            $result = $collection->find( [ 'name' => 'ApsaraDB for Mongodb'] );
            foreach ($result as $entry)
            {
              echo $entry->_id, ': ', $entry->name, "\n";
            }
        ? >
    ```


## Java

Related links:

-   Official [Quick Start](http://mongodb.github.io/mongo-java-driver/3.0/driver/getting-started/)
-   JAR package [download](https://oss.sonatype.org/content/repositories/releases/org/mongodb/mongo-java-driver/3.0.4/)

1.  Obtain connection strings of ApsaraDB for MongoDB instances.
2.  Use the following Java sample code.

    -   Maven configuration

        ```
            <dependencies> 
                <dependency> 
                    <groupId>org.mongodb</groupId>
                    <artifactId>mongo-java-driver</artifactId>
                    <version>3.0.4</version>
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
                public static ServerAddress seed1 = new ServerAddress("demotest-1.mongodb.tbc3.newtest.rdstest.aliyun-inc.com", 27017);
                public static ServerAddress seed2 = new ServerAddress("demotest-2.mongodb.tbc3.newtest.rdstest.aliyun-inc.com", 27017);
                public static String username = "demouser";
                public static String password = "123456";
                public static String ReplSetName = "mgset-1441984463";
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
                    credentials.add(MongoCredential.createScramSha1Credential(username,
                            DEFAULT_DB, password.toCharArray()));
                    // Construct operation options. Configure options other than requiredReplicaSetName based on your actual requirements. The default parameter settings are sufficient for most scenarios.
                    MongoClientOptions options = MongoClientOptions.builder()
                            .requiredReplicaSetName(ReplSetName).socketTimeout(2000)
                            .connectionsPerHost(1).build();
                    return new MongoClient(seedList, credentials, options);
                }
                public static MongoClient createMongoDBClientWithURI() {
                    // Use a URI to initialize the MongoClient.
                    //mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][? options]]
                    MongoClientURI connectionString = new MongoClientURI("mongodb://" + username + ":" + password + "@" + 
                                                                         seed1 + "," + seed2 + "/" + 
                                                                         DEFAULT_DB + 
                                                                         "? replicaSet=" + ReplSetName);
                    return new MongoClient(connectionString);
                }
                public static void main(String args[]) {
                    MongoClient client = createMongoDBClient();
                    //or
                    //MongoClient client = createMongoDBClientWithURI();
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
                    return ;
                }
            }
        ```


## Python

Related links:

-   [Pymongo download](https://pypi.python.org/pypi/pymongo/)
-   [Official documentation](http://api.mongodb.org/python/current/index.html)

1.  Install PyMongo.

    ```
        pip install pymongo
    ```

2.  Obtain the connection strings of ApsaraDB for MongoDB instances.
3.  Use the following Python sample code.

    ```
        import uuid
            from pymongo import MongoClient
            # Specify two addresses used to connect to the primary and secondary nodes of the instance.
            CONN_ADDR1 = 'demotest-1.mongodb.tbc3.newtest.rdstest.aliyun-inc.com:27017'
            CONN_ADDR2 = 'demotest-2.mongodb.tbc3.newtest.rdstest.aliyun-inc.com:27017'
            REPLICAT_SET = 'mgset-1441984463'
            username = 'demouser'
            password = '123456'
            # Obtain the MongoClient.
            client = MongoClient([CONN_ADDR1, CONN_ADDR2], replicaSet=REPLICAT_SET)
            # Authenticate. Here, the username is for authentication of the admin database.
            client.admin.authenticate(username, password)
            # Use the collection:testColl of the test database as an example. Insert doc and search for documents based on the demo name.
            demo_name = 'python-' + str(uuid.uuid1())
            print 'demo_name:', demo_name
            doc = dict(DEMO=demo_name, MESG="Hello ApsaraDB For MongoDB")
            doc_id = client.test.testColl.insert(doc)
            print 'doc_id:', doc_id
            for d in client.test.testColl.find(dict(DEMO=demo_name)):
                print 'find documents:', d
    ```


