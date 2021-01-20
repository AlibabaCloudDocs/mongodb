# Use MongoShake to implement delayed synchronization among ApsaraDB for MongoDB instances

This topic describes how to use MongoShake to synchronize data among ApsaraDB for MongoDB instances after a buffer period.

The MongoShake version must be 2.4.6 or later. For more information, visit the [MongoShake releases page](https://github.com/alibaba/MongoShake).

If you use MongoShake to synchronize data among multiple instances in real time, MongoShake synchronizes misoperations on the primary instance to the secondary instances. In this case, you must restore data of the secondary instances to undo the misoperations. To resolve this issue, a parameter is added to MongoShake version 2.4.6 to allow delayed synchronization. This feature provides a buffer period for data synchronization among ApsaraDB for MongoDB instances. If a misoperation is performed on the primary instance, you can disable synchronization during the buffer period and migrate your workloads to a secondary instance to which the incorrect data is not synchronized.

**Note:** This topic describes how to use the `incr_sync.target_delay` parameter. For more information about how to use MongoShake, see [Use MongoShake to implement one-way synchronization between ApsaraDB for MongoDB replica set instances](/intl.en-US/User Guide/Data migration and synchronization/Data synchronization/Use MongoShake to implement one-way synchronization between ApsaraDB for MongoDB replica
         set instances.md).

## Preparations

1.  For best synchronization performance, make sure that the source ApsaraDB for MongoDB replica set instance resides in a VPC. If the source instance resides in the classic network, switch the network type to VPC. For more information, see [Switch the network type of an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Network connection management/Switch the network type of an ApsaraDB for MongoDB instance.md).

2.  Create an ApsaraDB for MongoDB replica set instance as the synchronization destination. Select the same VPC as the one used by the source ApsaraDB for MongoDB replica set instance to minimize network latency. For more information, see [Create a replica set instance](/intl.en-US/Quick Start/Create an instance/Create a replica set instance.md).

3.  Create an ECS instance to run MongoShake. Select the same VPC as the one used by the source ApsaraDB for MongoDB instance to minimize network latency. For more information, see [t9601.dita\#topic\_2386095]().

4.  Add the private IP address of the ECS instance to the whitelists of the source and destination ApsaraDB for MongoDB instances. Make sure that the ECS instance can connect to the source and destination ApsaraDB for MongoDB instances. For more information, see [Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).


**Note:** If the network type does not meet the preceding requirements, you can apply for public endpoints for the source and destination ApsaraDB for MongoDB instances. Then, add the public IP address of the ECS instance to the whitelists of the source and destination ApsaraDB for MongoDB instances. This way, you can synchronize data by using the Internet. For more information, see [Apply for a public endpoint for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Network connection management/Public IP Connection/Apply for a public endpoint for an ApsaraDB for MongoDB instance.md) and [Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).

## Configure delayed synchronization among ApsaraDB for MongoDB instances

The following example uses an Ubuntu Elastic Compute Service \(ECS\) instance to describe how to configure delayed synchronization among ApsaraDB for MongoDB instances. For more information, see [Preparations](#section_prc_09g_855).

1.  Log on to the [ECS instance](https://www.alibabacloud.com/help/zh/doc-detail/25434.htm).

2.  Run the following command to download the MongoShake program:

    ```
    wget <Download address of the latest MongoShake package>
    ```

    Example:

    ```
    wget https://github.com/alibaba/MongoShake/releases/download/release-v2.0.7-20190817/mongo-shake-2.0.7.tar.gz
    ```

    **Note:** The download address of the latest MongoShake package is listed on the [MongoShake releases page](https://github.com/alibaba/MongoShake/releases).

3.  Run the following command to decompress the MongoShake package:

    ```
    tar xvf <Name of the MongoShake package>
    ```

    Example:

    ```
    tar xvf mongoshake-2.0.tar.gz
    ```

4.  Run the `vi collector.conf` command to configure MongoShake. For information about the configuration parameters, see [MongoShake parameters](/intl.en-US/User Guide/Data migration and synchronization/Data synchronization/Use MongoShake to implement one-way synchronization between ApsaraDB for MongoDB replica
         set instances.md). Find the `incr_sync.target_delay` parameter in the collector.conf file and set this parameter based on your needs. The unit is seconds. In this example, the buffer period is set to 1,800 seconds.

    ```
    incr_sync.target_delay = 1800
    ```

5.  Save and close the collector.conf file to complete the configuration.

6.  Run the following command to start synchronization based on the collector.conf file and print the logs.

    ```
    ./collector.linux -conf=collector.conf -verbose
    ```

    **Note:** MongoShake synchronizes changes in the primary instance to secondary instances 30 minutes after the changes.


## Perform a switchover between the primary instance and a secondary instance after a misoperation

When you perform create, read, update, and delete \(CURD\) operations on the primary instance, a misoperation may occur. For example, a statement is executed to write unwanted data to the primary instance. To respond to a misoperation, you can follow these steps to migrate your workloads to a secondary instance to which the incorrect data is not synchronized.

1.  Query the operation logs of the primary ApsaraDB for MongoDB instance to identify the time when the misoperation occurred. For example, you can run the following command to query all operation logs that were generated from June 1, 2020 to June 2, 2020. For more information about how to query operation logs, see [MongoDB official documentation](https://docs.mongodb.com/manual/reference/command/find/).

    ```
    use local#Switch to the local database.
    db.oplog.rs.find({"o.createTime": {$gte:new Date(2020,6,1),$lte:new Date(2020,6,2)}}) #Query operation logs based on the specified conditions.
    ```

2.  Run the following Restful API command to inject the ExitPoint parameter to MongoShake to terminate the MongoShake program at a specified time.

    ```
    curl -X POST --data '{"ExitPoint": <UNIX timestamp>}' <MongoShake server ID>:<Port number>/sentinel/options
    ```

    Example:

    ```
    curl -X POST --data '{"ExitPoint": 1593534600}' 127.0.0.1:9100/sentinel/options
    ```

    **Note:** The string `1593534600` is a UNIX timestamp that indicates 16:30:00 June 30, 2020. MongoShake automatically exits at the specified time.

3.  Run the `vi collector.conf` command to open the configuration file and exchange the IP addresses of the primary instance and the secondary instance. For more information, see [Use MongoShake to implement one-way synchronization between ApsaraDB for MongoDB replica set instances](/intl.en-US/User Guide/Data migration and synchronization/Data synchronization/Use MongoShake to implement one-way synchronization between ApsaraDB for MongoDB replica
         set instances.md).

4.  Run the following command to restart synchronization based on the collector.conf file and print the logs.

    ```
    ./collector.linux -conf=collector.conf -verbose
    ```

5.  Migrate your workloads to the new primary instance to complete the switchover operation.


## Monitor the MongoShake status

For more information, see [Monitor the MongoShake status](/intl.en-US/User Guide/Data migration and synchronization/Data synchronization/Use MongoShake to implement one-way synchronization between ApsaraDB for MongoDB replica
         set instances.md).

