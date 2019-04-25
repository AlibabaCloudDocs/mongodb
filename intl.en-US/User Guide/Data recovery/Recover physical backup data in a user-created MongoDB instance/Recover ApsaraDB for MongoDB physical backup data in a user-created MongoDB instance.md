# Recover ApsaraDB for MongoDB physical backup data in a user-created MongoDB instance {#concept_lf5_qxp_5fb .concept}

You can log on to the ApsaraDB for MongoDB console to download a physical backup file from an ApsaraDB for MongoDB instance. This topic describes how to recover ApsaraDB for MongoDB physical backup data in a user-created MongoDB instance.

## Prerequisites {#section_kdp_sxp_5fb .section}

-   This feature applies only to ApsaraDB for MongoDB replica set instances.
-   The storage engine of the ApsaraDB for MongoDB instance must be WiredTiger or RocksDB.

    **Note:** If the storage engine of the ApsaraDB for MongoDB instance is TerarkDB, you can recover logical backup data in the user-created MongoDB instance. For more information, see [Recover logical backup data in a user-created MongoDB instance](intl.en-US/User Guide/Data recovery/Recover logical backup data in a user-created MongoDB instance.md#).

-   If the storage engine of the ApsaraDB for MongoDB instance is RocksDB, you need to compile and install a MongoDB application that is configured with the RocksDB storage engine.
-   The user-created MongoDB instance must be compatible with the ApsaraDB for MongoDB instance. The following table lists the mappings between the database versions of the ApsaraDB for MongoDB instance and the user-created MongoDB instance.

    |Database version of the ApsaraDB for MongoDB instance|Database version of the user-created MongoDB instance|
    |:----------------------------------------------------|:----------------------------------------------------|
    |MongoDB 3.2|MongoDB 3.2 or MongoDB 3.4|
    |MongoDB 3.4|MongoDB 3.4|
    |MongoDB 4.0|MongoDB 4.0|


## Preparations {#section_lxg_5xp_5fb .section}

The following procedure uses a Linux server as an example. \(MongoDB of the required version has been installed on the Linux server. For more information about how to install MongoDB, see the official MongoDB manual.\)

Download a physical backup file from an ApsaraDB for MongoDB instance and decompress the downloaded file in the user-created MongoDB instance.

1.  [Download a physical backup file from an ApsaraDB for MongoDB instance](intl.en-US/User Guide/Data recovery/Recover physical backup data in a user-created MongoDB instance/Download the physical backup data of a replica set instance.md#).
2.  Clear data from the data directory \(**which must be empty**\) where MongoDB is installed on the local server.

    Assume that /path/to/mongo is the directory used for physical recovery operations of the user-created MongoDB instance.

    ```
    cd /path/to/mongo/data/
    rm -rf *
    ```

3.  Copy the downloaded ApsaraDB for MongoDB physical backup file to the /path/to/mongo/data/ directory and decompress the file.

    ```
    tar xzvf hins_xxx.tar.gz 
    ```


## Recover ApsaraDB for MongoDB physical backup data in standalone mode {#section_pwz_yxp_5fb .section}

1.  Create a mongod.conf file in the /path/to/mongo directory.

    ```
    touch mongod.conf
    ```

2.  Modify the mongod.conf file to meet the configuration requirements for starting the user-created MongoDB instance recovered from ApsaraDB for MongoDB physical backup data.

    Based on the storage engine, select a configuration template for the startup of the user-created MongoDB instance in standalone mode with authentication enabled. You can copy the selected configuration template to the mongod.conf file.

    -   WiredTiger

        ```
        systemLog:
            destination: file
            path: /path/to/mongo/mongod.log
            logAppend: true
        security:
            authorization: enabled
        storage:
            dbPath: /path/to/mongo/data
            directoryPerDB: true
        net:
            http:
                enabled: false
            port: 27017
            unixDomainSocket:
                enabled: false
        processManagement:
            fork: true
            pidFilePath: /path/to/mongo/mongod.pid
        ```

        **Note:** The ApsaraDB for MongoDB instance is configured with the WiredTiger storage engine by default, and the **directoryPerDB** option is enabled. Therefore, this option is specified in the configuration.

    -   RocksDB

        ```
        systemLog:
        	destination: file
        	path: /path/to/mongo/logs/mongod.log
        	logAppend: true
        security:
        	authorization: enabled​
        storage:
        	dbPath: /path/to/mongo/data
                engine: rocksdb
        net:
        	http:
        		enabled: false
        	port: 27017
        	unixDomainSocket:
        		enabled: false
        processManagement:
        	fork: true
        	pidFilePath: /path/to/mongo/logs/mongod.pid
        ```

3.  Use the new configuration file mongod.conf to start the user-created MongoDB instance.

    ```
    /usr/bin/mongod -f /path/to/mongo/mongod.conf
    ```

4.  Log on to the user-created MongoDB instance through the mongo shell on the local server.

    ```
    mongo --host 127.0.0.1 -u <username> -p <password> --authenticationDatabase admin
    ```

    Notes:

    -   <username\>: The database username used to log on to the ApsaraDB for MongoDB instance. The default username is root.
    -   <password\>: The database password used to log on to the ApsaraDB for MongoDB instance.

## Start the user-created MongoDB instance in replica set mode {#section_c4j_fcs_5fb .section}

ApsaraDB for MongoDB physical backup data contains the replica set configuration of the original ApsaraDB for MongoDB instance by default. You need to start the user-created MongoDB instance in standalone mode. Otherwise, you may fail to access it.

To start the user-created MongoDB instance in replica set mode, you need to [recover ApsaraDB for MongoDB physical backup data in standalone mode](#section_pwz_yxp_5fb) first and do as follows:

1.  Log on to the user-created MongoDB instance through the mongo shell on the local server.
2.  Remove the original replica set configuration.

    ```
    use local
    db.system.replset.remove({})
    ```

3.  Shut down MongoDB.

    ```
    use admin
    db.shutdownServer()
    					
    ```

4.  Modify the mongod.conf file in the /path/to/mongo/ directory to add the replication configuration. For more information about the command, see [Deploy a Replica Set](https://docs.mongodb.com/manual/tutorial/deploy-replica-set/index.html) in the official MongoDB manual.
5.  Use the new configuration file mongod.conf to start the user-created MongoDB instance.

    ```
    /usr/bin/mongod -f /path/to/mongo/mongod.conf
    ```

6.  Add started nodes to a replica set and initialize the replica set.

    **Note:** This step uses an `rs.initiate()` command. For more information about the command, see [rs.initiate\(\)](https://docs.mongodb.com/manual/reference/method/rs.initiate/) in the official MongoDB manual.


