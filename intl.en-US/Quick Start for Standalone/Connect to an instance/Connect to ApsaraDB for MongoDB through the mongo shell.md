# Connect to ApsaraDB for MongoDB through the mongo shell {#task_iw5_tg4_hfb .task}

You can use the mongo shell to connect to an ApsaraDB for MongoDB instance.

Use mongo shell 3.0 or a later version to connect to ApsaraDB for MongoDB, otherwise authentication fails.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  Click the target instance ID to go to its Basic Information page.
3.  In the left-side navigation pane, click **Database Connection** to view the connection information under **Intranet Connection - VPC** and **Public IP Connection** and select a connection type as required, as shown in the following figure. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6664/155592656413741_en-US.png) 

    In each connection address, the domain name is separated from the port number with a colon \(:\). The default port number is 3717, and the default database name is admin.

4.  On an [ECS](https://www.alibabacloud.com/help/zh/doc-detail/25367.htm) instance, run a mongo command to connect to ApsaraDB for MongoDB. The following command is an example: 

    ```
    mongo --host dds-xxxx.mongodb.rds.aliyuncs.com:3717 -u root -p 123456 --authenticationDatabase admin
    ```

    Mongo shell FAQs

    -   [Connection](https://www.alibabacloud.com/help/doc-detail/61100.htm)
    -   [Connections](https://www.alibabacloud.com/help/doc-detail/61114.htm)
    -   [High load](https://www.alibabacloud.com/help/doc-detail/61149.htm)

