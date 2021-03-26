什么是云数据库MongoDB版 
====================================

云数据库MongoDB版（ApsaraDB for MongoDB）完全兼容MongoDB协议，基于飞天分布式系统和高可靠存储引擎，提供多节点高可用架构、弹性扩容、容灾、备份恢复、性能优化等功能。

MongoDB的数据结构 
---------------------------------

MongoDB是面向文档的NoSQL（非关系型）数据库，它的数据结构由字段（Field）和值（Value）组成，类似于JSON对象，示例如下：



    {
        name:"张三",
        sex:"男性",
        age:30
    }



MongoDB的存储结构 
---------------------------------

MongoDB的存储结构区别于传统的关系型数据库，由如下三个单元组成：



* 文档（Document）：MongoDB中最基本的单元，由BSON键值对（key-value）组成。相当于关系型数据库中的行（Row）。

  

* 集合（Collection）：一个集合可以包含多个文档，相当于关系型数据库中的表格（Table）。

  

* 数据库（Database）：等同于关系型数据库中的数据库概念，一个数据库中可以包含多个集合。您可以在MongoDB中创建多个数据库。

  




为什么选择云数据库MongoDB版 
--------------------------------------

详情请参见[产品优势]()和[应用场景](/cn.zh-CN/产品简介/应用场景.md)。

学习路径 
-------------------------

您可以通过[云数据库MongoDB版学习路径](https://help.aliyun.com/product/26556.html)，由浅入深地了解云数据库MongoDB版的相关概念、基础操作、进阶操作等。

产品定价 
-------------------------

详情请参见[收费项目及价格说明](/cn.zh-CN/产品定价/收费项目及价格说明.md)。

专属集群 
-------------------------

当前专属集群MyBase已支持MongoDB引擎，您可以以MyBase的形态购买MongoDB实例。详情请参见[什么是云数据库专属集群MyBase]()。

部署建议 
-------------------------

您可以从以下维度考虑如何创建并使用MongoDB实例：

* 地域和可用区 

  地域指阿里云的数据中心，可用区是指在同一地域内，电力和网络互相独立的物理区域。地域和可用区决定了MongoDB实例所在的物理位置，一旦成功创建MongoDB实例后将无法更换地域。更多详情，请参见[地域和可用区](~~40654~~)。

  您可以从用户地理位置、阿里云产品发布情况、应用可用性以及是否需要内网通信等因素选择地域和可用区。例如，您的应用部署在[云服务器ECS](~~25367~~)（Elastic Compute Service）上，需要使用MongoDB实例作为该应用的数据库，那么在创建MongoDB实例时，应当选择与ECS实例相同的地域和可用区。 

  
  **说明**

  同一可用区内的ECS实例和MongoDB实例通过内网连接时，网络延时最小。

  

* 网络规划 

  阿里云推荐您使用[专有网络VPC](~~34217~~)，您可自行规划私网IP地址段。专有网络是一种隔离的网络环境，安全性和性能均高于传统的经典网络，您可以使用默认的专有网络，也可以自行事先创建，详情请参见[新建实例场景下配置专有网络](/cn.zh-CN/用户指南/管理网络连接/新建实例场景下配置专有网络.md)。
  

* 安全方案 

  针对用户重点关注的数据安全，云数据库MongoDB版提供了全面的安全保障。您可以通过同城容灾、RAM授权、审计日志、网络隔离、白名单、密码认证、透明数据加密TDE等多手段保障数据库数据安全。详情请参见[云数据库MongoDB版数据安全最佳实践](/cn.zh-CN/最佳实践/云数据库MongoDB版数据安全最佳实践.md)。
  




如何使用云数据库MongoDB版 
-------------------------------------

您可以通过以下方式管理MongoDB实例，进行实例创建、网络设置、数据库创建、账号创建等操作：

* [控制台](https://mongodb.console.aliyun.com/)：提供图形化的Web界面，操作方便。

  

* [CLI](https://help.aliyun.com/product/29991.html)：控制台上所有的操作都可以通过CLI实现。

  

* [SDK](https://help.aliyun.com/document_detail/62676.html)：控制台上所有的操作都可以通过SDK实现。

  

* [API](/cn.zh-CN/API参考/API概览.md)：控制台上所有的操作都可以通过API实现。

  




创建MongoDB实例后，您可以通过以下方式访问MongoDB实例：

* DMS：您可以[通过DMS连接MongoDB副本集实例](/cn.zh-CN/快速入门/连接实例/通过DMS连接MongoDB副本集实例.md)，在Web界面进行数据库开发工作。

  

* Mongo Shell：MongoDB官方命令行工具，您可以[通过Mongo Shell连接MongoDB副本集实例](/cn.zh-CN/快速入门/连接实例/通过Mongo Shell连接MongoDB副本集实例.md)，对数据库进行管理操作。

  

* 客户端：云数据库MongoDB版完全兼容MongoDB协议，您可以使用通用的数据库客户端工具访问MongoDB实例。例如Robo 3T、Studio 3T等。

  




相关服务 
-------------------------

* [ECS](~~25367~~)：云服务器ECS（Elastic Compute Service）通过内网访问同一地域的MongoDB实例时，可实现最佳性能。ECS搭配MongoDB实例是典型的业务访问架构。

  

* [DTS](/cn.zh-CN/产品简介/什么是数据传输服务DTS.md)：您可以使用数据传输服务DTS（Data Transmission Service）将本地MongoDB数据库迁移上云。

  

* [OSS](~~31817~~)：对象存储服务OSS（Object Storage Service）是阿里云提供的海量、安全、低成本、高可靠的云存储服务。

  

* [DAS](https://help.aliyun.com/product/63907.html)：数据库自治服务DAS（Database Autonomy Service）帮助企业打通混合云数据库架构，提供多环境统一管理、快速弹性、容灾切换的能力，您可以通过DAS查询云数据库MongoDB的实时性能和实时操作，分析慢日志、管理存储空间等操作。

  




<!-- -->

* [DLA]()：云原生数据湖分析DLA（Data Lake Analytics）是新一代大数据解决方案，采取计算与存储完全分离的架构，提供弹性的Serverless SQL与Serverless Spark服务，满足在线交互式查询、流处理、批处理、机器学习等诉求。相关链接：

  * [Serverless SQL对接MongoDB快速入门]()

    
  
  * [Serverless Spark对接MongoDB快速入门]()

    
  

  




<!-- -->

* [云HBase](https://help.aliyun.com/document_detail/49501.html)：云HBase是基于Apache HBase和HBase生态构建的低成本一站式数据处理平台，又称HBase X-Pack。云Spark分析引擎支持对接云数据库MongoDB版，提供分析MongoDB数据库的能力。

  



