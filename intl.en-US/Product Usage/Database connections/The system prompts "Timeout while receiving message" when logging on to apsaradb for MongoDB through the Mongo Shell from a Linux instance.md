# How to troubleshoot logon issues for the mongo shell

You can use DMS or the mongo shell to log on to ApsaraDB for MongoDB. This topic describes the typical problems that may occur when you use the mongo shell to log on to ApsaraDB for MongoDB and the corresponding solutions.

## The message "connection attempt failed" is displayed

Symptom:

```
#mongo --host ali12345678.mongodb.rds.aliyuncs.com:3717 --authenticationDatabase admin -u root -p xxx
MongoDB shell version: 3.2.3
DB Prefix:
connecting to: 10.1.2.8:3717/admin
2016-05-31T15:25:58.940+0800 W NETWORK  Failed to connect to 10. *. *.8:3717 after 5000 milliseconds, giving up.
2016-05-31T15:25:58.943+0800 E QUERY    Error: couldn't connect to server 10. *. *.8:3717 (10.1.2.8), connection attempt failed
    at connect (src/mongo/shell/mongo.js:181:14)
    at (connect):1:6 at src/mongo/shell/mongo.js:181
exception: connect failed
```

|Possible cause|Solution|
|:-------------|:-------|
|The ECS instance on which you run the mongo shell command and the ApsaraDB for MongoDB instance are not in the same VPC or have different network types.|-   If they are not in the same VPC, switch the network type of the ApsaraDB for MongoDB instance to classic network and then switch back to VPC.

**Note:** The VPC must be the same as that of the ECS instance.

-   If they have different network types, perform troubleshooting by referring to [How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different.md). |

Supplementary troubleshooting method: You can run the Telnet command, such as `telnet dds-ali123456789.mongodb.rds.aliyuncs.com 3717`, to check whether the network of the ApsaraDB for MongoDB instance is accessible.

![Test the port](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7837297751/p34454.png)

This figure shows that the URL can be resolved and port 3717 works properly.

## The message "Authentication failed" is displayed

Symptom:

```
#mongo --host ali12345678.mongodb.rds.aliyuncs.com:3717  --authenticationDatabase admin -u root -p xxx
MongoDB shell version: 3.2.3
connecting to: 10.1.2.8:3717/test
2016-05-31T15:50:18.623+0800 E QUERY    Error: 18 Authentication failed.
    at DB._authOrThrow (src/mongo/shell/db.js:1271:32)
    at (auth):6:8
    at (auth):7:2 at src/mongo/shell/db.js:1271
exception: login failed
```

|Possible cause|Solution|
|:-------------|:-------|
|The username used for database logon is incorrect.|Log on to the database with the correct username.|
|The password used for database logon is incorrect.|Log on to the database with the correct user password. If you forget the password, reset the password for the root user in the console. For details, see [t6711.md\#](/intl.en-US/User Guide/Account management/Reset the password for an ApsaraDB for MongoDB instance.md).|
|The logon user does not match the authentication database.|The user must match the authentication database. For example, the root user is a user of the admin database, so the authentication database must be assigned as admin if this user is used to log on.|
|The client version is outdated.|The mongo shell version must be 3.0 or later. For information about how to install the mongo shell, see [Install MongoDB](https://docs.mongodb.com/v3.4/installation/). For version requirements of clients in other programming languages, see [Driver compatibility documentation](https://docs.mongodb.com/ecosystem/drivers/driver-compatibility-reference/).|

## A network error occurs when you run the isMaster command

Symptom:

```
#mongo --host ali12345678.mongodb.rds.aliyuncs.com:3717 --authenticationDatabase test -u root -p xxxxxx
MongoDB shell version v3.4.10
connecting to: mongodb:ali1234567878.mongodb.rds.aliyuncs.com:3717/
2018-12-18T14:26:11.946+0800 E QUERY    [thread1] Error: network error while attempting to run command 'isMaster' on host 'ft12345678.mongodb.rds.aliyuncs.com:3717'  :
connect@src/mongo/shell/mongo.js:237:13
@(connect):1:6
exception: connect failed
```

|Possible cause|Solution|
|:-------------|:-------|
|The IP address of the ECS instance is not in the whitelist of the ApsaraDB for MongoDB instance.|Add the IP address of the ECS instance to the whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).|

## The message "Timeout while receiving message" is displayed

```
org.springframework.data.mongodb.UncategorizedMongoDbException: Timeout while receiving message; nested exception is com.mongodb.MongoSocketReadTimeoutException: Timeout while receiving message
```

|Possible cause|Solution|
|:-------------|:-------|
|Abnormal slow queries occupy instance resources, causing CPU usage to surge or even peak.|Check for slow queries. We recommend that you create indexes for optimization. For more information, see [Analyze slow database requests](/intl.en-US/Best Practices/Performance/Troubleshoot the high CPU utilization of ApsaraDB for MongoDB.md).|
|The configuration of the application connection pool, such as the timeout setting, is incorrect.|For more information, see [Limit the number of connections for terminals](/intl.en-US/Product Usage/Hot issues/How do I query and limit the number of connections?.md).|

## Common connection scenarios

-   [Connect to an ApsaraDB for MongoDB instance over the Internet](/intl.en-US/User Guide/Instance connection/Connect to an ApsaraDB for MongoDB instance over the Internet.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when their network types are different.md)
-   [How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in different regions](/intl.en-US/User Guide/Instance connection/How to connect an ECS instance to an ApsaraDB for MongoDB instance when they are in
         different regions.md)
-   [Connect an ECS instance with an ApsaraDB for MongoDB instance in another Alibaba Cloud account](/intl.en-US/User Guide/Instance connection/Connect an ECS instance with an ApsaraDB for MongoDB instance in another Alibaba Cloud
         account.md)

