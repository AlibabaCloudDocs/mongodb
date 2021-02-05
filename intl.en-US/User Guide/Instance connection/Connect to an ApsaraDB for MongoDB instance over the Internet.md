# Connect to an ApsaraDB for MongoDB instance over the Internet

This topic describes how to connect a local client to an ApsaraDB for MongoDB instance over the Internet.

## Prerequisites

A public endpoint for the ApsaraDB for MongoDB instance is obtained. For more information, see the following topics:

-   [Apply for a public endpoint for a standalone ApsaraDB for MongoDB instance]()
-   [Apply for a public endpoint for an ApsaraDB for MongoDB instance](/intl.en-US/Quick Start/Apply for a public endpoint for an ApsaraDB for MongoDB instance.md)
-   [Apply for a public endpoint for a sharded cluster instance]()

## Precautions

Read this topic only when you want to connect a local client to an ApsaraDB for MongoDB instance. If you want to connect to an ApsaraDB for MongoDB instance by using an ECS instance, you can obtain both the public and private IP addresses from the ECS instance details page in the ECS console.

If you connect to an ApsaraDB for MongoDB instance over the Internet, security risks may arise. We recommend that you connect to an ApsaraDB for MongoDB instance by using an ECS instance.

## Method 1: Query an IP address library for the public IP address of your local client and connect to an ApsaraDB for MongoDB instance

You can query an IP address library for the public IP address of your local client and connect to an ApsaraDB for MongoDB instance.

1.  Query the public IP address of your local client.
2.  Add the public IP address to a whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).
3.  Log on to the ApsaraDB for MongoDB instance by using the mongo shell from your local client. For more information, see [Connect to an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance connection/Connect to an ApsaraDB for MongoDB instance.md).

    **Note:** You can also log on to the ApsaraDB for MongoDB instance by using other client tools.


You may have added the public IP address of your local client to the whitelist but still fail to connect to the ApsaraDB for MongoDB instance. However, after you add 0.0.0.0/0 to the whitelist, you can connect to the instance. In this case, we recommend that you query the connection information for the public IP address. For more information, see [Method 2: Query the connection information for the public IP address of your local client and connect to an ApsaraDB for MongoDB instance](#section_6vm_is9_ani).

## Method 2: Query the connection information for the public IP address of your local client and connect to an ApsaraDB for MongoDB instance

You can query the connection information for the public IP address of your local client and connect to an ApsaraDB for MongoDB instance.

1.  Add the 0.0.0.0/0 entry to a whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure a whitelist or an ECS security group for an ApsaraDB for MongoDB instance.md).

    **Note:** If you add the 0.0.0.0/0 entry to the whitelist, all servers are granted access to the ApsaraDB for MongoDB instance. This may raise security risks. Exercise caution when you add the 0.0.0.0/0 entry to a whitelist. Remove the 0.0.0.0/0 entry if you no longer need it.

2.  Log on to the ApsaraDB for MongoDB instance by using the mongo shell from your local client. For more information, see [Connect to an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Instance connection/Connect to an ApsaraDB for MongoDB instance.md).
3.  Run the following command to query information about the client where you log on:

    ```
    db.currentOp({"appName" : "MongoDB Shell","active" : true})
    ```

    The following figure shows an example.

    ![Query the client IP address](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1335298951/p44647.png)

    **Note:** If you log on to the ApsaraDB for MongoDB instance using other methods, you can run the following command to query information about all clients:

    ```
    db.runCommand({currentOp: 1, "active" : true})
    ```

4.  Add the IP address obtained in the preceding step to the whitelist of the ApsaraDB for MongoDB instance, and remove the 0.0.0.0/0 entry that you added in [Step 1](#li_cz7_zr1_e25) from the whitelist.

## References

If the public IP address of your local client dynamically changes, you can use one of the following methods to connect to an ApsaraDB for MongoDB instance:

-   Connect to the instance by using an ECS instance.
-   Connect to the instance by using a VPN. For more information, see [Connect a local client to an ApsaraDB for MongoDB instance through an SSL VPN tunnel](/intl.en-US/User Guide/Instance connection/Connect a local client to an ApsaraDB for MongoDB instance through an SSL VPN tunnel.md).

