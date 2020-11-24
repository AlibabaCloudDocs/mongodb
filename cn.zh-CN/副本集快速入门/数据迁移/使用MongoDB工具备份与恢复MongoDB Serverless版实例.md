# 使用MongoDB工具备份与恢复MongoDB Serverless版实例

您可以使用MongoDB数据库自带的备份还原工具mongodump和mongorestore，备份和恢复MongoDB Serverless版实例。

由于当前Serverless控制台暂不支持备份与恢复功能，您可以通过MongoDB官方工具来达到备份恢复的目的。

## 注意事项

-   确保安装的mongodump和mongorestore软件版本为4.2。安装步骤详情请参见官方文档[Install MongoDB](https://docs.mongodb.com/v3.4/installation/)。
-   通过MongoDB工具备份Serverless实例的数据库为全量逻辑备份。为保障数据一致性，备份操作开始前请停止源库的相关业务，并停止数据写入。
-   执行mongodump备份命令将覆盖dump文件夹中的历史备份文件。如果您之前使用mongodump命令对源库执行过备份操作，请将dump文件夹中的备份文件移动至其他目录并确保dump文件夹为空。
-   必须在安装有MongoDB数据库的服务器上执行mongodump和mongorestore命令，而不是在mongo shell环境下执行。
-   您必须拥有目标数据库的读写权限。
-   您必须先申请公网连接地址。详情请参见[申请公网连接地址]()。

## 使用mongodump备份Serverless实例数据库

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。

2.  在页面左上角，选择实例所在的资源组和地域。

3.  在左侧导航栏，单击**Serverless实例列表**。

4.  在左侧导航栏中，单击**数据库连接**。

5.  找到并复制公网连接地址。

6.  在安装有mongodump和mongorestore的本地服务器中，执行如下命令进行数据备份。

    ```
    mongodump --host <mongodb_host>:3717 -u <username> --authenticationDatabase admin
    ```

    **说明：**

    -   <host\>：Serverless实例的公网连接地址。
    -   <username\>：连接Serverless实例数据库的账号名。您可以在MongoDB控制台**基本信息**页面中的**连接信息**区域找到**账号名**。
    示例：

    ```
    mongodump --host dds-t4n**********-pub.mongodb.singapore.rds.aliyuncs.com:3717 -u user12345 --authenticationDatabase admin
    ```

    **说明：** 如果提示无法连接，请先将本地服务器的IP地址添加到Serverless实例的白名单中。详情请参见[设置白名单]()。

7.  命令行提示`Enter password:`时，输入数据库账号对应的密码，数据库开始备份。如果您丢失了该密码，请[重置密码]()。

    **说明：** 等待备份完成，数据将备份至当前目录下的dump文件夹中。


## 使用mongorestore恢复Serverless实例数据库

1.  登录[MongoDB管理控制台](https://mongodb.console.aliyun.com/)。

2.  在页面左上角，选择实例所在的资源组和地域。

3.  在左侧导航栏，单击**Serverless实例列表**。

4.  在左侧导航栏中，单击**数据库连接**。

5.  找到并复制公网连接地址。

6.  在安装有mongodump和mongorestore的本地服务器中，执行如下命令将备份数据导入至Serverless实例数据库。

    ```
    mongorestore --host <mongodb_host>:3717 -u <username> -d <database>  <dir> --authenticationDatabase admin
    ```

    **说明：**

    -   <mongodb\_host\>：Serverless实例的公网连接地址。
    -   <username\>：连接Serverless实例数据库的账号名。您可以在MongoDB控制台**基本信息**页面中的**连接信息**区域找到**账号名**。
    -   <database\>：需要导入的数据库。备份文件中如有多个数据库，需要重复本步骤进行其它数据库的导入。
    -   <dir\>：数据库备份文件所在的目录。
    示例：

    -   导入数据库备份文件中的mongodbtest数据库：

        ```
        mongodump --host dds-t4n**********-pub.mongodb.singapore.rds.aliyuncs.com:3717 -u user12345 --authenticationDatabase admin -d mongodbtest /dump/mongodbtest 
        ```

    -   导入数据库备份文件中的test123数据库：

        ```
        mongodump --host dds-t4n**********-pub.mongodb.singapore.rds.aliyuncs.com:3717 -u user12345 --authenticationDatabase admin -d test123 /dump/test123 
        ```

    **说明：** 如果提示无法连接，请先将本地服务器的IP地址添加到Serverless实例的白名单中。详情请参见[设置白名单]()。

7.  命令行提示`Enter password:`时，输入数据库账号对应的密码，数据库开始导入。如果您丢失了该密码，请[重置密码]()。

    **说明：** 等待恢复完成，数据将导入至Serverless实例数据库中。


