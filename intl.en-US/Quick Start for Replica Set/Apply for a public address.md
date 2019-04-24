# Apply for a public address {#task_z3n_1xz_jfb .task}

ApsaraDB for MongoDB allows you to apply for a public address to connect to an instance through the Internet.

There are certain security risks for connecting to an instance through the Internet. To guarantee data security, you need to release a public address in a timely manner after using it.

1.  Log on to the [ApsaraDB for MongoDB console](https://mongodb.console.aliyun.com/).
2.  In the upper-left corner of the home page, select the region where the target instance is located.
3.  Click the target instance ID or choose **![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6671/155609796213267_en-US.png)** \> **Manage**in the Operation column corresponding to the target instance.
4.  On the Basic Information page that appears, click **Database Connection** in the left-side navigation pane.
5.  On the page that appears, click **Apply for Public IP** to the right of Public IP Connection.
6.  In the Apply for Public IP dialog box that appears, click **OK**. 

    **Note:** After the application procedure, you can use the obtained public address to access the target instance. Before that, you need to add the public IP address of the terminal that you use to connect to the instance to the whitelist. For more information, see [Configure a whitelist](intl.en-US/Quick Start for Replica Set/Configure a whitelist.md#).


After the application procedure, the target ApsaraDB for MongoDB replica set instance provides separate addresses for you to connect to the primary and secondary nodes. For more information, see [Obtain the replica set instance connection information](intl.en-US/Quick Start for Replica Set/Connect to an instance/Obtain the replica set instance connection information.md#).

