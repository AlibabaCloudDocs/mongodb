# DynamoDB协议兼容版实例支持详情

云数据库MongoDB版对DynamoDB协议提供了支持。本文详细介绍MongoDB对DynamoDB协议的兼容情况。

## 背景信息

Amazon DynamoDB是一种完全托管的NoSQL数据库服务，提供快速而可预测的性能，能够实现无缝扩展。阿里云数据库MongoDB版现在兼容了DynamoDB协议，您可以在创建MongoDB实例时选择支持DynamoDB协议即可使用DynamoDB协议。如何创建DynamoDB协议兼容版实例，请参见[创建DynamoDB协议兼容版实例](/cn.zh-CN/DynamoDB协议兼容版/创建DynamoDB协议兼容版实例.md)。

## 注意事项

-   仅云数据库MongoDB版4.0版本分片集群实例支持DynamoDB协议。
-   存量实例可通过开启兼容DynamoDB协议来获取支持。
-   目前DynamoDB兼容功能仅支持在VPC环境下使用，使用无需鉴权。

## DynamoDB协议支持情况

|接口名|参数|是否支持|备注|
|---|--|----|--|
|CreateTable|请求参数|必选参数：AttributeDefinitions|是|无|
|必选参数：KeySchema|是|无|
|必选参数：TableName|是|-   不能包含以下特殊字符：美元符号 （$）。
-   不能以`system.`前缀开头。
-   长度限制：1~100字节。 |
|可选参数：BillingMode|否|无|
|可选参数：GlobalSecondaryIndexes|是|无|
|可选参数：LocalSecondaryIndexes|是|无|
|可选参数：ProvisionedThroughput|否|无|
|可选参数：SSESpecification|否|无|
|可选参数：StreamSpecification|是|`StreamViewType`参数当前仅支持如下值：-   KEYS\_ONLY
-   NEW\_IMAGE

**说明：** NEW\_IMAGE当前仅可包含分区键（Partition key），如果表中存在排序键（Sort key），该排序键将会被忽略。 |
|可选参数：Tags|否|无|
|返回参数|TableDescription|是|无|
|UpdateTable|请求参数|可选参数：AttributeDefinitions|是|无|
|可选参数：BillingMode|否|无|
|必选参数：GlobalSecondaryIndexesUpdates|是|支持Create和Delete，不支持Update。|
|可选参数：ProvisionedThroughput|否|无|
|可选参数：ReplicaUpdates|否|无|
|可选参数：SSESpecification|否|无|
|可选参数：StreamSpecification|是|`StreamViewType`参数当前仅支持如下值：-   KEYS\_ONLY
-   NEW\_IMAGE

**说明：** NEW\_IMAGE当前仅可包含分区键（Partition key），如果表中存在排序键（Sort key），该排序键将会被忽略。 |
|必选参数：TableName|是|无|
|返回参数|TableDescription|是|参见TableDescription。|
|DescribeTable|请求参数|必选参数：TableName|是|无|
|返回参数|Table|是|参见TableDescription。|
|ListTables|请求参数|可选参数：ExclusiveStartTableName|否|不支持分页查询，没有返回记录条数的限制。|
|可选参数：Limit|否|不支持分页查询，没有返回记录条数的限制。|
|返回参数|LastEvaluatedTableName|否|无|
|TableNames|是|无|
|DeleteTable|请求参数|必选参数：TableName|是|无|
|返回参数|TableDescription|是|参见TableDescription。|
|PutItem|请求参数|必选参数：Item|是|无|
|必选参数：TableName|是|无|
|可选参数：ConditionalOperator|否|无|
|可选参数：ConditionExpression|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：Expected|否|无|
|可选参数：ExpressionAttributeNames|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：ExpressionAttributeValues|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：ReturnConsumedCapacity|否|无|
|可选参数：ReturnItemCollectionMetrics|否|无|
|可选参数：ReturnValues|是|无|
|返回参数|Attributes|是|无|
|ConsumedCapacity|否|无|
|ItemCollectionMetrics|否|无|
|UpdateItem|请求参数|必选参数：Key|是|无|
|必选参数：TableName|是|无|
|可选参数：AttributeUpdates|否|无|
|可选参数：ConditionalOperator|否|无|
|可选参数：ConditionExpression|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：Expected|否|无|
|可选参数：ExpressionAttributeNames|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：ExpressionAttributeValues|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：ReturnConsumedCapacity|否|无|
|可选参数：ReturnItemCollectionMetrics|否|无|
|可选参数：ReturnValues|是|无|
|可选参数：UpdateExpression|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|返回参数|Attributes|是|无|
|ConsumedCapacity|否|无|
|ItemCollectionMetrics|否|无|
|GetItem|请求参数|必选参数：Key|是|无|
|必选参数：TableName|是|无|
|可选参数：AttributesToGet|否|无|
|可选参数：ConsistentRead|否|无|
|可选参数：ExpressionAttributeNames|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：ProjectionExpression|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：ReturnConsumedCapacity|否|无|
|返回参数|ConsumedCapacity|否|无|
|Item|是|无|
|DeleteItem|请求参数|必选参数：Key|是|无|
|必选参数：TableName|是|无|
|可选参数：ConditionalOperator|否|无|
|可选参数：ConditionExpression|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：Expected|否|无|
|可选参数：ExpressionAttributeNames|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：ExpressionAttributeValues|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：ReturnConsumedCapacity|否|无|
|可选参数：ReturnItemCollectionMetrics|否|无|
|可选参数：ReturnValues|是|无|
|返回参数|Attributes|是|无|
|ConsumedCapacity|否|无|
|ItemCollectionMetrics|否|无|
|BatchWriteItem|请求参数|必选参数：RequestItems|是|无|
|可选参数：ReturnConsumedCapacity|否|无|
|可选参数：ReturnItemCollectionMetrics|否|无|
|返回参数|ConsumedCapacity|否|无|
|ItemCollectionMetrics|否|无|
|UnprocessedItems|是|无|
|BatchGetItem|请求参数|必选参数：RequestItems|是|Item元素不支持`AttributesToGet`和`ConsistentRead`参数。|
|可选参数：ReturnConsumedCapacity|否|无|
|返回参数|ConsumedCapacity|否|无|
|Responses|是|无|
|UnprocessedKeys|是|无|
|Query|请求参数|必选参数：TableName|是|无|
|可选参数：AttributesToGet|否|无|
|可选参数：ConditionalOperator|否|无|
|可选参数：ConsistentRead|否|无|
|可选参数：ExclusiveStartKey|是|无|
|可选参数：ExpressionAttributeNames|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：ExpressionAttributeValues|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：FilterExpression|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：IndexName|是|无|
|可选参数：KeyConditionExpression|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：KeyConditions|否|无|
|可选参数：Limit|是|无|
|可选参数：ProjectionExpression|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：QueryFilter|否|无|
|可选参数：ReturnConsumedCapacity|否|无|
|可选参数：ScanIndexForward|是|无|
|可选参数：Select|否|无|
|返回参数|ConsumedCapacity|否|无|
|Count|是|无|
|Items|是|无|
|LastEvaluatedKey|是|无|
|ScannedCount|是|无|
|Scan|请求参数|必选参数：TableName|是|无|
|可选参数：AttributesToGet|否|无|
|可选参数：ConditionalOperator|否|无|
|可选参数：ConsistentRead|否|无|
|可选参数：ExclusiveStartKey|是|无|
|可选参数：ExpressionAttributeNames|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：ExpressionAttributeValues|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：FilterExpression|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：IndexName|是|无|
|可选参数：Limit|是|无|
|可选参数：ProjectionExpression|是|参见[表达式支持情况](#section_wlf_yls_m1d)。|
|可选参数：ReturnConsumedCapacity|否|无|
|可选参数：ScanFilter|否|无|
|可选参数：Segment|是|无|
|可选参数：Select|否|无|
|可选参数：TotalSegments|是|无|
|返回参数|ConsumedCapacity|否|无|
|Count|是|无|
|Items|是|无|
|LastEvaluatedKey|是|无|
|ScannedCount|是|无|

|接口名|参数|是否支持|备注|
|---|--|----|--|
|DescribeStream|请求参数|必选参数：StreamArn|是|无|
|可选参数：Limit|否|无|
|可选参数：ExclusiveStartShardId|否|无|
|返回参数|必选参数：StreamDescription|是|对比AWS DynamoDB实例，该返回参数返回结果有如下区别：-   `StartingSequenceNumber`字段固定为`unknown`。
-   `EndingSequenceNumber`字段以时间戳体现。
-   由于DynamoDB协议兼容版实例仅有一个Shard，`ShardId`字段固定为`arn:alibaba:mongo-dynamodb@shard-only-1`。 |
|ListStreams|请求参数|可选参数：TableName|是|无|
|可选参数：Limit|否|无|
|可选参数：ExclusiveStartStreamArn|否|无|
|返回参数|必选参数：Streams|是|每个表中最多只能返回一个Stream。|
|GetShardIterator|请求参数|必选参数：StreamArn|是|无|
|必选参数：ShardId|是|由于DynamoDB协议兼容版实例仅有一个Shard，本字段固定为`arn:alibaba:mongo-dynamodb@shard-only-1`。|
|必选参数：ShardIteratorType|是|当前仅支持传入`LATEST`和`AFTER_SEQUENCE_NUMBER`。|
|可选参数：SequenceNumber|是|当`ShardIteratorType`为`AFTER_SEQUENCE_NUMBER`时使用，可传入32位秒级时间戳。|
|返回参数|必选参数：ShardIterator|是|无|
|GetRecords|请求参数|必选参数：ShardIterator|是|无|
|可选参数：Limit|是|不指定时默认按照每101条记录进行分页，而非1MB数据大小。|
|返回参数|必选参数：Records|是|无|

|数据类型|字段|是否支持|
|----|--|----|
|TableDescription|ArchivalSummary|否|
|AttributeDefinitions|否|
|BillingModeSummary|否|
|CreationDateTime|否|
|GlobalSecondaryIndexes|是|
|GlobalTableVersion|否|
|ItemCount|是|
|KeySchema|是|
|LatestStreamArn|是|
|LatestStreamLabel|是|
|LocalSecondaryIndexes|是|
|ProvisionedThroughput|否|
|Replicas|否|
|RestoreSummary|否|
|SSEDescription|否|
|StreamSpecification|是|
|TableArn|否|
|TableId|否|
|TableName|是|
|TableSizeBytes|是|
|TableStatus|是|

## 表达式支持情况

-   带`.`属性名的处理：一个带`.`的属性名可能表示一个scalar属性，也可能表示一个嵌入文档。在DynamoDB中的处理规则是：如果在表达式属性名中能够找到该属性名对应的映射，就按照scalar属性进行处理，否则按照嵌入文档进行处理。

    **说明：** 目前暂不支持带`.`scalar属性的相关处理，如查询、投影等。

-   ProjectionExpression： 只支持一维数组，并且当表达式中只包含数组某个元素时则会返回其他字段。
-   ConditionExpression：
    -   DynamoDB中的ConditionExpression语法如下：

        ```
        condition-expression ::=
              operand comparator operand
            | operand BETWEEN operand AND operand
            | operand IN ( operand (',' operand (, ...) ))
            | function
            | condition AND condition
            | condition OR condition
            | NOT condition
            | ( condition )
        
        comparator ::=
            =
            | <>
            | <
            | <=
            | >
            | >=
        
        function ::=
            attribute_exists (path)
            | attribute_not_exists (path)
            | attribute_type (path, type)
            | begins_with (path, substr)
            | contains (path, operand)
            | size (path)
        ```

    -   `operand1 comparator operand2`语法中，`operand1`必须为`path`，`operand2`必须为表达式属性值。
    -   `operand1 BETWEEN operand2 AND operand3`语法中，`operand1`必须为`path`，其余`operand`必须为表达式属性值。
    -   `operand1 IN ( operand2 (',' operand3 (, ...) ))`语法中，`operand1`必须为`path`，其余`operand`必须为表达式属性值。
    -   对于`function`中的`size(path)`函数，只支持`path`字段为字符串类型（判断长度）或`Set/List`类型，用于判断大小，不支持`Binary`和`Map`类型。
-   UpdateExpression：
    -   DynamoDB中的UpdateExpression语法如下：

        ```
        update-expression ::=
            [ SET action [, action] ... ]
            [ REMOVE action [, action] ...]
            [ ADD action [, action] ... ]
            [ DELETE action [, action] ...]
        
        set-action ::=
            path = value
        
        value ::=
            operand
            | operand '+' operand
            | operand '-' operand
        
        operand ::=
            path | function
        
        function ::=
            if_not_exists (path, value)
            | list_append (list1, list2)
        
        remove-action ::=
            path
        
        add-action ::=
            path value
        
        delete-action ::=
            path value
        ```

    -   set-action：
        -   `SET path = operand`语法中，不支持`operand`是`path`的场景。
        -   `SET path = operand1 '+'|'-' operand2`语法中，`operand1`必须等于`path`，即在此场景下只支持字段自增或自减。
        -   `SET path = if_not_exists (path, value)`语法中，两个`path`必须相等，且`value`只能是表达式属性值。
        -   `SET path = if_not_exists (path, value)`语法中，在同时指定多个时不支持部分更新，即需要满足全部条件才能执行成功。
        -   `SET path = list_append(list1, list2)`语法中，`list1`和`list2`中必须有一个等于`path`，另外一个是表达式属性值。
    -   remove-action：用于移除`List`中某个元素时，用`null`代替被移除的元素，`List`大小不变，剩下的元素不会发生移位。

## 数据类型映射说明

DynamoDB提供的数据类型和MongoDB的不同，因此，阿里云会在DynamoDB协议兼容版以及MongoDB的数据类型之间做映射，使二者相互兼容彼此的数据类型。

数据类型映射关系表：

|DynamoDB数据类型|MongoDB数据类型|
|------------|-----------|
|B|Binary data|
|BOOL|Boolean|
|BS|\*|
|L|Array|
|M|Object|
|N|Double|
|NS|\*|
|NULL|Null|
|S|String|
|SS|\*|

**说明：** DynamoDB中的BS（binary set）、NS（number set）、SS（string set）数据类型不允许重复数据。例如，在NS中插入`1,2,2,3`，NS会对数据做去重操作，最终结果会变成`1,2,3`。而DynamoDB协议兼容版当前暂不支持对这三种数据类型进行去重，因此上面表格中标记为星号（\*）的部分都将作为数组（Array）进行处理。阿里云会在后续版本中对这三种数据类型进行优化以支持去重。

## 最佳实践

您可以将DynamoDB迁移到阿里云数据库MongoDB版，详情请参见[使用NimoShake将Amazon DynamoDB迁移至阿里云](/cn.zh-CN/用户指南/数据迁移和同步/第三方云迁移到阿里云/使用NimoShake将Amazon DynamoDB迁移至阿里云.md)。

