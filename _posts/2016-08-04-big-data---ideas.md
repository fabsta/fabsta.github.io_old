---
title: "Big Data Concepts"
description: "Overview of hadoop tools"
category: BigData
tags: [BigData]
---



### Table of contents

* TOC
{:toc}


# General

## Lambda architecture
![https://lh3.googleusercontent.com/sWNk04rO-YJZP9Hm5tP6Nx-_NTVV0x_0iX8liBFB3M3HKm75-Yvy7r5-o_1HelRrgKRRIQedTXtZ_S7zzZkoZ2USdtx8f6TRZchmbrQAg_BdU5BhL5JT9d5iQhfIbQ4qow](https://lh3.googleusercontent.com/sWNk04rO-YJZP9Hm5tP6Nx-_NTVV0x_0iX8liBFB3M3HKm75-Yvy7r5-o_1HelRrgKRRIQedTXtZ_S7zzZkoZ2USdtx8f6TRZchmbrQAg_BdU5BhL5JT9d5iQhfIbQ4qow)

(<a href="#top">Back to top</a>)
<hr>


# Distributions

## Mapr
![http://images.slideplayer.com/15/4706189/slides/slide_4.jpg](http://images.slideplayer.com/15/4706189/slides/slide_4.jpg)

(<a href="#top">Back to top</a>)
<hr>

## Cloudera
![http://www.techweekly.com/viewpoints/wp-content/uploads/2013/06/Cloudera-hadoop-02.png](http://www.techweekly.com/viewpoints/wp-content/uploads/2013/06/Cloudera-hadoop-02.png)

(<a href="#top">Back to top</a>)<hr>

## Hortonworks
![http://hortonworks.com/wp-content/uploads/2016/03/asparagus-chart-hdp24.png](http://hortonworks.com/wp-content/uploads/2016/03/asparagus-chart-hdp24.png)

(<a href="#top">Back to top</a>)
<hr>


# Storage

## HDFS

### Architecture
![https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/6688OT_03_02.jpg](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/6688OT_03_02.jpg)

(<a href="#top">Back to top</a>)
<hr>

### Datanode
![https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/6688OT_03_03.jpg](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/6688OT_03_03.jpg)

(<a href="#top">Back to top</a>)
<hr>


### Read Path
![https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/6688OT_03_04.jpg](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/6688OT_03_04.jpg)

1. The client using a Distributed FileSystem object of Hadoop client API calls open() which initiate the read request.
2. Distributed FileSystem connects with NameNode. NameNode identifies the block locations of the file to be read and in which DataNodes the block is located. 
3. NameNode then sends the list of DataNodes in order of nearest DataNodes from the client.
4. Distributed FileSystem then creates FSDataInputStream objects, which, in turn, wrap a DFSInputStream, which can connect to the DataNodes selected and get the block, and return to the client. The client initiates the transfer by calling the read() of FSDataInputStream.
5. FSDataInputStream repeatedly calls the read() method to get the block data.
6. When the end of the block is reached, DFSInputStream closes the connection from the DataNode and identifies the best DataNode for the next block.
7. When the client has finished reading, it will call close() on FSDataInputStream to close the connection.

(<a href="#top">Back to top</a>)
<hr>


### Write Path
![https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/6688OT_03_05.jpg](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/6688OT_03_05.jpg)

1. The client, using a Distributed FileSystem object of Hadoop client API, calls create(), which initiates the write request.
2. Distributed FileSystem connects with NameNode. NameNode initiates a new file creation, and creates a new record in metadata and initiates an output stream of type FSDataOutputStream, which wraps DFSOutputStream and returns it to the client. Before initiating the file creation, NameNode checks if a file already exists and whether the client has permissions to create a new file and if any of the condition is true then an IOException is thrown to the client.
3. The client uses the FSDataOutputStream object to write the data and calls the write() method. The FSDataOutputStream object, which is DFSOutputStream, handles the communication with the DataNodes and NameNode.
4. DFSOutputStream splits files to blocks and coordinates with NameNode to identify the DataNode and the replica DataNodes. The number of the replication factor will be the number of DataNodes identified. Data will be sent to a DataNode in packets, and that DataNode will send the same packet to the second DataNode, the second DataNode will send it to the third, and so on, until the number of DataNodes is identified.
5. When all the packets are received and written, DataNodes send an acknowledgement packet to the sender DataNode, to the client. DFSOutputStream maintains a queue internally to check if the packets are successfully written by DataNode. DFSOutputStream also handles if the acknowledgment is not received or DataNode fails while writing.
6. If all the packets have been successfully written, then the client closes the stream.
7. If the process is completed, then the Distributed FileSystem object notifies the NameNode of the status.

(<a href="#top">Back to top</a>)
<hr>

### HDFS federation
![https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/6688OT_03_06.jpg](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/6688OT_03_06.jpg)

(<a href="#top">Back to top</a>)
<hr>




## NoSQL

### HBase

#### Overview 
* Sparse: HBase is columnar and partition oriented. Usually, a record may have many columns and many of them may have null data, or the values may be repeated. HBase can efficiently and effectively save the space in sparse data.
* Distributed: Data is stored in multiple nodes, scattered across the cluster.
* Persistent: Data is written and saved in the cluster.
* Multidimensional: A row can have multiple versions or timestamps of values.
* Map: Key-Value Pair links the data structure to store the data.
* Sorted: The Key in the structure is stored in a sorted order for faster read and write optimization.

#### Advantages
* Need of real-time random read/write on a high scale
* Variable Schema: columns can be added or removed at runtime
* Many columns of the datasets are sparse
* Key based retrieval and auto sharding is required
* Need of consistency more than availability
* Data or tables have to be denormalized for better performance

#### ACID

* Atomicity: An operation in HBase either completes entirely or not at all for a row, but across nodes it is eventually consistent.
* Durability: An update in HBase will not be lost due to WAL and MemStore.
* Consistency and Isolation HBase is strongly consistent for a single row level but not across levels.

([further reading](http://hbase.apache.org/acid-semantics.html))

(<a href="#top">Back to top</a>)
<hr>

#### Schema design

#### Write Path

![http://image.slidesharecdn.com/storageforbigdata-140207132641-phpapp01/95/storage-systems-for-big-data-hdfs-hbase-and-intro-to-kv-store-redis-36-638.jpg?cb=1391782647](http://image.slidesharecdn.com/storageforbigdata-140207132641-phpapp01/95/storage-systems-for-big-data-hdfs-hbase-and-intro-to-kv-store-redis-36-638.jpg?cb=1391782647)

1. Client requests data to be written in HTable, the request comes to a RegionServer.
2. The RegionServer writes the data first in WAL.
3. The RegionServer identifies the Region which will store the data and the data will be saved in MemStore of that Region.
4. MemStore holds the data in memory and does not persist it. When the threshold value reaches in the MemStore, then the data is flushed as a HFile in that region.


(<a href="#top">Back to top</a>)
<hr>

#### Read Path
![http://image.slidesharecdn.com/dwudevqos0kkksaqhvaj-signature-db258e0cddfb79ee29c1770895f09e97072db8b5ff7ee174f82789933a229c35-poli-140804080932-phpapp01/95/hbase-application-performance-improvement-16-638.jpg?cb=1432894628](http://image.slidesharecdn.com/dwudevqos0kkksaqhvaj-signature-db258e0cddfb79ee29c1770895f09e97072db8b5ff7ee174f82789933a229c35-poli-140804080932-phpapp01/95/hbase-application-performance-improvement-16-638.jpg?cb=1432894628)

1. Client sends a read request. The request is received by the RegionServer which identifies all the Regions where the HFiles are present.
2. First, the MemStore of the Region is queried; if the data is present, then the request is serviced.
3. If the data is not present, the BlockCache is queried to check if it has the data; if yes, the request is serviced.
4. If the data is not present in the BlockCache, then it is pulled from the Region and serviced. Now the data is cached in MemStore and BlockCache..

#### Architecture
![https://www.safaribooksonline.com/library/view/hadoop-the-definitive/9781449398644/httpatomoreillycomsourceoreillyimages684893.png](https://www.safaribooksonline.com/library/view/hadoop-the-definitive/9781449398644/httpatomoreillycomsourceoreillyimages684893.png)
![https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/B03765_05_01.jpg](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/B03765_05_01.jpg)

(<a href="#top">Back to top</a>)
<hr>

#### Regions
![https://www.mapr.com/sites/default/files/blogimages/HBaseArchitecture-Blog-Fig11.png](https://www.mapr.com/sites/default/files/blogimages/HBaseArchitecture-Blog-Fig11.png)

(<a href="#top">Back to top</a>)
<hr>

#### Region server
![https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/B03765_05_02.jpg](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/B03765_05_02.jpg)

(<a href="#top">Back to top</a>)
<hr>

#### Table
![https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/B03765_05_03.jpg](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/B03765_05_03.jpg)

(<a href="#top">Back to top</a>)
<hr>


#### Table splitting
![http://i62.tinypic.com/16h0rdk.jpg](http://i62.tinypic.com/16h0rdk.jpg)

(<a href="#top">Back to top</a>)
<hr>

#### Perfomance tuning

* Compression
* Filters
* Counters
* HBase co-processors

(<a href="#top">Back to top</a>)<hr>

### Cassandra


#### Data nodes
<img src="https://www.safaribooksonline.com/library/view/cassandra-the-definitive/9781491933657/assets/ctdg_0604.png" width="1000px">

(<a href="#top">Back to top</a>)<hr>

#### Read Path
<img src="https://www.safaribooksonline.com/library/view/cassandra-the-definitive/9781491933657/assets/ctdg_0903.png" width="1000px">

##### Within node
<img src="https://www.safaribooksonline.com/library/view/cassandra-the-definitive/9781491933657/assets/ctdg_0904.png" width="1000px">

(<a href="#top">Back to top</a>)<hr>

#### Write Path
<img src="http://4.bp.blogspot.com/-mb-4_3qLkGk/TrG5kOlMGCI/AAAAAAAAAWY/_DEzto-YwOs/s1600/local.png" width="1000px">

<img src="https://www.safaribooksonline.com/library/view/cassandra-the-definitive/9781491933657/assets/ctdg_0901.png" width="1000px">

(<a href="#top">Back to top</a>)<hr>

#### Partitioning and Replication
![http://d42w8nhblerei.cloudfront.net/images/slides/cassandra-1.png](http://d42w8nhblerei.cloudfront.net/images/slides/cassandra-1.png)

(<a href="#top">Back to top</a>)<hr>

#### Hashing / Tokens
![http://d42w8nhblerei.cloudfront.net/images/slides/cassandra-2.png](http://d42w8nhblerei.cloudfront.net/images/slides/cassandra-2.png)

(<a href="#top">Back to top</a>)<hr>

#### Security
<img src="https://www.safaribooksonline.com/library/view/cassandra-the-definitive/9781491933657/assets/ctdg_1301.png" width="1000px">

(<a href="#top">Back to top</a>)<hr>

### Comparisons

#### Cassandra vs HBase vs MongoDB vs Couchbase
<img src="http://www.datastax.com/wp-content/themes/datastax-2014-08/images/nosql/chart-load-process-v3.jpg" width="1000px">

![http://planetcassandra.org/wp-content/uploads/2015/03/Benchmark-Page-6-Insert-Mostly-Workload.png](http://planetcassandra.org/wp-content/uploads/2015/03/Benchmark-Page-6-Insert-Mostly-Workload.png)

(<a href="#top">Back to top</a>)
<hr>

# SQL on hadoop

## Hive
![http://image.slidesharecdn.com/sparkandshark-120620130508-phpapp01/95/spark-and-shark-22-728.jpg?cb=1340197567](http://image.slidesharecdn.com/sparkandshark-120620130508-phpapp01/95/spark-and-shark-22-728.jpg?cb=1340197567)
![http://blog.cloudera.com/wp-content/uploads/2013/07/hiveserver1.png](http://blog.cloudera.com/wp-content/uploads/2013/07/hiveserver1.png)

(<a href="#top">Back to top</a>)
<hr>


## Comparison (Impala, Hive, Spark)
![https://integratc.files.wordpress.com/2015/04/which-hadoop-table-4.jpg](https://integratc.files.wordpress.com/2015/04/which-hadoop-table-4.jpg)

(<a href="#top">Back to top</a>)
<hr>

## Overview
![http://wwwcdn2.actian.com/wp-content/uploads/2014/12/SQL-comparison-chart.jpg](http://wwwcdn2.actian.com/wp-content/uploads/2014/12/SQL-comparison-chart.jpg)

(<a href="#top">Back to top</a>)
<hr>

# Engine

##Batch
### Spark


#### Components
![https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/3765_07_10.jpg](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/3765_07_10.jpg)


#### RDD vs dataframe
<img src="https://databricks.com/wp-content/uploads/2015/02/Screen-Shot-2015-02-16-at-9.46.39-AM.png" width="1000px">

(<a href="#top">Back to top</a>)
<hr>



### MapReduce

#### MapReduce - Job Sumission

![https://www.safaribooksonline.com/library/view/hadoop-the-definitive/9780596521974/httpatomoreillycomsourceoreillyimages300097.png](https://www.safaribooksonline.com/library/view/hadoop-the-definitive/9780596521974/httpatomoreillycomsourceoreillyimages300097.png)

further reading: [here](https://www.google.co.uk/url?sa=i&rct=j&q=&esrc=s&source=imgres&cd=&cad=rja&uact=8&ved=0ahUKEwjauKrMpqfOAhWIDiwKHbahC5MQjhwIBQ&url=https%3A%2F%2Fwww.safaribooksonline.com%2Flibrary%2Fview%2Fhadoop-the-definitive%2F9780596521974%2Fch06.html&psig=AFQjCNE0ZLPAr2Z9x5k8C-hLyKAl6igncQ&ust=1470384324685192).

(<a href="#top">Back to top</a>)
<hr>

![https://www.safaribooksonline.com/library/view/hadoop-in-practice/9781617292224/01fig10_alt.jpg](https://www.safaribooksonline.com/library/view/hadoop-in-practice/9781617292224/01fig10_alt.jpg)

#### Shuffle and Sort
![https://www.safaribooksonline.com/library/view/hadoop-in-practice/9781617292224/01fig07_alt.jpg](https://www.safaribooksonline.com/library/view/hadoop-in-practice/9781617292224/01fig07_alt.jpg)


#### Hadoop 1 vs Hadoop 2
![http://cdn.edureka.co/blog/wp-content/uploads/2014/08/Hadoop1vs2.png](http://cdn.edureka.co/blog/wp-content/uploads/2014/08/Hadoop1vs2.png)

![http://image.slidesharecdn.com/hadooparchitecture-091019175427-phpapp01/95/big-data-analytics-with-hadoop-25-638.jpg?cb=1411551606](http://image.slidesharecdn.com/hadooparchitecture-091019175427-phpapp01/95/big-data-analytics-with-hadoop-25-638.jpg?cb=1411551606)

(<a href="#top">Back to top</a>)
<hr>

### Comparison
![http://1.bp.blogspot.com/-p08vLljU6t0/ViWpJip29KI/AAAAAAAAASc/GSjD2s9Z2K8/s1600/TeraSort3.png](http://1.bp.blogspot.com/-p08vLljU6t0/ViWpJip29KI/AAAAAAAAASc/GSjD2s9Z2K8/s1600/TeraSort3.png)
[source](http://eastcirclek.blogspot.de/2015/06/terasort-for-spark-and-flink-with-range.html)

(<a href="#top">Back to top</a>)
<hr>

## Streaming

### Comparison
![https://databaseline.files.wordpress.com/2016/03/apache-streaming-technologies3.png](https://databaseline.files.wordpress.com/2016/03/apache-streaming-technologies3.png)

(<a href="#top">Back to top</a>)
<hr>




### Storm

#### Physical Architecture
![https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/3765_07_01.jpg](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/3765_07_01.jpg)

* Nimbus: Master process that distributes processing across clusters
* Supervisor: Manages worker nodes
* Worker: Executes tasks assigned by Nimbus
* Zookeeper: Coordinates between Nimbus and Supervisors

(<a href="#top">Back to top</a>)
<hr>

#### Data Architecture
![https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/3765_07_02.jpg](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/3765_07_02.jpg)

* Spout: Produces Stream or data source
* Bolt: Ingests the Spout tuples then processes it and produces output stream; it can be used to filter, aggregate, or join data, or talk to databases
* Topology: A network graph between Spouts and Bolts

![https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/3765_07_03.jpg](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/3765_07_03.jpg)

(<a href="#top">Back to top</a>)
<hr>


# Ingestion

## Overview
![http://image.slidesharecdn.com/hadoopdataingestion-140602114824-phpapp01/95/hadoop-data-ingestion-2-638.jpg?cb=1401709743](http://image.slidesharecdn.com/hadoopdataingestion-140602114824-phpapp01/95/hadoop-data-ingestion-2-638.jpg?cb=1401709743)

(<a href="#top">Back to top</a>)
<hr>


## Flume

### Architecture

![http://cdn.guru99.com/images/Big_Data/061114_1038_Introductio2.png](http://cdn.guru99.com/images/Big_Data/061114_1038_Introductio2.png)

(<a href="#top">Back to top</a>)
<hr>


## Sqoop

![https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/3765_06_03.jpg](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/3765_06_03.jpg)

(<a href="#top">Back to top</a>)
<hr>


## Kafka

### Cluster
![https://camo.githubusercontent.com/37760a9ee91e47c3d0a7ceca0524fd5e1629f333/68747470733a2f2f646c2e64726f70626f782e636f6d2f732f643366796570367870316c6e726b622f6b61666b612d636c75737465722d6f766572766965772e706e67](https://camo.githubusercontent.com/37760a9ee91e47c3d0a7ceca0524fd5e1629f333/68747470733a2f2f646c2e64726f70626f782e636f6d2f732f643366796570367870316c6e726b622f6b61666b612d636c75737465722d6f766572766965772e706e67)

(<a href="#top">Back to top</a>)
<hr>

### Tiered Kafka architecture (across data) 
![https://content.linkedin.com/content/dam/engineering/en-us/blog/migrated/Tier%20Architecture%202.png](https://content.linkedin.com/content/dam/engineering/en-us/blog/migrated/Tier%20Architecture%202.png)

(<a href="#top">Back to top</a>)
<hr>


# Management

## Yarn

### Architecture

![https://s3.amazonaws.com/files.dezyre.com/images/blog/Hadoop_2.0_and_YARN_Advantages_over_Hadoop_1.0_4.png](https://s3.amazonaws.com/files.dezyre.com/images/blog/Hadoop_2.0_and_YARN_Advantages_over_Hadoop_1.0_4.png)

(<a href="#top">Back to top</a>)
<hr>
### Job submission
![https://www.safaribooksonline.com/library/view/hadoop-the-definitive/9781491901687/images/hddg_0701.png](https://www.safaribooksonline.com/library/view/hadoop-the-definitive/9781491901687/images/hddg_0701.png)
![http://www.ibm.com/developerworks/library/bd-yarn-intro/fig04.png](http://www.ibm.com/developerworks/library/bd-yarn-intro/fig04.png)

(<a href="#top">Back to top</a>)
<hr>

## Mesos
![http://mesos.apache.org/assets/img/documentation/architecture3.jpg](http://mesos.apache.org/assets/img/documentation/architecture3.jpg)

(<a href="#top">Back to top</a>)
<hr>

## Ambari

### Architecture
![http://image.slidesharecdn.com/sako-sposetti-june26-1210pm-210c-130709114227-phpapp01/95/managing-your-hadoop-clusters-with-apache-ambari-13-638.jpg?cb=1373370195](http://image.slidesharecdn.com/sako-sposetti-june26-1210pm-210c-130709114227-phpapp01/95/managing-your-hadoop-clusters-with-apache-ambari-13-638.jpg?cb=1373370195)

(<a href="#top">Back to top</a>)
<hr>

### System architecture
![http://image.slidesharecdn.com/ambari-summit-bof-2013-06-25-preso-1-overview-130701185125-phpapp01/95/apache-ambari-bof-overview-hadoop-summit-2013-5-638.jpg?cb=1372704835](http://image.slidesharecdn.com/ambari-summit-bof-2013-06-25-preso-1-overview-130701185125-phpapp01/95/apache-ambari-bof-overview-hadoop-summit-2013-5-638.jpg?cb=1372704835)

(<a href="#top">Back to top</a>)
<hr>

### Metrics collector

![https://cwiki.apache.org/confluence/download/attachments/51812623/ams-arch.jpg?version=1&modificationDate=1430946127000&api=v2](https://cwiki.apache.org/confluence/download/attachments/51812623/ams-arch.jpg?version=1&modificationDate=1430946127000&api=v2)

(<a href="#top">Back to top</a>)
<hr>


## Other

### JMX architecture
<img src="https://www.safaribooksonline.com/library/view/cassandra-the-definitive/9781491933657/assets/ctdg_1001.png" width="1000px">

