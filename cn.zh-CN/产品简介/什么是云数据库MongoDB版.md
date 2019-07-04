# 什么是云数据库MongoDB版 {#concept_egq_tvn_tdb .concept}

云数据库MongoDB版（ApsaraDB for MongoDB）完全兼容MongoDB协议，基于飞天分布式系统和高可靠存储引擎，提供多节点高可用架构、弹性扩容、容灾、备份回滚、性能优化等解决方案。

## 为什么选择云数据库MongoDB版 {#section_6o9_uoy_1e1 .section}

详情请参见[云数据库MongoDB与自建数据库对比优势](cn.zh-CN/产品简介/云数据库MongoDB与自建数据库对比优势.md#)和[应用场景](cn.zh-CN/产品简介/应用场景.md#)。

## 学习路径 {#section_ojj_18l_fp1 .section}

您可以通过[云数据库MongoDB版学习路径](https://help.aliyun.com/product/26556.html)，由浅入深地了解云数据库MongoDB版的相关概念、基础操作、进阶操作等。

## 支持的架构 {#section_r8z_cic_h4w .section}

云数据库MongoDB版支持灵活的部署架构，能够满足不同的业务场景。

|实例架构|说明|
|:---|:-|
|单节点实例|单节点实例适用于开发、测试及其他非企业核心数据存储的场景。让您能够以更低的入门价格享受云数据库MongoDB版在运维支持、内核级优化上的产品优势。|
|副本集实例| 在系统自动搭建的副本集实例中，提供一个可使用的Primary节点，一个隐藏的Secondary节点（对用户不可见），剩余节点为可使用的Secondary节点。

 您可以根据业务需要，例如阅读类网站、订单查询系统等读多写少场景或有临时活动的突发业务，按需增删Secondary节点，更好地实现读取性能扩展。

 |
|分片集群实例|基于多个副本集（每个副本集沿用三副本模式）组成的分片集群实例。分片集群实例提供Mongos、Shard、ConfigServer三个组件。您可以自由地选择Mongos和Shard节点的个数和配置，组建服务能力不同的MongoDB集群。更多关于组件作用的详细介绍，请参见[名词解释](cn.zh-CN/产品简介/名词解释.md#)。 **说明：** 

-   Mongos节点：为服务代理，当前是单节点架构。单个分片集群实例支持2-32个Mongos节点。
-   Shard节点：为分片服务器，当前是三节点副本集架构。单个分片集群实例支持2-32个Shard节点。
-   ConfigServer节点：为配置服务器，当前是三节点副本集架构。默认规格为1核2G，20GB存储空间，不支持变更规格和存储空间。

 |

## 产品定价 {#section_vhd_jie_3qu .section}

详情请参见[收费项目及价格说明](../../../../cn.zh-CN/产品定价/收费项目及价格说明.md#)。

## 部署建议 {#section_706_2ma_zim .section}

您可以从以下维度考虑如何创建并使用MongoDB实例：

-   地域和可用区

    地域指阿里云的数据中心，可用区是指在同一地域内，电力和网络互相独立的物理区域。地域和可用区决定了MongoDB实例所在的物理位置，一旦成功创建MongoDB实例后将无法更换地域。更多详情，请参见[地域和可用区](https://help.aliyun.com/document_detail/40654.html)。

    您可以从用户地理位置、阿里云产品发布情况、应用可用性以及是否需要内网通信等因素选择地域和可用区。例如，您的应用部署在[云服务器ECS](https://help.aliyun.com/document_detail/25367.html)（Elastic Compute Service）实例上，需要使用MongoDB实例作为该应用的数据库，那么在创建MongoDB实例时，应当选择与ECS实例相同的地域和可用区。

    **说明：** 同一可用区内的ECS实例和MongoDB实例通过内网连接时，网络延时最小。

-   网络规划

    阿里云推荐您使用[专有网络VPC](https://help.aliyun.com/document_detail/34217.html?spm=a2c4g.11186623.2.46.4b8550bf7ZVeSp#concept-kbk-cpz-ndb)，您可自行规划私网IP地址段。专有网络是一种隔离的网络环境，安全性和性能均高于传统的经典网络，专有网络需要事先创建，详情请参见[新建实例场景下配置专有网络](../../../../cn.zh-CN/用户指南/管理网络连接/新建实例场景下配置专有网络.md#)。

-   安全方案

    针对用户重点关注的数据安全，云数据库MongoDB版提供了全面的安全保障。您可以通过同城容灾、RAM授权、审计日志、网络隔离、白名单、密码认证等多手段保障数据库数据安全。详情请参见[云数据库MongoDB版数据安全最佳实践](../../../../cn.zh-CN/最佳实践/云数据库MongoDB版数据安全最佳实践.md#)。


## 如何使用云数据库MongoDB版 {#section_mun_mlh_q4w .section}

您可以通过以下方式管理MongoDB实例，进行实例创建、网络设置、数据库创建、账号创建等操作：

-   [控制台](https://mongodb.console.aliyun.com/)：提供图形化的Web界面，操作方便。
-   [CLI](https://help.aliyun.com/product/29991.html)：控制台上所有的操作都可以通过CLI实现。
-   [SDK](https://help.aliyun.com/document_detail/62676.html)：控制台上所有的操作都可以通过SDK实现。
-   [API](https://help.aliyun.com/document_detail/61715.html)：控制台上所有的操作都可以通过API实现。

创建MongoDB实例后，您可以通过以下方式访问MongoDB实例：

-   DMS：您可以[通过DMS登录MongoDB数据库](../../../../cn.zh-CN/副本集快速入门/连接实例/通过DMS登录MongoDB数据库.md#)，在Web界面进行数据库开发工作。
-   Mongo Shell：MongoDB官方命令行工具，您可以[通过Mongo Shell登录MongoDB数据库](../../../../cn.zh-CN/副本集快速入门/连接实例/通过Mongo Shell登录MongoDB数据库.md#)，对数据库进行管理操作。
-   客户端：云数据库MongoDB版完全兼容MongoDB协议，您可以使用通用的数据库客户端工具访问MongoDB实例。例如Robo 3T、Studio 3T等。

## 相关服务 {#section_e5v_kp9_9ig .section}

-   [ECS](https://help.aliyun.com/document_detail/25367.html)：云服务器ECS（Elastic Compute Service）通过内网访问同一地域的MongoDB实例时，可实现最佳性能。ECS搭配MongoDB实例是典型的业务访问架构。
-   [DTS](https://help.aliyun.com/document_detail/26592.html)：您可以使用数据传输服务DTS（Data Transmission Service）将本地MongoDB数据库迁移上云。
-   [OSS](https://help.aliyun.com/document_detail/31817.html)：对象存储服务OSS（Object Storage Service）是阿里云提供的海量、安全、低成本、高可靠的云存储服务。
-   [HDM](https://help.aliyun.com/product/63907.html)：混合云数据库管理HDM（Hybrid Cloud Database Management）帮助企业打通混合云数据库架构，提供多环境统一管理、快速弹性、容灾切换的能力，您可以通过HDM查询云数据库MongoDB的实时性能和实时操作，分析慢日志、管理存储空间等操作。
-   [云HBase](https://help.aliyun.com/document_detail/49501.html)：云HBase是基于Apache HBase和HBase生态构建的低成本一站式数据处理平台，又称HBase X-Pack。云Spark分析引擎支持对接云数据库MongoDB版，提供分析MongoDB数据库的能力。

