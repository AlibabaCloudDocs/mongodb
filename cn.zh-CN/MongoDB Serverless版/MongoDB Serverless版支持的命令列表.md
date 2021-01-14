# MongoDB Serverless版支持的命令列表

MongoDB Serverless版实例对部分MongoDB官方命令提供了支持，本文列举MongoDB Serverless版实例支持的所有命令。

|命令类型|命令列表|备注|
|----|----|--|
|查询和写入操作命令|-   `insert`
-   `update`
-   `find`
-   `findAndModify`
-   `delete`
-   `getMore`
-   `getLastError`
-   `resetError`

|-   `find`命令不支持`$where`操作符。
-   不支持读写`admin`和`config`数据库。 |
|查询和写入操作命令|-   `aggregate`
-   `count`
-   `distinct`

|-   聚合命令不支持`$merge`、`$where`操作符。
-   聚合命令的`$changestream`阶段不支持订阅整个实例级别的增量。 |
|鉴权命令|-   `authenticate`
-   `getnonce`
-   `logout`

|无|
|用户管理命令|`userinfo`|仅支持查看当前用户信息。|
|角色管理命令|`rolesInfo`|仅支持查看当前用户拥有的角色信息。|
|副本集命令|`isMaster`|无|
|分片集群命令|`isdbgrid`|无|
|会话命令|-   `abortTransaction`
-   `commitTransaction`
-   `endSessios`
-   `killSessions`
-   `refreshSessions`
-   `startSession`

|无|
|实例管理命令|-   `create`
-   `createIndexes`
-   `drop`
-   `dropDatabase`
-   `dropIndexes`
-   `killCursors`
-   `listCollections`
-   `listDatabases`
-   `listIndexes`
-   `renameCollection`

|无法查看`admin`和`config`库中的集合和索引。|
|诊断命令|-   `collStats`
-   `connectionStatus`
-   `dataSize`
-   `dbStats`
-   `explain`
-   `ping`

|无|

