# Architecture of replica set instances {#concept_bnt_3zn_tdb .concept}

ApsaraDB for MongoDB automatically configures replica set instances. You can operate the primary and secondary nodes. Advanced functions such as disaster recovery failover and faulty node recovery are encapsulated in a package. You are not aware of these functions when you use instances.

## Architecture of replica set instances {#section_zhz_hl5_xgb .section}

![Architecture of ApsaraDB for MongoDB replica set instances](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/6645/156222401739716_en-US.png)

## Scale out replica set nodes {#section_xwg_jl5_xgb .section}

ApsaraDB for MongoDB allows you to scale out the number of nodes to five or seven. You can increase the number of secondary nodes as needed.

For example, you can add or remove secondary nodes to adjust the read/write performance for scenarios that require higher reading performance or unexpected business requirements from temporary activities.

