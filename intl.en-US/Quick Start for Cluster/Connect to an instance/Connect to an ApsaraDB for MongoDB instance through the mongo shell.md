# Connect to an ApsaraDB for MongoDB instance through the mongo shell {#concept_mnd_xg2_qgb .concept}

You can install the Mongo shell in an [ECS](https://www.alibabacloud.com/help/zh/doc-detail/25367.htm) instance and use the mongo shell to connect to an ApsaraDB for MongoDB instance.

## Prerequisites {#section_u3n_sh2_qgb .section}

-   For successful authentication, you must use mongo shell 3.0 or later to connect to an ApsaraDB for MongoDB instance. For more information about the installation procedure, see [Install MongoDB](https://docs.mongodb.com/v3.4/installation/).
-   Add the server IP addresses that need access to the instance to the whitelist in advance. For more information, see [Configure a whitelist](intl.en-US/Quick Start for Cluster/Configure a whitelist.md#).
-   To log on to ApsaraDB for MongoDB over the Internet, you must apply for a public IP address. For more information, see [Apply for a public IP address](intl.en-US/Quick Start for Cluster/Apply for a public IP address.md#).

## Procedure {#section_xx5_wh2_qgb .section}

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/detail/dds-bp141308a7947204/info).
2.  In the upper-left corner of the homepage, select the region of the instance.
3.  In the left-side navigation pane, click **Sharding instances**.
4.  Locate the target instance, and then click the instance ID.
5.  On the Basic Information page that appears, click **Database Connection** in the left-side navigation pane to obtain the address of the mongos.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6695/155926683213838_en-US.png)

    Three mongos are displayed in this example. You can use one of their addresses to log on to the mongos.

6.  Connect to a mongos from a local server or an ECS instance with mongo shell installed.

    ```
    mongo --host <mongos_host> -u <username> -p --authenticationDatabase <database>
    ```

    **Note:** 

    -   <mongos\_host\>: the address of any mongos in the ApsaraDB for MongoDB instance.
    -   <username\>: the account for the instance. The default username is root.
    -   <database\>: the name of the authentication database for the local MongoDB database. The default database name is admin.
    Example:

    ```
    mongo --host s-bp**********.mongodb.rds.aliyuncs.com:3717 -u root -p --authenticationDatabase admin
    ```

7.  When `Enter password:` is displayed, enter the password. If you forget the password of the root account, you can reset the password by using the method specified in [Set a password](intl.en-US/Quick Start for Cluster/Set a password.md#).

    **Note:** The characters entered into the password field are not displayed.


## More information {#section_zsr_lf2_qgb .section}

We recommend that you do not log on to an ApsaraDB for MongoDB instance as the root user in the production environment. You can create users and grant permissions based on your business needs. For more information, see [db.createUser\(\)](https://docs.mongodb.com/manual/reference/method/db.createUser/).

