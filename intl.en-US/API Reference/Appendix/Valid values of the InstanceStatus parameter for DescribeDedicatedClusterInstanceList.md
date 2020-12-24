# Valid values of the InstanceStatus parameter for DescribeDedicatedClusterInstanceList

This topic lists the valid values of the InstanceStatus parameter for the DescribeDedicatedClusterInstanceList operation and the instance statuses that the values correspond to.

|Value|Corresponding status|Description|
|-----|--------------------|-----------|
|0|CREATING|The instance is being created.|
|1|ACTIVATION|The instance is in use.|
|2|AUDITING|The instance is being audited.|
|3|DELETING|The instance is being deleted.|
|4|BACKING|The instance has failed an audit.|
|5|RESTARTING|The instance is restarting.|
|6|CLASS\_CHANGING|The instance type is being changed.|
|6|INS\_MAINTAINING|The instance is under maintenance.|
|6|TRANSING|The instance is being migrated.|
|6|TRANSING\_ACCROSS|The instance is being migrated to another zone.|
|6|CLASS\_CHANGING|The High-availability Edition instance is being changed to an Enterprise Edition instance.|
|6|CLASS\_CHANGING|The Enterprise Edition instance is being changed to a High-availability Edition instance.|
|6|VERSION\_TRANSING|The version is being changed.|
|6|DATABASE\_TRANSING|The database is being migrated.|
|6|GUARD\_CREATING|A disaster recovery instance is being created.|
|6|MINOR\_VERSION\_TRANSING|The instance is being changed to another minor version.|
|6|RECOVER\_CUSTINS|The instance is being recovered.|
|6|UPGRADE\_TO\_HAS\_ING|The instance is being upgraded to an HAS version.|
|6|ACCOUNT\_MODE\_UPGRADING|The account is being upgraded.|
|6|READINS\_TRANSING|The read-only instance is being migrated.|
|6|SCALING\_OUT|The instance is going through a scale-out.|
|6|SCALING\_IN|The instance is going through a scale-in.|
|6|READINS\_MAINTAINING|The read-only instance is under maintenance.|
|6|SLAVE\_INS\_TRANSING|A secondary node of the instance is being migrated.|
|6|NODE\_CREATING|A node is being created in the instance.|
|6|NODE\_DELETING|A node of the instance is being deleted.|
|6|MINOR\_VERSION\_UPGRADING|The instance is being upgraded to a later minor version.|
|6|UPGRADE\_SERVICE\_UPGRADING|Service of the instance is being upgraded.|
|6|MINOR\_VERSION\_HOT\_UPGRADING|The instance is going through a hot upgrade.|
|6|DATA\_FLUSHING|Data of the instance is being deleted.|
|6|REPLICA\_ADDING|The replica set instance is going through a scale-out.|
|6|REPLICA\_DELETING|The replica set instance is going through a scale-in.|
|6|GROUP\_ADDING|The instance is going through a scale-out.|
|6|STORAGE\_EXPANDING|The storage of the instance is expanding.|
|7|BACKUP\_RECOVERING|The instance is being restored from a backup.|
|7|INS\_CLONING|The instance is being cloned.|
|7|INS\_COPYING|The instance is being copied.|
|7|SUBINS\_CREATING|A temporary instance is being created.|
|7|DATA\_IMPORTING|Data is being imported into the instance.|
|7|DATABASE\_ONLINE|The database is being published.|
|7|DATABASE\_IMPORTING|The database is being imported.|
|7|DATABASE\_CLEARING|The database is being cleared.|
|8|NET\_SWITCHING|The network type is being changed.|
|8|NET\_CREATING|Network connection is being created.|
|8|NET\_DELETING|Network connection is being released.|
|8|NET\_MODIFYING|Network connection is being modified.|
|8|INS\_MAINTAINING|The network of the instance is under maintenance.|
|8|PROXY\_GROUP\_CHANGE|The proxy group is being changed.|
|8|LINK\_SWITCHING|The link is being changed.|
|8|GUARD\_SWITCHING|The instance is going through a switchover for disaster recovery.|
|8|HA\_SWITCHING|The instance is going through a switchover for high availability.|
|8|ROLE\_SWITCHING|The role of the instance is being changed.|
|8|CONFIG\_SWITCHING|The instance configuration is being changed.|
|8|CONFIG\_ENCRYPTING|The instance configuration is being encrypted.|
|8|SSL\_MODIFYING|The SSL configuration of the instance is being changed.|
|8|TDE\_MODIFYING|The Transparent Data Encryption \(TDE\) configuration of the instance is being changed.|
|5|HBASE\_EXPANDING|The storage of the HBase database is expanding.|
|5|HBASE\_SCALE\_OUT|The HBase node is going through a scale-out.|
|8|HBASE\_PUB\_CONN\_SWITCHING|The status of the HBase database that is connected over the Internet is being updated.|
|8|HBASE\_CLASSIC\_CONN\_SWITCHING|The status of the HBase database that is deployed in the classic network is being updated.|
|5|ANALYSIS\_EXPANDING|The storage of the instance is expanding.|
|5|HBASE\_COLD\_EXPANDING|The cold storage of the HBase database is expanding.|
|8|RWVIP\_MODIFYING|The virtual IP address for read/write splitting is being modified.|
|9|CLEAR\_EXPIRED\_DATA|The expired data is being deleted.|
|10|COMP\_ADDING|A component is being installed.|
|10|COMP\_REMOVING|A component is being uninstalled.|
|10|MODUlE\_INSTALLING|A module is being installed.|
|10|MODUlE\_UPGRADING|A module is being upgraded.|
|10|MODUlE\_UNINSTALLING|A module is being uninstalled.|
|8|HBASE\_HAS\_ROLLING\_BACK|The HAS security hardening feature is being rolled back.|
|6|MINOR\_VERSION\_WARM\_UPGRADING|The instance is going through a warm upgrade.|
|15|STOPED|The instance is being stopped.|
|6|STARTING|The instance is starting.|
|11|DESTORYED|The instance has been destroyed.|

