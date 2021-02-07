# DescribeParameterModificationHistory

You can call this operation to query the modification records of ApsaraDB for MongoDB instance parameters.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Dds&api=DescribeParameterModificationHistory&type=RPC&version=2015-12-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeParameterModificationHistory|The operation that you want to perform. Set the value to **DescribeParameterModificationHistory**. |
|StartTime|String|Yes|2019-01-01T12:10Z|The beginning of the time range to query. Specify the time in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC. |
|EndTime|String|Yes|2019-01-02T12:10Z|The end of the time range to query. Specify the time in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC. |
|DBInstanceId|String|Yes|dds-bpxxxxxxxx|The ID of the instance.

**Note:** If you set the value to the ID of a sharded cluster instance, you must specify the **NodeId** parameter. |
|CharacterType|String|Yes|mongos|The role of the object that you want to query. Valid values:

-   db: shard
-   cs: Configserver
-   mongos: mongos
-   logic: sharded cluster instance |
|NodeId|String|No|d-bpxxxxxxxx|The ID of the mongos or shard node in the specified sharded cluster instance.

**Note:** This parameter takes effect only when you set the **DBInstanceId** parameter to the ID of a sharded cluster instance. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeDBInstanceAttribute](~~62010~~) operation to query the region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|HistoricalParameters|Array of HistoricalParameter| |Details about the parameter modification records. |
|HistoricalParameter| | | |
|ModifyTime|String|2019-03-12T07:58:24Z|The time when the parameter was modified. The time is in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC. |
|NewParameterValue|String|200|The parameter value after modification. |
|OldParameterValue|String|100|The parameter value before modification. |
|ParameterName|String|operationProfiling.slowOpThresholdMs|The name of the modified parameter. |
|RequestId|String|B1BB6E0E-B4EF-4145-81FA-A07719860248|The ID of the request. |

## Examples

Sample requests

```
http(s)://mongodb.aliyuncs.com/? Action=DescribeParameterModificationHistory
&StartTime=2019-01-01T12:10Z
&EndTime=2019-01-02T12:10Z
&DBInstanceId=dds-bpxxxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeParameterModificationHistoryResponse>
      <HistoricalParameters>
            <HistoricalParameter>
                  <OldParameterValue>100</OldParameterValue>
                  <ModifyTime>2019-03-12T07:58:24Z</ModifyTime>
                  <NewParameterValue>200</NewParameterValue>
                  <ParameterName>operationProfiling.slowOpThresholdMs</ParameterName>
            </HistoricalParameter>
      </HistoricalParameters>
      <RequestId>B1BB6E0E-B4EF-4145-81FA-A07719860248</RequestId>
</DescribeParameterModificationHistoryResponse>
```

`JSON` format

```
{
    "HistoricalParameters": {
        "HistoricalParameter": [
            {
                "OldParameterValue": "100",
                "ModifyTime": "2019-03-12T07:58:24Z",
                "NewParameterValue": "200",
                "ParameterName": "operationProfiling.slowOpThresholdMs"
            }
        ]
    },
    "RequestId": "B1BB6E0E-B4EF-4145-81FA-A07719860248"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Dds).

