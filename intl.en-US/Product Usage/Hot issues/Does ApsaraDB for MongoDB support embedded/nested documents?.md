# Does ApsaraDB for MongoDB support embedded/nested documents?

Yes, ApsaraDB for MongoDB supports embedded/nested documents. In the following example, the fields key specifies an embedded/nested document.

```
{
        "_id" : ObjectId("5cf0e51d8d1acb8a892ca65e"),
        "id" : "16399864",
        "timestamp" : "1453185620",
        "tablename" : "houseinfo",
        "dbname" : "corp_officebuilding",
        "primaryKeys" : "Id",
        "class" : "class com.uban.dts.bean.DtsLog",
        "dbType" : "MYSQL",
        "fieldCount" : "138",
        "opt" : "UPDATE",
        "fields" : {
                "Status" : {
                        "dest" : "0",
                        "orgi" : "1420041600"
                }
        }
}
```

