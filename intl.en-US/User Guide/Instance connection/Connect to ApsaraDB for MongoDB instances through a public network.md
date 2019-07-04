# Connect to ApsaraDB for MongoDB instances through a public network {#concept_183456 .concept}

When you need to connect a local server to an ApsaraDB for MongoDB instance by using the IP address of a public network, you can use the methods described in this topic.

## Precautions {#section_zb0_uhw_7ay .section}

This topic is only applicable when you connect a local server to an ApsaraDB for MongoDB instance. If you need to connect to ApsaraDB for MongoDB instances through ECS, you can view the IP addresses of the public network and the internal network on the ECS instance details page.

If you connect to ApsaraDB for MongoDB instances through a public network, security risks may arise. We recommend that you connect to ApsaraDB for MongoDB instances through ECS instances.

## Method 1 Locate the public IP address of the local server in an IP address library and connect to the instance {#section_jyp_fmc_rks .section}

**Procedure**

1.  Access the [IP address library of Taobao](http://ip.taobao.com/ipSearch.html) to query your public IP address.
2.  Add the public IP address to the whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist](intl.en-US/User Guide/Data security/Configure a whitelist.md#).
3.  On the local server, log on to the ApsaraDB for MongoDB instance through the mongo shell. For more information, see [Log on to the MongoDB instance through the mongo shell](../../../../intl.en-US/Quick Start for Replica Set/Connect to an instance/Log on to the MongoDB instance through the mongo shell.md#).

    **Note:** You can also log on to ApsaraDB for MongoDB instances through other client tools.


In a case you have added the public IP address of the local server to the whitelist of the ApsaraDB for MongoDB instance but you still fail to connect to the instance. However, if you set the IP address in the whitelist to 0.0.0.0/0, you can connect to the instance. In this case, we recommend you locate the public IP address in connection information. For more information, see [Method 2 Locate the public IP address in connection information](#section_6vm_is9_ani).

## Method 2 Locate the public IP address in connection information {#section_6vm_is9_ani .section}

**Procedure**

1.  Add the IP address 0.0.0.0/0 to the whitelist of the ApsaraDB for MongoDB instance. For more information, see [Configure a whitelist](intl.en-US/User Guide/Data security/Configure a whitelist.md#).

    **Note:** If you add 0.0.0.0/0 to the whitelist, any server can access the ApsaraDB for MongoDB instance. This may pose security risks. Exercise caution when you add 0.0.0.0/0 to the whitelist. Remove 0.0.0.0/0 as soon as you no longer need it.

2.  On the local server, log on to the ApsaraDB for MongoDB instance through the mongo shell. For more information, see [Log on to the MongoDB instance through the mongo shell](../../../../intl.en-US/Quick Start for Replica Set/Connect to an instance/Log on to the MongoDB instance through the mongo shell.md#).

    **Note:** When you log on to an ApsaraDB for MongoDB instance through the mongo shell, log on by using the public connection address.

3.  Run the following command to query information about the client to which you log on through the mongo shell:

    ``` {#codeblock_zug_isw_oks}
    db.currentOp({"appName" : "MongoDB Shell","active" : true})
    ```

    Output examples

    ![Query the IP address of the client](images/44647_en-US.png)

    **Note:** If you log on to the ApsaraDB for MongoDB instance using other methods, you can run the following command to query information about all the clients:

    ``` {#codeblock_wyj_b93_qav}
    db.runCommand({currentOp: 1, "active" : true})
    ```

4.  Add the obtained IP addresses to the whitelist of the ApsaraDB for MongoDB instance, and remove the IP address 0.0.0.0/0 that you added in [Step 1](#li_cz7_zr1_e25) from the whitelist.

## More information {#section_d1k_0nu_2ez .section}

If your public IP address is not static and changes frequently, you can use either of the following methods to connect to an ApsaraDB for MongoDB instance:

-   Connect to ApsaraDB for MongoDB instances through ECS. For more information, see [Log on to the MongoDB instance through the mongo shell](../../../../intl.en-US/Quick Start for Replica Set/Connect to an instance/Log on to the MongoDB instance through the mongo shell.md#).
-   Connect to ApsaraDB for MongoDB instances through a VPN. For more information, see [Connect the local client to ApsaraDB for MongoDB instances through an SSL VPN tunnel](intl.en-US/User Guide/Instance connection/Connect the local client to ApsaraDB for MongoDB instances through an SSL VPN tunnel.md#).

