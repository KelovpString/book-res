# 简介

## 简要介绍

## 特点

## Why ElasticSearch

作为一款开源的全文搜索引擎，Es在业内也非常有名，他是建立在全文搜索引擎 Apache Lucene基础上的搜索引擎。其实在上家公司也有接触和使用同类型的搜索引擎Solr（用于查询复杂的城市价格配置、自己维护的POI点信息，由于Solr在索引变更和新增数据的时候对CPU的损耗较高，所以一般像配置信息这种变动低频次的信息我们使用Solr存储[其实更深层次的原因是团队的成员对于solr都有非常不错的实践经验，所以那个时候选择的是Solr]），而这次我们面对的场景是亿级订单的查询（由于业务并未对订单时间维度做区分，所以订单量稳定在亿级别以上。）同时每天百万级的新增数量以及订单状态机对于同步和变更有着很苛刻的要求，基于Es分布式的特性，我我们选择了Es作为订单的搜索引擎