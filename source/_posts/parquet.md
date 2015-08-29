<<TableOfContents(3)>>

= ����Parquet =
Parquet�����������ҵ�����ʽ�洢��ʽ����Twitter��Cloudera����������2015��5�´�Apache�ķ��������ҵ��ΪApache������Ŀ��ϸ����ο�[[����|http://parquet.apache.org/documentation/latest/]]��

== ��ʽ�洢 ==

��ʽ�洢����ʽ�洢�������Щ�����أ�

  *�����������������������ݣ�ֻ��ȡ��Ҫ�����ݣ�����IO��������
  *ѹ��������Խ��ʹ��̴洢�ռ䡣����ͬһ�е�����������һ���ģ�����ʹ�ø���Ч��ѹ�����루����Run Length Encoding��Delta Encoding����һ����Լ�洢�ռ䡣
  *ֻ��ȡ��Ҫ���У�֧���������㣬�ܹ���ȡ���õ�ɨ�����ܡ�

== ������ּ����� ==

Parquet�������޹صģ����Ҳ����κ�һ�����ݴ����ܰ���һ������������Ժ�������ܹ���Parquet��ϵ�����У�

��ѯ����: Hive, Impala, Pig, Presto, Drill, Tajo, HAWQ, IBM Big SQL

������: MapReduce, Spark, Cascading, Crunch, Scalding, Kite

����ģ��: Avro, Thrift, Protocol Buffers, POJOs

== ���� ==

Parquet���ǻ���Google��Dremelϵͳ������ģ�ͺ��㷨ʵ�ֵġ�����˼����ʹ�á�record shredding and assembly algorithm������ʾ���ӵ�Ƕ���������ͣ�ͬʱ���԰��еĸ�Чѹ���ͱ��뼼����ʵ�ֽ��ʹ�

���ռ䣬���IOЧ�ʣ������ϲ�Ӧ���ӳ١�

Parquet��ʽ�洢�����������ϵ������ҵ���Ѿ��õ��˳�ֵ��Ͽɣ��ر��ǵ����ǵı�ǳ���column�ǳ��ࣩ��ʱ��Parquet��������Դ�����ʻ��������϶��������ԡ����������ָ������ο��ĵ���

Spark�Ѿ���Parquet��ΪĬ�ϵ��ļ��洢��ʽ��ClouderaͶ���˺ܶ๤��ʦ��Impala+Parquet��ؿ����У�Hive/Pig��ԭ��֧��Parquet��Parquet����ΪTwitter���ٽ�ʡ��1/3�Ĵ洢�ռ䣬ͬʱ��ʡ�˴����ı�

ɨ��ͷ����л���ʱ�䡣��������ֱ�ӷ�Ӧ���ǽ�Լ�ɱ���������ܣ����[[YaqiangZang#benchmark|benchmark]]����

<<Anchor(benchmark)>>
= benchmark =
�������չʾ��־Ϊ�����Ƚ���Avro��Parquet���ִ洢��ʽ�����ܣ�camus-2015/05/24����־��5,361,809����¼��ns005��hadoop2.4��Spark1.3.1�����£�
||-||encoded size(MB,Snappy)||Standlone���߳�1�У�ms��(read, fliter, count)||SparkSql 1��(ms)(read, fliter, count)||Spark 1��(ms)(read��fliter, count)||Spark 4��(read, count)||
||Avro||687||43,634||-||28,469(newAPIHadoopFile��39,226)||29,020||
||Parquet||660||3,355||6,981||3,530||9,359||

��ע��1. ���Դ������[[https://gitlab.corp.youdao.com/zangyq/avroparquetbenchmark/tree/master|AvroParquetBenchMark]]   2. ��ȡAvro������API���ܲ��ϴ�Ŀǰ��δ�ҵ�ԭ��

== ��Avro ==

֮ǰ��ͳ��ϵͳ��Quipu������־������Avro�����л��ʹ洢������Parquet�����ƺͶ�Avro�ļ��ݣ���HDFS�ϵĴ洢��ʽ��ΪParuqet������ֻ������С�ĸĶ�����ԭ��ȡAvro��API��ȡParquet�����в�ѯЧ�ʿ�

����߽�һ����������



= Schema =
Parquet�ļ�β���洢���ļ���Ԫ������Ϣ��ͳ����Ϣ���������ģ����������������ԭAvro��schema��
