---
title: phoenix-Hbase
date: 2023-10-10 15:33:08
tags:
toc: false
published: false
---

# Phoeix-Hbase是什么

​	Phoenix-Hbase是一个开源的工具，它将Apache Hbase（一个分布式NoSQL数据库）与Apache Phoenix（一个基于SQL的查询引擎）集成在一起，以便在Hbase上执行SQL查询。这个工具使用户能够使用熟悉的SQL语言来查询和操作存储在Hbase中的数据，而无需编写复杂的Hbase客户端代码。

​	Phoenix-Hbase提供了类似于传统关系型数据库的查询功能，包括筛选、排序、聚合和连接等操作，但可以在Hbase这种分布式和高可扩展性的存储系统上执行这些操作。这对于需要在大规模数据上执行实时查询的应用程序非常有用，例如大数据分析和实时报告生成。

# 为什么要使用Phoenix-Hbase

Phoenix-Hbase允许您使用SQL语言来查询和操作存储在Hbase中的数据，Phoenix-Hbase简化了与Hbase交互的方式，减少了开发人员的工作量。您可以像与传统关系型数据库一样执行查询，而不必处理Hbase的底层复杂性

# 如何使用Phoenix-Hbase

### Quick start

- 安装部署完成，在命令行输入

```
//sqlline是Phoenix的启动脚步，192.168.60.40是zookeeper的地址
sqlline.py 192.168.60.40:2181
```

- 创建一个表

```
create table "test" (mykey integer not null primary key, mycolumn varchar);
upsert into "test" values (1,'Hello');
upsert into "test" values (2,'World!');
```

```
select * from "test";
```

- 查询的结构

```
+-------+------------+
| MYKEY |  MYCOLUMN  |
+-------+------------+
| 1     | Hello      |
| 2     | World!     |
+-------+------------+
```



### 如何将Phoenix的表映射对应已有的Hbase的表

- Hbase创建一个表

  'con'：表名

  'log' :列族

  ```
  create 'con',{NAME => 'log', VERSIONS => 2}
  ```

- 创建列族的列

  ```
  alter 'con', {NAME => 'log', VERSIONS => 1}, {NAME => 'userid'}, {NAME => 'productid'}, {NAME => 'action'}, {NAME => 'time'}
  ```

- 添加数据到'con'

  ```
  put 'con', '1_122_1563799412', 'log:userid', '1'
  put 'con', '1_122_1563799412', 'log:productid', '122'
  put 'con', '1_122_1563799412', 'log:time', '1563799412'
  put 'con', '1_122_1563799412', 'log:action', '1'
  
  put 'con', '1_123_1563799391', 'log:userid', '1'
  put 'con', '1_123_1563799391', 'log:productid', '123'
  put 'con', '1_123_1563799391', 'log:time', '1563799391'
  put 'con', '1_123_1563799391', 'log:action', '2'
  
  put 'con', '1_123_1563799393', 'log:userid', '1'
  put 'con', '1_123_1563799393', 'log:productid', '123'
  put 'con', '1_123_1563799393', 'log:time', '1563799393'
  put 'con', '1_123_1563799393', 'log:action', '2'
  
  put 'con', '1_124_1563799394', 'log:userid', '1'
  put 'con', '1_124_1563799394', 'log:productid', '124'
  put 'con', '1_124_1563799394', 'log:time', '1563799394'
  put 'con', '1_124_1563799394', 'log:action', '2'
  ```

- 使用scan扫描Hbase中con表的全部数据

  ```
  ROW                                       COLUMN+CELL                                                                                                                                                                    
   1_122_1563799412                  column=log:_0, timestamp=2023-10-10T14:57:22.038, value=                                                                                                                       
   1_122_1563799412                  column=log:action, timestamp=2023-10-10T14:57:22.038, value=1                                                                                                                  
   1_122_1563799412                  column=log:productid, timestamp=2023-10-10T14:57:22.020, value=122                                                                                                             
   1_122_1563799412                  column=log:time, timestamp=2023-10-10T14:57:22.028, value=1563799412                                                                                                           
   1_122_1563799412                  column=log:userid, timestamp=2023-10-10T14:57:22.007, value=1                                                                                                                  
   1_123_1563799391                  column=log:_0, timestamp=2023-10-10T14:56:09.584, value=                                                                                                                       
   1_123_1563799391                  column=log:action, timestamp=2023-10-10T14:56:09.584, value=2                                                                                                                  
   1_123_1563799391                  column=log:productid, timestamp=2023-10-10T14:56:09.571, value=123                                                                                                             
   1_123_1563799391                  column=log:time, timestamp=2023-10-10T14:56:09.577, value=1563799391                                                                                                           
   1_123_1563799391                  column=log:userid, timestamp=2023-10-10T14:56:09.461, value=1                                                                                                                  
   1_123_1563799393                  column=log:_0, timestamp=2023-10-10T14:57:08.231, value=                                                                                                                       
   1_123_1563799393                  column=log:action, timestamp=2023-10-10T14:57:08.231, value=2                                                                                                                  
   1_123_1563799393                  column=log:productid, timestamp=2023-10-10T14:57:08.221, value=123                                                                                                             
   1_123_1563799393                  column=log:time, timestamp=2023-10-10T14:57:08.225, value=1563799393                                                                                                           
   1_123_1563799393                  column=log:userid, timestamp=2023-10-10T14:57:08.213, value=1                                                                                                                  
   1_124_1563799394                  column=log:_0, timestamp=2023-10-10T14:57:14.731, value=                                                                                                                       
   1_124_1563799394                  column=log:action, timestamp=2023-10-10T14:57:14.731, value=2                                                                                                                  
   1_124_1563799394                  column=log:productid, timestamp=2023-10-10T14:57:14.705, value=124                                                                                                             
   1_124_1563799394                  column=log:time, timestamp=2023-10-10T14:57:14.718, value=1563799394                                                                                                           
   1_124_1563799394                  column=log:userid, timestamp=2023-10-10T14:57:14.692, value=1   
  ```

  

