# SSL connection sample code for MongoDB drivers

ApsaraDB for MongoDB supports sslAllowConnectionsWithoutCertificates to allow you to establish SSL connections to MongoDB clients without a certificate. However, you must configure the CA to verify the server certificate and ignore hostname verification.

For more information about how to configure SSL encryption, see [Configure SSL encryption for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure SSL encryption for an ApsaraDB for MongoDB instance.md).

## Node.js

For more information, visit [MongoDB Node.js Driver](http://mongodb.github.io/node-mongodb-native/2.0/tutorials/enterprise_features/).

Sample code

Add /?ssl = true to the end of the MongoDB client URI, set sslCA to the path of the CA certificate, and then set checkServerIndentity to false to ignore hostname verification.

```
var MongoClient = require('mongodb').MongoClient,
  f = require('util').format,
  fs = require('fs');

// Read the certificate authority
var ca = [fs.readFileSync(__dirname + "/path/to/ca.pem")];

// Connect validating the returned certificates from the server
MongoClient.connect("mongodb://host01:27017,host02:27017,host03:27017/? replicaSet=myreplset&ssl=true", {
  server: {
      sslValidate:true,
      checkServerIdentity:false,#ignore host name validation
      sslCA:ca
  }
}, function(err, db) {
  db.close();
});
```

## PHP

For more information, visit [MongoDB Node.js Driver](https://docs.mongodb.com/php-library/master/reference/method/MongoDBClient__construct/index.html).

Sample code

Use MongoDB\\Client::\_\_construct to create a client instance with the following groups of parameters: $uri, $uriOptions, and $driverOptions.

```
function __construct($uri = 'mongodb://127.0.0.1/', array $uriOptions = [], array $driverOptions = [])
```

In $uriOptions, set ssl to true to enable SSL connection. In $driverOptions, set ca\_file to the path of the CA certificate. Set allow\_invalid\_hostname to true to ignore hostname verification. In $uriOptions, set ssl to true to enable SSL connection. In $driverOptions, set ca\_file to the path of the CA certificate. Set allow\_invalid\_hostname to true to ignore hostname verification.

```
<? php
$client = new MongoDB\Client(
    'mongodb://host01:27017,host02:27017,host03:27017',
    [   'ssl' => true,
        'replicaSet' => 'myReplicaSet'
    ],
    [
        "ca_file" => "/path/to/ca.pem",
        "allow_invalid_hostname" => true

    ]
);
? >
```

## Java

For more information, visit [MongoDB Node.js Driver](http://mongodb.github.io/mongo-java-driver/3.0/driver/reference/connecting/ssl/).

Sample code

In MongoClientOptions, set sslEnabled to true to enable SSL connection. Set sslInvalidHostNameAllowed to true to ignore hostname verification.

```
import com.mongodb.MongoClientURI;
import com.mongodb.MongoClientOptions;
MongoClientOptions options
= MongoClientOptions.builder().sslEnabled(true).sslInvalidHostNameAllowed(true).build();
MongoClient client = new MongoClient("mongodb://host01:27017,host02:27017,host03:27017/? replicaSet=myreplset", options);
```

Run a keytool command to specify the CA certificate.

```
keytool -importcert -trustcacerts -file <path to certificate authority file> 
        -keystore <path to trust store> -storepass <password>
```

Set Java Virtual Machine \(JVM\) system properties to specify the correct trust store and password store.

```
System.setProperty("javax.net.ssl.trustStore","/trust/mongoStore.ts");
System.setProperty("javax.net.ssl.trustStorePassword","StorePass");
```

## Python

For more information, visit [MongoDB Python Driver](http://api.mongodb.com/python/current/examples/tls.html?_ga=2.57718378.1155670878.1532603447-1232357619.1526624834&amp;_gac=1.125002488.1532603447.CjwKCAjw4uXaBRAcEiwAuAUz8HGUi3R9xvI1e_uYZo6IN3vi9dwy_Ozh2bq6VLYfkYE5O-W_3SWYaxoCPtIQAvD_BwE).

Sample code

Set ssl to True to enable SSL connection, set ssl\_ca\_certs to the path of the CA certificate, and then set ssl\_match\_hostname to False to ignore hostname verification.

```
import ssl
from pymongo import MongoClient

uri = "mongodb://host01:27017,host02:27017,host03:27017/? replicaSet=myreplset"
client = MongoClient(uri,
                     ssl=True,
                     ssl_ca_certs='ca.pem',
                     ssl_match_hostname=False)
```

## C

For more information, visit [MongoDB C Driver](http://mongoc.org/libmongoc/current/advanced-connections.html).

Sample code

Add /?ssl = true to the end of the MongoDB client URI. Use [mongoc\_ssl\_opt\_t](http://mongoc.org/libmongoc/current/mongoc_ssl_opt_t.html) to set SSL options and set ca\_file to the path of the CA certificate. Set allow\_invalid\_hostname to false to ignore hostname verification.

```
mongoc_client_t *client = NULL;
client = mongoc_client_new (
      "mongodb://host01:27017,host02:27017,host03:27017/? replicaSet=myreplset&ssl=true");
const mongoc_ssl_opt_t *ssl_default = mongoc_ssl_opt_get_default ();
mongoc_ssl_opt_t ssl_opts = { 0 };

/* optionally copy in a custom trust directory or file; otherwise the default is used. */
memcpy (&ssl_opts, ssl_default, sizeof ssl_opts);
ssl_opts.ca_file = "/path/to/ca.pem"
ssl_opts.allow_invalid_hostname = false
mongoc_client_set_ssl_opts (client, &ssl_opts);
```

## C++

For more information, visit [MongoDB C++ Driver](https://mongodb.github.io/mongo-cxx-driver/mongocxx-v3/configuration/).

Sample code

Add /?ssl = true to the end of the MongoDB client URI. Use [mongocxx::options::ssl](https://mongodb.github.io/mongo-cxx-driver/api/mongocxx-v3/classmongocxx_1_1options_1_1ssl.html) to set SSL parameters and set ca\_file to the path of the CA certificate.

**Note:** You cannot ignore hostname verification for the MongoDB C++ driver.

```
#include <mongocxx/client.hpp>
#include <mongocxx/uri.hpp>
#include <mongocxx/options/client.hpp>
#include <mongocxx/options/ssl.hpp>

mongocxx::options::client client_options;
mongocxx::options::ssl ssl_options;

// If the server certificate is not signed by a well-known CA,
// you can set a custom CA file with the `ca_file` option.
ssl_options.ca_file("/path/to/ca.pem");

client_options.ssl_opts(ssl_options);

auto client = mongocxx::client{
    uri{"mongodb://host01:27017,host02:27017,host03:27017/? replicaSet=myreplset&ssl=true"}, client_opts};
                
```

## Scala

For more information, visit [MongoDB Scala Driver](http://mongodb.github.io/mongo-scala-driver/2.2/reference/connecting/ssl/).

Sample code

The MongoDB Scala driver uses the underlying SSL provided by Netty to support SSL connections to MongoDB servers. In MongoClientOptions, set sslEnabled to true to enable SSL connection and set sslInvalidHostNameAllowed to true to ignore hostname verification.

```
import org.mongodb.scala.connection.{ NettyStreamFactoryFactory, SslSettings}

MongoClientSettings.builder()
                   .sslSettings(SslSettings.builder()
                                           .enabled(true)                 
                                           .invalidHostNameAllowed(true)  
                                           .build())                      
                   .streamFactoryFactory(NettyStreamFactoryFactory())
                   .build()
val client: MongoClient = MongoClient("mongodb://host01:27017,host02:27017,host03:27017/? replicaSet=myreplset")
                
```

Run a keytool command to specify the CA certificate, which is the same as the method for Java.

```
keytool -importcert -trustcacerts -file <path to certificate authority file> 
        -keystore <path to trust store> -storepass <password>
```

Set JVM system properties to specify the correct trust store and password store.

```
System.setProperty("javax.net.ssl.trustStore","/trust/mongoStore.ts");
System.setProperty("javax.net.ssl.trustStorePassword","StorePass");
```

## Golang

For more information, visit [MongoDB Golang Driver](https://godoc.org/github.com/globalsign/mgo) and [Crypto tls package](https://golang.org/pkg/crypto/tls/).

Sample code

The MongoDB Golang driver uses the underlying SSL provided by Netty to support SSL connections to MongoDB servers. Use Config to set SSL options. Set RootCAs to specify the CA certificate and set InsecureSkipVerify to true to ignore hostname verification.

```
import (
    "crypto/tls"
    "crypto/x509"
    "gopkg.in/mgo.v2
)
rootPEM, err := ioutil.ReadFile("path/to/ca.pem")
roots := x509.NewCertPool()
ok := roots.AppendCertsFromPEM([]byte(rootPEM)
tlsConfig := &tls.Config{
                  RootCAs: roots,
       InsecureSkipVerify: true
}
url := "mongodb://host01:27017,host02:27017,host03:27017/? replicaSet=myreplset&ssl=true"
dialInfo, err := ParseURL(url)
dialInfo.DialServer = func(addr *ServerAddr) (net.Conn, error) {
    return tls.Dial("tcp", addr.String(), tlsConfig)
}

session, err := DialWithInfo(dialInfo)
if err ! = nil {
    panic(err)
}
session.Close()
                
```

## .NET Core

1.  Install .NET. For more information, visit [Download .NET](https://dotnet.microsoft.com/download).
2.  Create a project and go to the project directory.

    ```
    dotnet new console -o MongoDB
    cd MongoDB
    ```

3.  Run the following command to install the driver package of .NET Core for MongoDB.

    ```
    dotnet add package mongocsharpdriver --version 2.11.5
    ```


Sample code

```
using System;
using System.Collections.Generic;
using System.Security.Cryptography.X509Certificates;
using MongoDB.Bson;
using MongoDB.Driver;namespace dotnetCase
{
class Program
{
static void Main(string[] args)
{
// Specify instance information.
const string host1 = "dds-***********-pub.mongodb.rds.aliyuncs.com";
const int port1 = 3717;
const string host2 = "dds-***********-pub.mongodb.rds.aliyuncs.com";
const int port2 = 3717;
const string replicaSetName = "mgset-********"; // Delete this row for a sharded cluster instance.
const string admin = "admin";
const string userName = "root";
const string passwd = "********";        
try
        {
            // Set the host information for connection.
            MongoClientSettings settings = new MongoClientSettings();
            List servers = new List();
            servers.Add(new MongoServerAddress(host1, port1));
            servers.Add(new MongoServerAddress(host2, port2));
            settings.Servers = servers;
            // Set the replica set instance name. Delete this row for a sharded cluster instance.
            settings.ReplicaSetName = replicaSetName;
            // Set the timeout period to 3 seconds.
            settings.ConnectTimeout = new TimeSpan(0, 0, 0, 3, 0);
            // Set the logon user and password.
            MongoCredential credentials = MongoCredential.CreateCredential(admin, userName, passwd);
            settings.Credential = credentials;
            // Set the SSL information.
            SslSettings sslSettings = new SslSettings{
                ClientCertificates = new[] {new X509Certificate("ca.pem")},
            };
            settings.UseTls = true;
            settings.AllowInsecureTls = true;
            settings.SslSettings = sslSettings;
            // Initialize the client.
            MongoClient client = new MongoClient(settings);
        }
        catch (Exception e)
        {
            Console.WriteLine("connection failed:"+e.Message);
        }
    }
}
}
```

