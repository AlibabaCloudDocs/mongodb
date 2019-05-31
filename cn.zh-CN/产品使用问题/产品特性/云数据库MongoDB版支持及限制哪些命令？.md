# 云数据库MongoDB版支持及限制哪些命令？ {#concept_39953_zh .concept}

MongoDB官方命令表： [http://docs.mongodb.org/master/reference/command/](http://docs.mongodb.org/master/reference/command/)

云数据库MongoDB版支持及限制命令如下表所示。

|名称|支持|不支持|
|:-|:-|:--|
|Aggregates Commands| -   aggregate
-   distinct
-   count
-   group
-   mapReduce

 |-|
|Geospatial Commands| -   geoNear
-   geoSearch

 |-|
|Query and Write Operation Commands| -   insert
-   update
-   delete
-   findAndModify
-   getLastError
-   getPrevError
-   resetError
-   parallelCollectionScan
-   eval

 |-|
|Query Plan Cache Commands| -   planCacheListFilters
-   planCacheSetFilter
-   planCacheClearFilters
-   planCacheListQueryShapes
-   planCacheListPlans
-   planCacheClear

 |-|
|Authentication| -   logout
-   authenticate
-   getnonce

 | -   authSchemaUpgrade
-   copydbgetnonce

 |
|User Management Commands| -   createUser
-   updateUser
-   dropUser
-   dropAllUsersFromDatabase
-   grantRolesToUser
-   revokeRolesFromUser
-   usersInfo

 |-|
|Role Management Commands| -   createRole
-   updateRole
-   dropRole
-   dropAllRolesFromDatabase
-   grantPrivilegesToRole
-   revokePrivilegesFromRole
-   grantRolesToRole
-   revokeRolesFromRole
-   rolesInfo
-   invalidateUserCache

 |-|
|Replication Commands Diagnostic| -   isMaster
-   applyOps

 |-|
|Diagnostic Commands| -   explain
-   listDatabases
-   dbHash
-   listCommands
-   availableQueryOptions
-   buildInfo
-   collStats
-   dbStats
-   cursorInfo
-   dataSize
-   ping
-   profile
-   top
-   whatsmyuri
-   serverStatus
-   features
-   isSelf
-   validate

 | -   driverOIDTest
-   connPoolStats
-   shardConnPoolStats
-   getCmdLineOpts
-   netstat
-   diagLogging
-   hostInfo

 |
|Instance Administration Commands| -   renameCollection
-   dropDatabase
-   listCollections
-   drop
-   create
-   cloneCollectionAsCapped
-   convertToCapped
-   filemd5
-   createIndexes
-   listIndexes
-   dropIndexes
-   fsync
-   connectionStatus
-   collMod
-   reIndex
-   touch
-   getParameter
-   compact

 | -   copydb
-   clone
-   clean
-   shutdown
-   logRotate
-   repairDatabase
-   repairCursor
-   setParameter
-   connPoolSync
-   setReadonly
-   cloneCollection

 |
|Replication Commands|-| -   replSetInitiate
-   replSetFreeze
-   replSetMaintenance
-   replSetGetConfig
-   replSetRequestVotes
-   replSetReconfig
-   replSetStepDown
-   replSetSyncFrom
-   replSetElect
-   replSetUpdatePosition
-   resync
-   appendOplogNote

 |
|Sharding Commands|-| -   addShard
-   removeShard
-   getShardVersion
-   setShardVersion
-   unsetSharding
-   checkShardingIndex

 |