- Phoenix创建映射Hbase的表

  如果创建表是表映射错了，要删除表，这样也会把habse的表也删除，删除表是需要保存好数据

  userid，productid，time，action是Hbase中的列，但这里用的是varchar,否则没有数据

  column_encoded_bytes：要加column_encoded_bytes=0,不然Phoenix用自己的编码,列的值就无法查看。

  ```
  CREATE TABLE "con" (
        "rowKey" VARCHAR NOT NULL PRIMARY KEY,
        "log"."userid"  VARCHAR,
        "log"."productid"  VARCHAR,
        "log"."time"  VARCHAR,
        "log"."action"  VARCHAR
  ) column_encoded_bytes=0;
  ```

- 查询数据

  ```
  select * from "con";
  ```

- 返回的数据

  ```
  +------------------+--------+-----------+------------+--------+
  |      rowKey      | userid | productid |    time    | action |
  +------------------+--------+-----------+------------+--------+
  | 1_122_1563799412 | 1      | 122       | 1563799412 | 1      |
  | 1_123_1563799391 | 1      | 123       | 1563799391 | 2      |
  | 1_123_1563799393 | 1      | 123       | 1563799393 | 2      |
  | 1_124_1563799394 | 1      | 124       | 1563799394 | 2      |
  +------------------+--------+-----------+------------+--------+
  ```

### 如何创建二级索引

#### 什么是索引

- 索引通常是数据库中的一种数据结构，用于快速检索和访问存储在数据库表中的数据，可以减少i/o操作

  - 不加索引会这么样

    假设你有一个表，表的数据有10万条数据，你要查询第10000条的数据，那么你就需要从第一条数据一条条的检索判断是否对应的数据，这样会使查询效率变慢

- 从 Phoenix 2.1 版开始，Phoenix 支持对可变和不可变数据进行索引。请注意，Phoenix 2.0.x 仅支持不可变数据上的索引。不可变表的索引写入性能索引比可变表稍快，但不可变表中的数据无法更新。

  - 可变表

    可以进行插入数据，更新数据，删除数据，数据是可以更改的

    ```
    create table test (id integer primary key, name varchar, email varchar);
    ```

    插入数据

    ```
    upsert into test values(1,'cc','163@163.com');
    upsert into test values(2,'ccsdas','admsd@163.com');
    upsert into test values(3,'ccsds','admsasdsad@163.com');
    ```

  - 不可变表

    数据一旦插入数据之后，就不能再进行更新或删除操作，这种表一般适合存储数据，

    ```
    create table test1 (id integer primary key, name varchar, email varchar) IMMUTABLE_ROWS=true;
    ```

    插入数据

    ```
    upsert into test1 values(1,'cc','163@163.com');
    upsert into test1 values(2,'ccsdas','admsd@163.com');
    upsert into test1 values(3,'ccsds','admsasdsad@163.com');
    ```

#### 二级索引

全局索引和本地索引

##### Global Indexes

全局索引适用于大量的读取数量，不适用于修改删除数据，都会引起索引表的更新，而索引表是分布在不同的数据节点上的，跨节点的数据传输带来了较大的性能消耗。

```
create index idx on test (email);
```

##### Local Indexes

本地索引目标*写入量大*，*空间有限*用例。就像全局索引一样，Phoenix 将在查询时自动选择是否使用本地索引。跟全局索引不一样索引表是分布在同一台数据节点上，防止写入期间产生任何网络开销。

##### immutable index

对于数据只写入一次并且从不就地更新的表，可以进行某些优化以减少增量维护的写入时间开销，IMMUTABLE_ROWS=true`属性添加到 DDL 语句来将表声明为不可变表

如果想要从不可变索引切换到可变索引，请使用`ALTER TABLE`命令，如下所示：

```
ALTER TABLE test1 SET IMMUTABLE_ROWS=false
```

##### mutable index

