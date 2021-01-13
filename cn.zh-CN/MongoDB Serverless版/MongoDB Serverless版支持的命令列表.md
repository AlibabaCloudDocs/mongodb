# MongoDB Serverless版支持的命令列表

MongoDB Serverless版实例对部分MongoDB官方命令提供了支持，本文列举MongoDB Serverless版实例支持的所有命令。

|命令类型|命令列表|备注|
|----|----|--|
|查询和写入操作命令**说明：** 不支持读写`admin`和`config`数据库

|`insert`|无|
|`update`|无|
|`findAndModify`|无|
|`find`|`find`命令不支持`$where`操作符。|
|`getMore`|无|
|`resetError`|无|
|`getLastError`|无|
|`delete`|无|
|聚合命令|`aggregate`|-   聚合命令不支持`$merge`、`$where`操作符。
-   聚合命令的`$changestream`阶段不支持订阅整个实例级别的增量。 |
|`count`|
|`distinct`|
|鉴权命令|`authenticate`|无|
|`getnonce`|无|
|`logout`|无|
|用户管理命令|`userinfo`|仅支持查看当前用户信息。|
|角色管理命令|`rolesInfo`|仅支持查看当前用户拥有的角色。|
|副本集命令|`isMaster`|无|
|分片集群命令|`isdbgrid`|无|
|会话命令|`abortTransaction`|无|
|`commitTransaction`|无|
|`endSessions`|无|
|`killSessions`|无|
|`refreshSessions`|无|
|`startSession`|无|
|实例管理命令**说明：** 无法查看`admin`和`config`库中的集合和索引。

|`create`|无|
|`createIndexes`|无|
|`drop`|无|
|`dropDatabase`|无|
|`dropIndexes`|无|
|`killCursors`|无|
|`listCollections`|无|
|`listDatabases`|无|
|`listIndexes`|无|
|`renameCollection`|无|
|诊断命令|`collStats`|无|
|`connectionStatus`|无|
|`dataSize`|无|
|`dbStats`|无|
|`explain`|无|
|`ping`|无|

