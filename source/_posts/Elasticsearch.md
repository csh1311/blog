---
title: Elasticsearch
date: 2023-09-18 12:53:28
tags:
---

# `Elasticsearch`

## 什么是`Elasticsearch`

​		`Elasticsearch`是一个开源的分布式` RESTful `搜索和分析引擎，它专注于处理和存储大量数据，以便快速、准确地进行搜索、分析和可视化,

​		`Elasticsearch` 是一个近乎实时的搜索平台。这意味着从对文档建立索引到可搜索之间存在轻微的延迟（通常为一秒）。

## 特点

### 三大特点

1. 具备很好的横向扩展能力，天然带着数据库的分片技术，如果你使用数据库还要分库分表，在`Elasticsearch`中不需，自带分片技术
2. 极限的性能，能够在毫秒级来返回你所搜索的结果，`Elasticsearch`技术特点相关，因为`Elasticsearch`基于倒排索引，通过索引来提升查询的效率
3. 相关性：

1. 全文搜索： `Elasticsearch`以全文搜索为核心功能，允许你轻松地在大规模文本数据中查找关键字、短语和复杂查询
2. 分布式架构： 它被设计为分布式系统，能够轻松处理大规模数据，自动分布到多个节点，以提高性能和可伸缩性。
3. 实时数据：`Elasticsearch`支持实时索引，允许不断的将数据添加到索引中，以便立即进行搜索和分析。
4. 多数据类型：除了文本数据，它还可以用于结构化和半结构化数据，包括日志、时间序列数据、地理空间数据等。
5. 强大的语言查询： `Elasticsearch`使用`JSON`格式的查询语言，允许你创建高度定制化的查询，包括范围查询、模糊搜索、过滤、聚合等。
6. 实时分析和可视化：*通过与工具如Kibana集成，你可以实时分析数据并创建仪表板、可视化数据趋势。
7. 用途广：` Elasticsearch`被广泛应用于各种领域，包括搜索引擎、日志和事件数据分析、安全信息与事件管理、电子商务产品搜索等。

## 学习步骤

### 安装`Elasticsearch`和`kibanna`

1. 如果使用Docker Desktop，请确保分配至少4`GB`的内存。您可以在Docker Desktop的设置>资源中调整内存使用情况。

2. 使用docker-compose

   ```
   version: "3.0"
   services:
     es-elasticsearch:
       container_name: es-elasticsearch
       image: docker.elastic.co/elasticsearch/elasticsearch:7.0.1
       environment:
         - cluster.name＝docker-cluster
         - xpack.security.enabled=false
         - "discovery.type=single-node"
       networks:
         - es-net
       ports:
         - 9200:9200
     kb-kibana:
       container_name: kb-kibana
       image: docker.elastic.co/kibana/kibana:7.0.1
       environment:
         - ELASTICSEARCH_HOSTS=http://es-elasticsearch:9200
         - I18N_LOCALE＝zh-CN
       networks:
         - es-net
       depends_on:
         - es-elasticsearch
       ports:
         - 5601:5601
   networks:
     es-net:
       driver: bridge
   ```

3. 安装完成在浏览器输入网址http://localhost:5601/

   ![image-20230921093636058](D:\project\blogImage\image-20230921093636058.png)

4. 设置中文，打开`/usr/share/kibana/config/kibana.yml`在里面添加以下代码

   ```
   i18n.locale: "zh-CN
   ```

   

## CRUD

1. 查询数据

   - 获取版本信息

     ```
     GET /
     ```

   - 

2. 添加数据

   数据是以文档的形式存储，但是文档的内容是以`json`对象的，这些文档可以存储在索引中

   - ccsh：索引名称
   - _doc:什么类型
   - 1:唯一标识

   ```
   POST ccsh/_doc/1
   {
     "user":"GB",
     "uid":1,
     "city":"Beijing",
     "province":"Beijing",
     "country":"china"
   }
   ```

3. 修改数据

   - 根据内容全部替换

     ```
     
     PUT ccsh/_doc/1
     {
       "user":"GB",
       "uid":1,
       "city":"北京",
       "province":"北京",
       "country":"中国"
     }
     ```

   - 更具字段修改该数据_update_by_query

     ```
     POST ccsh/_update_by_query
     {
       "script": {
         "source": "ctx._source.city = params.city; ctx._source.province = params.province; ctx._source.country = params.country;",
         "lang": "painless",
         "params": {
           "city": "上海",
           "province": "上海",
           "country": "中国"
         }
       },
       "query": {
         "match": {
           "user": "GB"
         }
       }
     }
     
     ```

   - 

4. 删除数据

   - 删除整个索引

     ```
     DELETE ccsh
     ```

   - 删除索引中的某个文档

     ```
     DELETE aa/_doc/2
     ```

   - 
