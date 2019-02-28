# DescribeRunningLogRecords {#concept_mpn_mbj_wgb .concept}

该接口用于查询实例的运行日志，适用于副本集实例和分片集群实例。

## 输入参数 {#section_qhk_j3j_wgb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是| 系统规定参数，取值：DescribeErrorLogList。

 |
|StartTime|String|是| 查询开始时间。

 格式为*yyyy-MM-dd*T*HH:mm*Z，例如2011-05-30T12:10Z。

 |
|EndTime|String|是| 查询结束时间，必须晚于查询开始时间。

 格式为*yyyy-MM-dd*T*HH:mm*Z，例如2011-05-30T12:11Z。

 |
|DBInstancId|String|是| 实例ID。

 |
|NodeId|String|否| Shard节点ID或Mongos节点ID。

 实例为分片集群实例时，该参数必传。

 |
|RoleType|String|否| 实例角色。取值 primary 或 secondary。

 |
|PageSize|Integer|是| 每页记录数，取值：\[30-100\]。

 |
|PageNumbers|Integer|是| 页码，大于0的整数。

 |

## 返回参数 {#section_ktp_k3j_wgb .section}

|参数|类型|说明|
|:-|:-|:-|
|LogRecords|List| 运行日志明细，数据格式为\[log1,log2,log3, …\]。

 |
|PageNumbers|Integer| 页码。

 |
|TotalRecordCount|Integer| 总记录数。

 |
|公共返回参数|-| 详见[公共返回参数](cn.zh-CN/API参考/公共参数.md#)。

 |

## LogRecords {#section_ptg_v3j_wgb .section}

|参数|类型|说明|
|:-|:-|:-|
|Category|String| 日志类别。

 |
|CreateTime|String| 日志生成的时间。

 格式为*yyyy-MM-dd*T*HH:mm:ss*Z，例如2011-05-30T12:10:20Z。

 |
|ConnInfo|String| 日志连接信息。

 |
|Content|String| 日志信息。

 |

