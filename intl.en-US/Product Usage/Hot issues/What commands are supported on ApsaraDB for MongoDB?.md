# What commands are supported on ApsaraDB for MongoDB?

For more information about MongoDB commands, visit [Database Commands](http://docs.mongodb.org/master/reference/command/).

The following table lists the commands supported on ApsaraDB for MongoDB.

|Command category|Supported|Not supported|
|:---------------|:--------|:------------|
|Aggregation command|-   aggregate
-   distinct
-   count
-   group
-   mapReduce

|N/A|
|Geospatial command|-   geoNear
-   geoSearch

|N/A|
|Query and write operation command|-   insert
-   update
-   delete
-   findAndModify
-   getLastError
-   getPrevError
-   resetError
-   parallelCollectionScan

|eval \(not supported on version 4.2 or later\)|
|Query plan cache command|-   planCacheListFilters
-   planCacheSetFilter
-   planCacheClearFilters
-   planCacheListQueryShapes
-   planCacheListPlans
-   planCacheClear

|N/A|
|Authentication command|-   logout
-   authenticate
-   getnonce

|-   authSchemaUpgrade
-   copydbgetnonce |
|User management command|-   createUser
-   updateUser
-   dropUser
-   dropAllUsersFromDatabase
-   grantRolesToUser
-   revokeRolesFromUser
-   usersInfo

|N/A|
|Role management command|-   createRole
-   updateRole
-   dropRole
-   dropAllRolesFromDatabase
-   grantPrivilegesToRole
-   revokePrivilegesFromRole
-   grantRolesToRole
-   revokeRolesFromRole
-   rolesInfo
-   invalidateUserCache

|N/A|
|Diagnostic command|-   explain
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

|-   driverOIDTest
-   connPoolStats
-   shardConnPoolStats
-   getCmdLineOpts
-   netstat
-   diagLogging
-   hostInfo |
|Instance management command|-   renameCollection
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

|-   copydb
-   clone
-   clean
-   shutdown
-   logRotate
-   repairDatabase
-   repairCursor
-   setParameter
-   connPoolSync
-   setReadonly
-   cloneCollection |
|Replication command|-   isMaster
-   applyOps

|-   replSetInitiate
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
-   appendOplogNote |
|Sharding command|N/A|-   addShard
-   removeShard
-   getShardVersion
-   setShardVersion
-   unsetSharding
-   checkShardingIndex |

