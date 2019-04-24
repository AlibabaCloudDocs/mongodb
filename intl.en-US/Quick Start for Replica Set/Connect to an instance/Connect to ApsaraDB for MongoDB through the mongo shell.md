# Connect to ApsaraDB for MongoDB through the mongo shell {#task_wdf_npz_jfb .task}

You can install the mongo shell on an ECS instance and use the mongo shell to connect to ApsaraDB for MongoDB.

To ensure successful authentication, use mongo shell 3.0 or a later version to connect to ApsaraDB for MongoDB.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/#/mongodb/detail/dds-bp141308a7947204/info).
2.  Click the target instance ID or choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6671/155609894213267_en-US.png)** \> **Manage** in the Operation column to go to the Basic Information page of the target instance.
3.  In the left-side navigation pane, click **Database Connection**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6675/155609894231535_en-US.png)

    -   Red boxes highlight the connection information.
    -   In each connection address, the default port number is 3717 and the domain name is separated from the port number with a colon \(:\).
4.  In the ECS instance, run a mongo command to connect to ApsaraDB for MongoDB. The following command is an example: 

    ```
    mongo --host dds-xxxx.mongodb.rds.aliyuncs.com:3717 -u root -p Ft123456 --authenticationDatabase admin
    ```


**Mongo shell FAQs**

-   [Connection](https://www.alibabacloud.com/help/doc-detail/61100.htm)
-   [Connections](https://www.alibabacloud.com/help/doc-detail/61114.htm)
-   [High load](https://www.alibabacloud.com/help/doc-detail/61149.htm)

