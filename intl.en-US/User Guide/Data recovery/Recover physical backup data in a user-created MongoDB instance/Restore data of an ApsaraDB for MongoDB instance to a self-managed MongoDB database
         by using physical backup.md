---
keyword: [backup and restoration, database restoration]
---

# Restore data of an ApsaraDB for MongoDB instance to a self-managed MongoDB database by using physical backup

This topic describes how to restore data of an ApsaraDB for MongoDB instance to a MongoDB database by using physical backup. Before you start to restore data, you must download the physical backup data of the ApsaraDB for MongoDB instance in the ApsaraDB for MongoDB console.

## Prerequisites

-   The ApsaraDB for MongoDB instance is a replica set instance.
-   The Transparent Data Encryption \(TDE\) feature is disabled for the ApsaraDB for MongoDB instance. For more information, see [Configure TDE for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure TDE for an ApsaraDB for MongoDB instance.md).
-   The storage engine of the ApsaraDB for MongoDB instance is WiredTiger or RocksDB. If the storage engine is TerarkDB, use logical backup to restore data of the ApsaraDB for MongoDB instance to the MongoDB database. For more information, see [Restore data of an ApsaraDB for MongoDB instance to user-created MongoDB databases by using logical backup](/intl.en-US/User Guide/Data recovery/Restore data of an ApsaraDB for MongoDB instance to user-created MongoDB databases by using logical backup.md).

    **Note:**

    -   You can view the storage engine of an ApsaraDB for MongoDB instance on the **Basic Information** page in the ApsaraDB for MongoDB console.
    -   If the storage engine is RocksDB, you must compile and install MongoDB for the MongoDB database to support the RocksDB storage engine.

## Database version requirements

The version of the ApsaraDB for MongoDB instance must correspond to the version of the MongoDB database. The following table lists the mappings between the ApsaraDB for MongoDB instance and the MongoDB database.

|ApsaraDB for MongoDB instance|Self-managed MongoDB database|
|:----------------------------|:----------------------------|
|V3.2|3.2 or 3.4|
|V3.4|3.4|
|V4.0|4.0|
|V4.2|4.2|

## Formats of physical backup files

|Physical backup file format|File extension|Description|
|---------------------------|--------------|-----------|
|tar|.tar.gz|ApsaraDB for MongoDB instances that were created before March 26, 2019 have physical backup files in the .tar format.|
|xbstream|\_qp.xb|ApsaraDB for MongoDB instances that were created on or after March 26, 2019 have physical backup files in the .xbstream format.**Note:** The .xbstream format is available only for Linux. The .xbstream format is not available for Windows because Windows does not support the Percona XtraBackup tool that is used to decompress the files in the .xbstream format. |

