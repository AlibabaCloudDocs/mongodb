# 云数据库MongoDB版是否支持嵌套 {#concept_39934_zh .concept}

云数据库MongoDB版支持嵌套，示例如下：

``` {#codeblock_tyv_vnb_ztq}
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

在上述示例中的`fields:{"Status":{"dest":"0","orgi":"1420041600"}}`处定义了嵌套文档。

