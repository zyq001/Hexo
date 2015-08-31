title: 列式Parquet与行式Avro，对比Benchmarks性能测试
date: 2015-09-01 00:40:09
tags: [parquet, 列式存储, HDFS, Spark]
categories: [Hadoop, HDFS, 存储格式] 

---

## 关于Parquet
Parquet是面向分析型业务的列式存储格式，由Twitter和Cloudera合作开发，2015年5月从Apache的孵化器里毕业成为Apache顶级项目，细节请参考[[这里|http://parquet.apache.org/documentation/latest/]]。

### 列式存储
<!-- more -->

列式存储和行式存储相比有哪些优势呢？

  *可以跳过不符合条件的数据，只读取需要的数据，降低IO数据量。
  *压缩编码可以降低磁盘存储空间。由于同一列的数据类型是一样的，可以使用更高效的压缩编码（例如Run Length Encoding和Delta Encoding）进一步节约存储空间。
  *只读取需要的列，支持向量运算，能够获取更好的扫描性能。

### 适配多种计算框架

Parquet是语言无关的，而且不与任何一种数据处理框架绑定在一起，适配多种语言和组件，能够与Parquet配合的组件有：

查询引擎: Hive, Impala, Pig, Presto, Drill, Tajo, HAWQ, IBM Big SQL

计算框架: MapReduce, Spark, Cascading, Crunch, Scalding, Kite

数据模型: Avro, Thrift, Protocol Buffers, POJOs

### 性能

Parquet就是基于Google的Dremel系统的数据模型和算法实现的。核心思想是使用“record shredding and assembly algorithm”来表示复杂的嵌套数据类型，同时辅以按列的高效压缩和编码技术，实现降低存

储空间，提高IO效率，降低上层应用延迟。

Parquet列式存储带来的性能上的提高在业内已经得到了充分的认可，特别是当你们的表非常宽（column非常多）的时候，Parquet无论在资源利用率还是性能上都优势明显。具体的性能指标详见参考文档。

Spark已经将Parquet设为默认的文件存储格式，Cloudera投入了很多工程师到Impala+Parquet相关开发中，Hive/Pig都原生支持Parquet。Parquet现在为Twitter至少节省了1/3的存储空间，同时节省了大量的表

扫描和反序列化的时间。这两方面直接反应就是节约成本和提高性能（详见[[YaqiangZang#benchmark|benchmark]]）。

## benchmark 
以邮箱的展示日志为例，比较了Avro和Parquet两种存储格式的性能：camus-2015/05/24的日志，5,361,809条记录，ns005，hadoop2.4，Spark1.3.1。如下：
||-||encoded size(MB,Snappy)||Standlone单线程1列（ms）(read, fliter, count)||SparkSql 1列(ms)(read, fliter, count)||Spark 1列(ms)(read，fliter, count)||Spark 4列(read, count)||
||Avro||687||43,634||-||28,469(newAPIHadoopFile：39,226)||29,020||
||Parquet||660||3,355||6,981||3,530||9,359||

备注：1. 测试代码详见[[https://github.com/zyq001/AvroParquetBenchMark]]   2. 读取Avro是新老API性能差距较大，目前还未找到原因。

## 与Avro 

之前新统计系统（Quipu）的日志都是用Avro做序列化和存储，鉴于Parquet的优势和对Avro的兼容，将HDFS上的存储格式改为Paruqet，并且只需做很小的改动就用原读取Avro的API读取Parquet，单列查询效率可

以提高近一个数量级。



## Schema
Parquet文件尾部存储了文件的元数据信息和统计信息，自描述的，方便解析。仍沿用原Avro的schema。