**Note:** You must use different methods to decompress the packages in the preceding two file formats. For more information, see [Step 2: Download and decompress a physical backup file](#section_lxg_5xp_5fb).

## Environment preparation

The following procedure uses an ECS instance created from a Ubuntu 16.04 64-bit image. For more information, see [Create an ECS instance](~~25424~~).

**Note:**

-   MongoDB of the required version is installed on the ECS instance. For more information about how to install MongoDB, visit [Install MongoDB](https://docs.mongodb.com/guides/server/install/).
-   Environment variables are configured for the MongoDB database on the ECS instance. When you run commands, you do not need to enter executable file paths again. For more information, see [Configure environment variables](#section_qbj_vae_xyv).
-   The /root/mongo/data directory of the ECS instance is used for the replica set instance.
-   The /root/mongo/data1 and /root/mongo/data1 directories of the ECS instance are used for the MongoDB database in a replica set node.
-   When you execute the commands that are provided in this topic on the ECS instance, you must press the Enter key after you enter the last command.

## Step 1: Configure environment variables

Configure environment variables for the MongoDB database. This way, you do not need to enter executable file paths when you run commands. Before you perform this step, make sure that MongoDB is installed. For more information, visit [Install MongoDB](https://docs.mongodb.com/guides/server/install/).

**Note:** If environment variables are configured for MongoDB, skip this step and perform [Step 2: Download and decompress a physical backup file](#section_lxg_5xp_5fb).

1.  Run the following command to open the `profile` file in Linux:

    ```
    vi /etc/profile
    ```

2.  Press the `I` key to enter the edit mode. Then, enter the following code in the last line:

    ```
    export PATH=$PATH:/<The path of the MongoDB server>/bin
    ```

    The following figure shows an example.

    ![Configure environment variables](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6482651161/p201717.png)

    **Note:** /root/mongo/bin is used as the path of the MongoDB server in this example. Use the actual path when you configure environment variables.

3.  Press the Esc key to exit the edit mode, and enter `:wq` to save the file and exit.
4.  Run the following command to make the configured environments variables take effect:

    ```
    source /etc/profile
    ```


## Step 2: Download and decompress a physical backup file

1.  Download the physical backup data of the ApsaraDB for MongoDB instance in the ApsaraDB for MongoDB console. For more information, see [Download the physical backup data of a replica set instance](/intl.en-US/User Guide/Data recovery/Recover physical backup data in a user-created MongoDB instance/Download the physical backup data of a replica set instance.md). You can also run the following command to download the data:

    ```
    wget -c '<The external download URL of the data backup file>' -O <The name that you want to use for the downloaded data backup file> <File name extension>
    ```

    **Note:** Make sure that the file extension is `.tar.gz` or `_qp.xb`.

2.  Run the following command to create a directory named `data` in the /root/mongo/ directory. Then, move the downloaded physical backup file of the ApsaraDB for MongoDB instance to the /root/mongo/data/ directory:

    ```
    mkdir -p /root/mongo/data && mv <<The name of the physical backup file>.<File name extension>> /root/mongo/data 
    ```

3.  Decompress the physical backup file.
    -   If the physical backup file has a .tar.gz extension, such as hins20190412.tar.gz, run the following command to decompress the file:

        ```
        cd /root/mongo/data/ && tar xzvf hins20190412.tar.gz 
        ```

        ![Decompression result](../images/p70466.png "Decompression result")

    -   If the physical backup file has a \_qp.xb extension, such as hins20190412\_qp.xb, perform the following operations to decompress the file:
        1.  Install the Percona XtraBackup tool.

            ```
            apt-get update
            apt install percona-xtrabackup
            ```

        2.  Download the qpress tool package. For the download URL, visit [QuickLZ](http://www.quicklz.com/).
        3.  Decompress the qpress tool package and install the tool.

            ```
            tar xvf qpress-11-linux-x64.tar
            chmod 775 qpress
            cp qpress /usr/bin
            ```

        4.  Decompress the physical backup file. In this example, the file is hins20190412\_qp.xb.

            ```
            cd /root/mongo/data/
            cat hins20190412_qp.xb | xbstream -x -v
            innobackupex --decompress --remove-original /root/mongo/data
            ```

            ![Decompression result](../images/p70454.png "Decompression result")


## Step 3: Restore data to the MongoDB database in standalone mode

1.  Run the following command to create a configuration file named mongod.conf in the /root/mongo directory:

    ```
    touch /root/mongo/mongod.conf
    ```

2.  On the command line, enter `vi /root/mongo/mongod.conf` to open the mongod.conf file. Press the `I` key to enter the edit mode.

    You can select a configuration template based on the storage engine of the ApsaraDB for MongoDB instance, and copy the selected configuration template to the mongod.conf configuration file.

    **Note:** In this file, enable standalone startup and authorization.

    -   WiredTiger

        ```
        systemLog:
            destination: file
            path: /root/mongo/mongod.log
            logAppend: true
        security:
            authorization: enabled
        storage:
            dbPath: /root/mongo/data
            directoryPerDB: true
        net:
            port: 27017
            unixDomainSocket:
                enabled: false
        processManagement:
            fork: true
            pidFilePath: /root/mongo/mongod.pid
        ```

        **Note:** By default, ApsaraDB for MongoDB uses the WiredTiger storage engine, and the directoryPerDB option is enabled. Therefore, the directoryPerDB option is set to true in the preceding configuration.

    -   RocksDB

        ```
        systemLog:
            destination: file
            path: /root/mongo/logs/mongod.log
            logAppend: true
        security:
            authorization: enabled
        storage:
            dbPath: /root/mongo/data
                engine: rocksdb
        net:
            port: 27017
            unixDomainSocket:
                enabled: false
        processManagement:
            fork: true
            pidFilePath: /root/mongo/mongod.pid
        ```

3.  Press the Esc key to exit the edit mode. Then, enter `:wq` to save the file and exit.
4.  Use the mongod.conf configuration file to start MongoDB.

    ```
    mongod -f /root/mongo/mongod.conf
    ```

    ![Example of a successful start](../images/p207008.png "Example of a successful start")

5.  After you start MongoDB, run the following command to log on to the ApsaraDB for MongoDB database and go to the mongo shell:

    ```
    mongo --host 127.0.0.1 -u <username> -p <password> --authenticationDatabase admin
    ```

    Parameter description:

    -   <username\>: the account used to log on to the MongoDB database. The default value is root.
    -   <password\>: the password used to log on to the MongoDB database.
    ![Example of a successful logon](../images/p207011.png "Example of a successful logon")

6.  Run the `show dbs` command in the mongo shell to query all the available databases on the MongoDB server. This way, you can check whether the recovery is successful.
7.  Run the `exit` command in the mongo shell to exit the mongo shell.

## Step 4: Start the MongoDB database in replica set mode

By default, the physical backup file of the ApsaraDB for MongoDB instance contains the replica set configuration. You must start MongoDB in standalone mode. Otherwise, the MongoDB database may be inaccessible.

If you want to start MongoDB in replica set mode, you must [restore data to the MongoDB database in standalone mode](#section_pwz_yxp_5fb) before you perform the following operations:

1.  On the command line, log on to the database as the root user by using the mongo shell.

    ```
    mongo --host 127.0.0.1 -u root -p <root account password> --authenticationDatabase admin
    ```

2.  After you log on to the database, run the commands in the following code block to perform the following operations:

    1.  Create a temporary user in the admin database and grant the temporary user the read and write permissions on the local database.
    2.  Switch to the temporary user and delete the original replica set configuration of the local database.
    3.  Switch back to the root user and delete the temporary user and the temporary permissions.

        **Note:** Replace `<The password of the root account>` in the following code with the password of your root account.

    ```
    use admin
    db.runCommand({
        createRole: "tmprole",
        roles: [
            {
                role: "root",
                db: "admin"
            }
        ],
        privileges: [
            {
                resource: {
                    db: 'local',
                    collection: 'system.replset'
                },
                actions: [
                    'remove'
                ]
            }
        ]
    })
    db.runCommand({
        createUser: "tmpuser",
        pwd: "tmppwd",
        roles: [
            'tmprole'
        ]
    })
    db.auth('tmpuser','tmppwd')
    use local
    db.system.replset.remove({})
    use admin
    db.auth('root','<The password of the root account>')
    db.dropRole('tmprole')
    db.dropUser('tmpuser')
    ```

    ![Example of an execution result](../images/p207017.png "Example of an execution result")

    **Note:** The root user has the read-only permissions on the `system.replset` collection in the local database. The root user cannot change its own permissions. Therefore, the system.replset collection can be deleted only by another user that has the required permissions.

3.  Run the following commands to shut down the MongoDB service and exit the mongo shell:

    ```
    use admin
    db.shutdownServer()
    exit
    ```

    ![Example of an execution result](../images/p207018.png "Example of an execution result")

4.  Create the authentication file on the replica set.

    To start MongoDB in replica set mode, you must create a key file for all replica set nodes to authenticate each other.

    1.  Run the following command to create the keyFile folder in the mongo directory as the authentication file directory and create a key file in the authentication file directory.

        ```
        mkdir -p /root/mongo/keyFile && touch /root/mongo/keyFile/mongodb.key
        ```

    2.  Run the `vi /root/mongo/keyFile/mongodb.key` command to open the mongodb.key file. Press the `I` key to enter the edit mode. Example:

        ```
        MongoDB Encrypting File
        ```

        **Note:** The key that is used to encrypt data has the following limits:

        -   The key must be 6 to 1,024 characters in length.
        -   The key can contain only Base64-encoded characters.
        -   The key cannot contain equal signs \(=\).
    3.  Press the Esc key to exit the edit mode, and enter `:wq` to save the file and exit.
    4.  On the command line, run the following command to assign `400` permissions on the authentication file. This way, only the owner of the file can view the content of the file.

        ```
        sudo chmod 400 /root/mongo/keyFile/mongodb.key
        ```

    **Note:** This authentication file is applied to all replica set nodes.

5.  Perform the following operations to prepare two empty nodes for the replica set:
    1.  Run the following command to create two copies of the mongod.conf file. The two copies are used as the configuration files for the other two nodes.

        ```
        cp /root/mongo/mongod.conf /root/mongo/mongod1.conf && cp /root/mongo/mongod.conf /root/mongo/mongod2.conf
        ```

    2.  Run the following command to create data directories for the other two nodes:

        ```
        mkdir -p /root/mongo/data1 && mkdir -p /root/mongo/data2
        ```

6.  Modify the configuration file of each node by performing the following operations:

    -   Run the `vi /root/mongo/mongod.conf` command to open the configuration file of Node 1. Modify the file based on the following content. Then, save and exit the configuration file.

        ```
        systemLog:
            destination: file
            path: /root/mongo/mongod.log
            logAppend: true
        security:
            authorization: enabled
            keyFile: /root/mongo/keyFile/mongodb.key
        storage:
            dbPath: /root/mongo/data
            directoryPerDB: true
        net:
            bindIp: 127.0.0.1
            port: 27017
            unixDomainSocket:
                enabled: false
        processManagement:
            fork: true
            pidFilePath: /root/mongo/mongod.pid
        replication:
            replSetName: "rs0"
        ```

    -   Run the `vi /root/mongo/mongod1.conf` command to open the configuration file of Node 2. Modify the file based on the following content. Then, save and exit the configuration file.

        ```
        systemLog:
            destination: file
            path: /root/mongo/mongod1.log
            logAppend: true
        security:
            authorization: enabled
            keyFile: /root/mongo/keyFile/mongodb.key
        storage:
            dbPath: /root/mongo/data1
            directoryPerDB: true
        net:
            bindIp: 127.0.0.1
            port: 27018
            unixDomainSocket:
                enabled: false
        processManagement:
            fork: true
            pidFilePath: /root/mongo/mongod1.pid
        replication:
            replSetName: "rs0"
        ```

    -   Run the `vi /root/mongo/mongod2.conf` command to open the configuration file of Node 3. Modify the file based on the following content. Then, save and exit the configuration file.

        ```
        systemLog:
            destination: file
            path: /root/mongo/mongod2.log
            logAppend: true
        security:
            authorization: enabled
            keyFile: /root/mongo/keyFile/mongodb.key
        storage:
            dbPath: /root/mongo/data2
            directoryPerDB: true
        net:
            bindIp: 127.0.0.1
            port: 27019
            unixDomainSocket:
                enabled: false
        processManagement:
            fork: true
            pidFilePath: /root/mongo/mongod2.pid
        replication:
            replSetName: "rs0"
        ```

    **Note:** Parameter description:

    -   path in systemLog.path: the path to store the MongoDB log files in the current node.
    -   dbpath: the path to store the MongoDB data files in the current node.
    -   pidFilePath: the path to store the MongoDB process ID \(PID\) files in the current node.
    -   keyFile: the path to store the authentication file for the replica set. All nodes in the replica set must use the same authentication file.
    -   bindIp: the IP address of the current node. If all nodes in the replica set are deployed on the same server, they can use the same IP address.
    -   port: the port number of the current node. If all nodes in the replica set are deployed on the same server, they must use different port numbers.
    -   replication: the configuration of the replica set.
    -   replSetName: the name of the replica set.
7.  Run the following command to start the three nodes:

    ```
    mongod -f /root/mongo/mongod.conf && mongod -f /root/mongo/mongod1.conf && mongod -f /root/mongo/mongod2.conf
    ```

8.  After you start the three nodes, use the root account to log on to the MongoDB database.

    ```
    mongo -u root -p <The password of the root account> --authenticationDatabase admin
    ```

9.  In the mongo shell, add the nodes that you created in the preceding operations to the replica set and initialize the replica set.

    ```
    rs.initiate( {
       _id : "rs0",
       version : 1,
       members: [
          { _id: 0, host: "127.0.0.1:27017" , priority : 1},
          { _id: 1, host: "127.0.0.1:27018" , priority : 0},
          { _id: 2, host: "127.0.0.1:27019" , priority : 0}
       ]
    })
    ```

    ![Example of successful initialization](../images/p207069.png "Example of successful initialization")

    **Note:** The `rs.initiate()` command is used in this step. For more information about the command, visit [rs.initiate\(\)](https://docs.mongodb.com/manual/reference/method/rs.initiate/).

    After the command is executed, data is synchronized between the two added nodes and the primary node. The time consumed in this process varies based on the size of the backup file. After the data is synchronized, the MongoDB database is started in replica set mode.

10. Perform the following operations to check whether the MongoDB database in replica set mode is started.
    1.  Run the `exit` command to exit the mongo shell.
    2.  Run the following command to log on to the MongoDB database again:

        ```
        mongo -u <username> -p <password> --authenticationDatabase admin
        ```

        Parameter description:

        -   <username\>: the account used to log on to the MongoDB database. The default value is root.
        -   <password\>: the password used to log on to the MongoDB database.
    3.  Check whether the MongoDB database is started in replica set mode. If `<The name of the replica set>:PRIMARY>` is displayed on the left side of the command line in the mongo shell, the MongoDB database is started in replica set mode.

        ![Replica set mode](../images/p207079.png "Example of a successful start of the MongoDB database in replica set mode")


## FAQ

Q: Why does an error occur when I use the specified `mongod.conf` configuration file to start the MongoDB database?

-   You may have started the MongoDB database before you specified the `mongod.conf` configuration file. As a result, the `storage.bson` file is automatically generated in the data directory. In this case, remove the storage.bson file and specify the `mongod.conf` configuration file to start the MongoDB database.
-   Another mongod process may be running in the current system. In this case, run the `ps -e | grep mongod` command to query the PID of the process and run the `kill <PID>` command to stop the process. Then, specify the `mongod.conf` configuration file to start the MongoDB database.
-   The specified systemLog.path log path in the `mongod.conf` configuration file may be invalid. In this case, check whether the specified path exists and whether the log file has the specified name. Example: `path: /<The path of the log file>/<The name of the log file>.log`.

Q: Why does an error occur when I use the `mongod.conf` configuration file to start the MongoDB database in replica set mode?

-   You may fail to assign `600` permissions on the specified `keyFile` authentication file. On the command line, run the `sudo chmod 600 <The path of keyFile>` command to modify the permissions. Then, attempt to start the MongoDB database in replica set mode.

Q: Why does the system performance become low after I start the MongoDB database in replica set mode?

-   After you start MongoDB in replica set mode, the system automatically starts to synchronize data of the primary node to other nodes. This process can affect the system performance. The system performance returns to normal after the data is synchronized.

