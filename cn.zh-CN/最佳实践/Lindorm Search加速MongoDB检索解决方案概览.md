# Lindorm Search加速MongoDB检索解决方案概览

本文介绍通过Lindorm Search功能，在MongoDB上构建全托管、一体化的搜索分析能力，助力企业更好地管理数据。

云数据库MongoDB版在互联网、游戏、金融等领域都有着广泛的应用。随着业务的不断发展，越来越多的企业希望对存储于MongoDB数据库中的数据进行搜索分析。原生MongoDB内置的全文索引（Text Indexes）仅支持字符串类型的搜索查询，而且查询能力有限，无法满足例如文本分词、模糊查询、打分排序、结果高亮显示、聚合分析等高级检索需求。如果将MongoDB中的数据同步到外部搜索系统Solr、Elasticsearch中，又会带来开发运维的复杂性。

为了满足这一需求，云数据库MongoDB与[云原生多模数据库Lindorm](https://www.aliyun.com/product/apsaradb/lindorm)联合推出一体化的全文搜索方案，极大程度上增强了MongoDB的检索能力。关于Lindorm的更多信息，请参见[Lindorm产品概述]()。

![解决方案](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7828805061/p181695.png)

## 核心能力

本方案提供如下几个核心能力：

|核心能力类别|核心能力说明|
|------|------|
|云原生|-   一键开通，完全托管。
-   资源弹性伸缩，满足任意规模的需求。 |
|丰富搜索功能|-   覆盖所有数据类型。
-   支持文本相关性查询，多语言智能分词。
-   具备查询补全、结果高亮显示、聚合分析等全文搜索功能。 |
|简单易用|-   索引列按需管理，可轻松增删。
-   历史数据自动构建、实时数据自动同步，毫秒级同步延迟。
-   即将支持MQL（MetaQuotes Language）统一访问，自动利用全文搜索优化查询。 |

## 功能支持

目前本解决方案定向邀测中，欢迎有需求的用户[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)或扫下列钉钉二维码进群。

![二维码](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7828805061/p181707.png)

