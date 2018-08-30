# MongoDB客户端SSL连接示例 {#concept_ant_1kw_y2b .concept}

云数据库MongoDB设置了sslAllowConnectionsWithoutCertificates，使用SSL连接客户端时不需要证书 ，但需要配置Ca验证服务器证书，同时忽略域名检测。

设置SSL加密请参见[SSL加密](intl.zh-CN/用户指南/安全/SSL加密.md#)。

## Node.js SSL连接示例 {#section_sbw_lhw_y2b .section}

**相关链接**：[MongoDB Node.js Driver](http://mongodb.github.io/node-mongodb-native/2.0/tutorials/enterprise_features/)

**示例代码**

将/?ssl = true添加到客户端URI的末尾，sslCA指向ca证书路径，checkServerIndentity设置为false，忽略域名检测。

```
var MongoClient = require('mongodb').MongoClient,
  f = require('util').format,
  fs = require('fs');

// Read the certificate authority
var ca = [fs.readFileSync(__dirname + "/path/to/ca.pem")];

// Connect validating the returned certificates from the server
MongoClient.connect("mongodb://host01:27017,host02:27017,host03:27017/?replicaSet=myreplset&ssl=true", {
  server: {
      sslValidate:true,
      checkServerIdentity:false,#ignore host name validation
      sslCA:ca
  }
}, function(err, db) {
  db.close();
});
```

## PHP SSL连接示例 {#section_vvq_shw_y2b .section}

**相关链接**：[MongoDB PHP Driver](https://docs.mongodb.com/php-library/master/reference/method/MongoDBClient__construct/index.html)

**示例代码**

PHP使用MongoDB\\Client::\_\_construct创建client实例。其包含三组参数：$uri、$uriOptions和$driverOptions。

```
function __construct($uri = 'mongodb://127.0.0.1/', array $uriOptions = [], array $driverOptions = [])
```

通过$uriOptions设置ssl为true，启用ssl连接。通过$driverOptions设置ca\_file指向ca证书路径。allow\_invalid\_hostname设置为true，忽略域名检测。

```
<?php
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
?>
```

## Java SSL连接示例 {#section_ncg_f3w_y2b .section}

**相关链接**：[MongoDB Java Driver](http://mongodb.github.io/mongo-java-driver/3.0/driver/reference/connecting/ssl/)

**示例代码**

将MongoClientOptions设置sslEnabled为True，启用ssl连接。将sslInvalidHostNameAllowed设置为true，忽略域名检测。

```
import com.mongodb.MongoClientURI;
import com.mongodb.MongoClientOptions;
MongoClientOptions options
= MongoClientOptions.builder().sslEnabled(true).sslInvalidHostNameAllowed(true).build();
MongoClient client = new MongoClient("mongodb://host01:27017,host02:27017,host03:27017/?replicaSet=myreplset", options);
```

java设置ca证书，需要使用keytool工具：

```
keytool -importcert -trustcacerts -file <path to certificate authority file> 
        -keystore <path to trust store> -storepass <password>
```

在程序中设置JVM 系统属性以指向正确的信任库和密钥库。

```
System.setProperty("javax.net.ssl.trustStore","/trust/mongoStore.ts");
System.setProperty("javax.net.ssl.trustStorePassword","StorePass");
```

## Python SSL连接示例 {#section_rkc_43w_y2b .section}

**相关链接**：[MongoDB Python Driver](http://api.mongodb.com/python/current/examples/tls.html?_ga=2.57718378.1155670878.1532603447-1232357619.1526624834&amp;_gac=1.125002488.1532603447.CjwKCAjw4uXaBRAcEiwAuAUz8HGUi3R9xvI1e_uYZo6IN3vi9dwy_Ozh2bq6VLYfkYE5O-W_3SWYaxoCPtIQAvD_BwE)

**示例代码**

设置ssl=True启用ssl连接，ssl\_ca\_certs参数用来指向ca文件路径，ssl\_match\_hostnames设置为False，忽略域名检测。

```
import ssl
from pymongo import MongoClient

uri = "mongodb://host01:27017,host02:27017,host03:27017/?replicaSet=myreplset"
client = MongoClient(uri,
                     ssl=True,
                     ssl_ca_certs='ca.pem',
                     ssl_match_hostnames=False)
```

## C SSL连接示例 {#section_x1q_r3w_y2b .section}

**相关链接**：[MongoDB C Driver](http://mongoc.org/libmongoc/current/advanced-connections.html)

**示例代码**

将/?ssl = true添加到客户端URI的末尾，C使用[mongoc\_ssl\_opt\_t](http://mongoc.org/libmongoc/current/mongoc_ssl_opt_t.html)来配置ssl选项，ca\_file指向ca证书路径。将allow\_invalid\_hostname设置为false，忽略域名检测。

```
mongoc_client_t *client = NULL;
client = mongoc_client_new (
      "mongodb://host01:27017,host02:27017,host03:27017/?replicaSet=myreplset&ssl=true");
const mongoc_ssl_opt_t *ssl_default = mongoc_ssl_opt_get_default ();
mongoc_ssl_opt_t ssl_opts = { 0 };

/* optionally copy in a custom trust directory or file; otherwise the default is used. */
memcpy (&ssl_opts, ssl_default, sizeof ssl_opts);
ssl_opts.ca_file = "/path/to/ca.pem"
ssl_opts.allow_invalid_hostname = false
mongoc_client_set_ssl_opts (client, &ssl_opts);
```

## C ++ SSL连接示例 {#section_s3r_w3w_y2b .section}

**相关链接**：[MongoDB C++ Driver](https://mongodb.github.io/mongo-cxx-driver/mongocxx-v3/configuration/)

**示例代码**

将/?ssl = true添加到客户端URI的末尾。C++通过 [mongocxx::options::ssl](https://mongodb.github.io/mongo-cxx-driver/api/mongocxx-v3/classmongocxx_1_1options_1_1ssl.html) 设置SSL参数，ca\_file参数用来指定ca文件路径。

**说明：** mongocxx驱动现不支持忽略域名检测。

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
    uri{"mongodb://host01:27017,host02:27017,host03:27017/?replicaSet=myreplset&ssl=true"}, client_opts};

```

## Scala SSL连接示例 {#section_ayt_1jw_y2b .section}

**相关链接**：[MongoDB Scala Driver](http://mongodb.github.io/mongo-scala-driver/2.2/reference/connecting/ssl/)

**示例代码**

Scala驱动程序使用Netty提供的SSL底层支持与MongoDB服务器进行SSL连接。其中，将MongoClientOptions设置sslEnabled为True，启用ssl连接；将sslInvalidHostNameAllowed设置为true，忽略域名检测。

```
import org.mongodb.scala.connection.{NettyStreamFactoryFactory, SslSettings}

MongoClientSettings.builder()
                   .sslSettings(SslSettings.builder()
                                           .enabled(true)                 
                                           .invalidHostNameAllowed(true)  
                                           .build())                      
                   .streamFactoryFactory(NettyStreamFactoryFactory())
                   .build()
val client: MongoClient = MongoClient("mongodb://host01:27017,host02:27017,host03:27017/?replicaSet=myreplset")

```

scala设置ca证书与java相同，同样需要使用keytool工具。

```
keytool -importcert -trustcacerts -file <path to certificate authority file> 
        -keystore <path to trust store> -storepass <password>
```

在程序中设置JVM 系统属性以指向正确的信任库和密钥库。

```
System.setProperty("javax.net.ssl.trustStore","/trust/mongoStore.ts");
System.setProperty("javax.net.ssl.trustStorePassword","StorePass");
```

## Golang SSL连接示例 {#section_wkp_ljw_y2b .section}

**相关链接**：[MongoDB Golang Driver](https://godoc.org/github.com/globalsign/mgo)、[Crypto tls package](https://golang.org/pkg/crypto/tls/)

**示例代码**

Golang驱动程序使用crypto/tls包提供的SSL底层支持与MongoDB服务器进行SSL连接。其中，Config结构用来配置ssl选项 ；RootCAs用来指定ca证书；InsecureSkipVerify设置为true，忽略域名检测。

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
url := "mongodb://host01:27017,host02:27017,host03:27017/?replicaSet=myreplset&ssl=true"
dialInfo, err := ParseURL(url)
dialInfo.DialServer = func(addr *ServerAddr) (net.Conn, error) {
    return tls.Dial("tcp", addr.String(), tlsConfig)
}

session, err := DialWithInfo(dialInfo)
if err != nil {
    panic(err)
}
session.Close()

```

