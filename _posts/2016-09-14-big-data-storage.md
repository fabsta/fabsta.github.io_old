---
title: "Big Data Concepts Storage"
description: "Overview of Hadoop Tools and Concepts - Storage"
category: BigData
tags: [BigData]
sidebar:
  nav: "new_side"
---



### Table of contents

* TOC
{:toc}


# Storage

## HDFS

### Architecture

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hdfs_architecture.jpg)
[image source](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/6688OT_03_02.jpg)

(<a href="#top">Back to top</a>)
<hr>

### Datanode
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hdfs_datanode.jpg)
[image source](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/6688OT_03_03.jpg)

(<a href="#top">Back to top</a>)
<hr>


### Journalnodes
In order for the Standby node to keep its state synchronized with the Active node, both nodes communicate with a group of separate daemons called "JournalNodes".

* Active node logs namespace modification to majority of JNs.
* Standby node can read edits from JNs and is constantly watching for changes in edit log

### Read Path
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hdfs_read_path.jpg)

[image source](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/6688OT_03_04.jpg)

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

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hdfs_write_path.jpg)

[image source](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/6688OT_03_05.jpg)

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

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hdfs_federation.jpg)

[image source](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/6688OT_03_06.jpg)

(<a href="#top">Back to top</a>)
<hr>

#### Active/passive Namenode

* Active Namenode is the one who is writing edits to JournalNodes. 
* DataNodes know about location of both Namenodes, they send block location information and heartbeats to both. 
* Passive Namenode performs checkpoints (of namespace state), no Secondary NameNode required.

(<a href="#top">Back to top</a>)
<hr>

#### High availability

In general, there are two approaches

* Shared Storage using NFS
* Quorum-based Storage

##### Shared Storage using NFS

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/shared-edit-log1.png)

[image source](https://hadoopabcd.files.wordpress.com/2015/02/shared-edit-log1.png?w=512&h=304)

(<a href="#top">Back to top</a>)
<hr>

##### Quorum-based Storage

![{{base}}/images/lambda_architecture.png]({{base}}/images/quorum-journal-without-zk.png)

[image source](https://hadoopabcd.files.wordpress.com/2015/02/quorum-journal-without-zk.png?w=663&h=338)

adds two new components to HDFS deployment
* Zookeeper quorum
* ZKFailoverController (ZKFC)

Automatic failover relies on Zookeeper:

* Each Namenode maintains persistent session in Zookeeper
* If machine crashes, session expires
* Other Namenode is notified to take over

ZKFC is responsible for:

* ZKFC pings its local Namenode. If unresponsive, ZKFC marks it as unhealthy.


(<a href="#top">Back to top</a>)
<hr>




## NoSQL

### Concepts

#### Row- vs. column-oriented
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/row_column_oriented.png)

[image source](http://1.bp.blogspot.com/_j6mB7TMmJJY/TK1npAatLqI/AAAAAAAAAd4/TscPInSeUoo/s1600/p1.png)

(<a href="#top">Back to top</a>)
<hr>

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
* Variable Schema: columns can be added or removed at runtime (schema-on-read)
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

##### Sparse 
“Sparse” means that for any given row you can have one or more columns, but each row doesn’t need to have all the same columns as other rows like it (as in a relational model)

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hbase_data_model.png)

[image source](http://www.ymc.ch/wp-content/uploads/2014/02/HBase-Data-Model.png)

(<a href="#top">Back to top</a>)
<hr>

#### Write Path
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hbase_write_path.jpg)

[image source](http://image.slidesharecdn.com/storageforbigdata-140207132641-phpapp01/95/storage-systems-for-big-data-hdfs-hbase-and-intro-to-kv-store-redis-36-638.jpg?cb=1391782647)

1. Client requests data to be written in HTable, the request comes to a RegionServer.
2. The RegionServer writes the data first in WAL.
3. The RegionServer identifies the Region which will store the data and the data will be saved in MemStore of that Region.
4. MemStore holds the data in memory and does not persist it. When the threshold value reaches in the MemStore, then the data is flushed as a HFile in that region.


(<a href="#top">Back to top</a>)
<hr>

#### Read Path
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hbase_read_path.jpg)

[image source](http://image.slidesharecdn.com/dwudevqos0kkksaqhvaj-signature-db258e0cddfb79ee29c1770895f09e97072db8b5ff7ee174f82789933a229c35-poli-140804080932-phpapp01/95/hbase-application-performance-improvement-16-638.jpg?cb=1432894628)

1. Client sends a read request. The request is received by the RegionServer which identifies all the Regions where the HFiles are present.
2. First, the MemStore of the Region is queried; if the data is present, then the request is serviced.
3. If the data is not present, the BlockCache is queried to check if it has the data; if yes, the request is serviced.
4. If the data is not present in the BlockCache, then it is pulled from the Region and serviced. Now the data is cached in MemStore and BlockCache..

#### Architecture
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hbase_architecture.png)

[image source](https://www.safaribooksonline.com/library/view/hadoop-the-definitive/9781449398644/httpatomoreillycomsourceoreillyimages684893.png)

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hbase_architecture2.png)

[image source](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/B03765_05_01.jpg)

![{{base}}/images/bigdata/hbase_architecture_complex.png]({{base}}/images/bigdata/hbase_architecture_complex.png)

[image source](https://bighadoop.files.wordpress.com/2014/05/hbase-architecture.png)



(<a href="#top">Back to top</a>)
<hr>

#### Table
An HBase table comprises a set of metadata information and a set of key/value pairs:

* Table Info: A manifest file that describes the table “settings”, like column families, compression and encoding codecs, bloom filter types, and so on.
* Regions: The table “partitions” are called regions. Each region is responsible for handling a contiguous set of key/values, and they are defined by a start key and end key.
* WALs/MemStore: Before writing data on disk, puts are written to the Write Ahead Log (WAL) and then stored in-memory until memory pressure triggers a flush to disk. The WAL provides an easy way to recover puts not flushed to disk on failure.
* HFiles: At some point all the data is flushed to disk; an HFile is the HBase format that contains the stored key/values. HFiles are immutable but can be deleted on compaction or region deletion.

[source](http://blog.cloudera.com/blog/2013/03/introduction-to-apache-hbase-snapshots/)

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hbase_table.jpg)

[image source](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/B03765_05_03.jpg)

(<a href="#top">Back to top</a>)
<hr>



#### Regions
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hbase_regions.png)

[image source](https://www.mapr.com/sites/default/files/blogimages/HBaseArchitecture-Blog-Fig11.png)

(<a href="#top">Back to top</a>)
<hr>

#### Region server
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hbase_region_server.jpg)

[image source](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/B03765_05_02.jpg)

![{{base}}/images/bigdata/hbase_table_regionServer.jpg]({{base}}/images/bigdata/hbase_table_regionServer.jpg)

[image source](http://image.slidesharecdn.com/larsgeorge-hw2011-adv-hbase-schema-111110131141-phpapp01/95/hadoop-world-2011-advanced-hbase-schema-design-8-728.jpg?cb=1320931550)

(<a href="#top">Back to top</a>)
<hr>


#### Region splitting

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hbase_table_splitting.jpg)

[image source](http://i62.tinypic.com/16h0rdk.jpg)

(<a href="#top">Back to top</a>)
<hr>

#### Region splitting process

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hbase_region_splitting.jpg)

[image source](http://hortonworks.com/wp-content/uploads/2013/02/hbase.jpg)


1. RegionServer decides locally to split the region, and prepares the split. As a first step, it creates a znode in zookeeper under /hbase/region-in-transition/region-name in SPLITTING state.
2. The Master learns about this znode, since it has a watcher for the parent region-in-transition znode.
3. RegionServer creates a sub-directory named “.splits” under the parent’s region directory in HDFS.
4. RegionServer closes the parent region, forces a flush of the cache and marks the region as offline in its local data structures. At this point, client requests coming to the parent region will throw NotServingRegionException. The client will retry with some backoff.
5. RegionServer create the region directories under .splits directory, for daughter regions A and B, and creates necessary data structures. Then it splits the store files, in the sense that it creates two Reference files per store file in the parent region. Those reference files will point to the parent regions files.
6. RegionServer creates the actual region directory in HDFS, and moves the reference files for each daughter.
7. RegionServer sends a Put request to the .META. table, and sets the parent as offline in the .META. table and adds information about daughter regions. At this point, there won’t be individual entries in .META. for the daughters. Clients will see the parent region is split if they scan .META., but won’t know about the daughters until they appear in .META.. Also, if this Put to .META. succeeds, the parent will be effectively split. If the RegionServer fails before this RPC succeeds, Master and the next region server opening the region will clean dirty state about the region split. After the .META. update, though, the region split will be rolled-forward by Master.
8. RegionServer opens daughters in parallel to accept writes.
9. RegionServer adds the daughters A and B to .META. together with information that it hosts the regions. After this point, clients can discover the new regions, and issue requests to the new region. Clients cache the .META. entries locally, but when they make requests to the region server or .META., their caches will be invalidated, and they will learn about the new regions from .META..
10. RegionServer updates znode /hbase/region-in-transition/region-name in zookeeper to state SPLIT, so that the master can learn about it. The balancer can freely re-assign the daughter regions to other region servers if it chooses so.
11. After the split, meta and HDFS will still contain references to the parent region. Those references will be removed when compactions in daughter regions rewrite the data files. Garbage collection tasks in the master periodically checks whether the daughter regions still refer to parents files.  If not, the parent region will be removed.

[source](http://hortonworks.com/blog/apache-hbase-region-splitting-and-merging/)

(<a href="#top">Back to top</a>)
<hr>

#### Perfomance tuning

* Compression
* Filters
* Counters
* HBase co-processors

(<a href="#top">Back to top</a>)
<hr>


#### Snapshots
A snapshot is a set of metadata information that allows an admin to get back to a previous state of the table. A snapshot is not a copy of the table; it’s just a list of file names and doesn’t copy the data. A full snapshot restore means that you get back to the previous “table schema” and you get back your previous data losing any changes made since the snapshot was taken

* Recovery from user/application errors
* Restore/Recover from a known safe state.
* View previous snapshots and selectively merge the difference into production.
* Save a snapshot right before a major application upgrade or change.
* Auditing and/or reporting on views of data at specific time
* Capture monthly data for compliance purposes.
* Run end-of-day/month/quarter reports.
* Application testing
* Test schema or application changes on data similar to that in production from a snapshot and then throw it away. For example: take a snapshot, create a new table from the snapshot content (schema plus data), and manipulate the new table by changing the schema, adding and removing rows, and so on. (The original table, the snapshot, and the new table remain mutually independent.)
* Offloading of work
* Take a snapshot, export it to another cluster, and run your MapReduce jobs. Since the export snapshot operates at HDFS level, you don’t slow down your main HBase cluster as much as CopyTable does.

[source](http://blog.cloudera.com/blog/2013/03/introduction-to-apache-hbase-snapshots/)

![{{base}}/images/bigdata/hbase_commit_snapshot.png]({{base}}/images/bigdata/hbase_commit_snapshot.png)

[image source](http://blog.cloudera.com/wp-content/uploads/2013/06/matteo2.png)


### Phoenix
Apache Phoenix enables OLTP and operational analytics in Hadoop for low latency applications by combining the best of both worlds:

* The power of standard SQL and JDBC APIs with full ACID transaction capabilities 

* The flexibility of late-bound, schema-on-read capabilities from the NoSQL world by leveraging HBase as its backing store

Apache Phoenix is fully integrated with other Hadoop products such as Spark, Hive, Pig, Flume, and Map Reduce.

#### where it fits in
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/phoenix_fits_in.png)

[image source](https://www.safaribooksonline.com/library/view/cassandra-the-definitive/9781491933657/assets/ctdg_0604.png)

#### Architecture
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/phoenix_fits_in.png)

[image source](https://www.safaribooksonline.com/library/view/cassandra-the-definitive/9781491933657/assets/ctdg_0604.png)

(<a href="#top">Back to top</a>)
<hr>

### Cassandra


#### Data nodes
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/cassandra_data_nodes.png)

[image source](https://www.safaribooksonline.com/library/view/cassandra-the-definitive/9781491933657/assets/ctdg_0604.png)

(<a href="#top">Back to top</a>)<hr>

#### Read Path

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/cassandra_read_path.png)

[image source](https://www.safaribooksonline.com/library/view/cassandra-the-definitive/9781491933657/assets/ctdg_0903.png)

##### Within node

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/cassandra_within_node.png)

[image source](https://www.safaribooksonline.com/library/view/cassandra-the-definitive/9781491933657/assets/ctdg_0904.png)

(<a href="#top">Back to top</a>)<hr>

#### Write Path

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/cassandra_write_path.png)

[image source](http://4.bp.blogspot.com/-mb-4_3qLkGk/TrG5kOlMGCI/AAAAAAAAAWY/_DEzto-YwOs/s1600/local.png)


![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/cassandra_write_path2.png)

[image source](https://www.safaribooksonline.com/library/view/cassandra-the-definitive/9781491933657/assets/ctdg_0901.png)

(<a href="#top">Back to top</a>)<hr>

#### Partitioning and Replication
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/cassandra_partitioning.png)

[image source](http://d42w8nhblerei.cloudfront.net/images/slides/cassandra-1.png)

(<a href="#top">Back to top</a>)<hr>

#### Hashing / Tokens

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/cassandra_hashing.png)

[image source](http://d42w8nhblerei.cloudfront.net/images/slides/cassandra-2.png)

(<a href="#top">Back to top</a>)<hr>

#### Security
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/cassandra_security.png)
[image source](https://www.safaribooksonline.com/library/view/cassandra-the-definitive/9781491933657/assets/ctdg_1301.png)


(<a href="#top">Back to top</a>)<hr>

### Graph databases

#### Titan

##### Architecture
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/titan_architecture.png)

[image source](https://i.kinja-img.com/gawker-media/image/upload/s--Pe8w2MVb--/c_scale,fl_progressive,q_80,w_800/x5plwhjhgwaahld8or9v.png)


```
<dependency>
   <groupId>com.thinkaurelius.titan</groupId>
   <artifactId>titan-core</artifactId>
   <version>1.0.0</version>
</dependency>
<!-- core, all, cassandra, hbase, berkeleyje, es, lucene -->
```

```
// who is hercules' grandfather?
g.V.has('name','hercules').out('father').out('father').name
```

#### Tinkerpop
The goal of TinkerPop, as a Graph Computing Framework, is to make it easy for developers to create graph applications by providing APIs and tools that simplify their endeavors.

##### Architecture
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/tinkerpop_architecture.png)
[image source](http://tinkerpop.apache.org/docs/current/images/provider-integration.png)


##### Graph landscape

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/tinkerpop_graph_landscape.png)
[image source](http://image.slidesharecdn.com/graphprocessingwithapachetinkerpop-160512003044/95/graph-processing-with-apache-tinkerpop-9-638.jpg?cb=1463410962)

(<a href="#top">Back to top</a>)
<hr>


##### Getting started - Example graph

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/tinkerpop_getting_started.jpg)
[image source](http://image.slidesharecdn.com/graphprocessingwithapachetinkerpop-160512003044/95/graph-processing-with-apache-tinkerpop-9-638.jpg?cb=1463410962)

[Gremlin get started](http://tinkerpop.apache.org/docs/current/tutorials/getting-started/)

(<a href="#top">Back to top</a>)
<hr>

### Comparisons

#### Cassandra vs HBase vs MongoDB vs Couchbase

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/cassandra_comparison.jpg)

[image source](http://www.datastax.com/wp-content/themes/datastax-2014-08/images/nosql/chart-load-process-v3.jpg)

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/cassandra_comparison3.png)

[image source](http://planetcassandra.org/wp-content/uploads/2015/03/Benchmark-Page-6-Insert-Mostly-Workload.png)

(<a href="#top">Back to top</a>)
<hr>


##### Update
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/cassandra_comparison_update.jpg)

[image source](http://jaxenter.com/wp-content/uploads/2014/02/sergey-3.jpg)

(<a href="#top">Back to top</a>)
<hr>

##### Cap Continuum
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/cap_continuum.png)

[image source](https://www.safaribooksonline.com/library/view/cassandra-the-definitive/9781449399764/httpatomoreillycomsourceoreillyimages715809.png)

In this depiction, relational databases are on the line between Consistency and Availability, which means that they can fail in the event of a network failure (including a cable breaking). This is typically achieved by defining a single master server, which could itself go down, or an array of servers that simply don’t have sufficient mechanisms built in to continue functioning in the case of network partitions.

Graph databases such as Neo4J and the set of databases derived at least in part from the design of Google’s Bigtable database (such as MongoDB, HBase, Hypertable, and Redis) all are focused slightly less on Availability and more on ensuring Consistency and Partition Tolerance.

Finally, the databases derived from Amazon’s Dynamo design include Cassandra, Project Voldemort, CouchDB, and Riak. These are more focused on Availability and Partition-Tolerance.

(<a href="#top">Back to top</a>)
<hr>

# SQL on hadoop

## BigSQL

### Architecture
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/bigsql_architecture.gif)
[image source](https://www.ibm.com/support/knowledgecenter/SSERCR_1.0.0/com.ibm.swg.im.infosphere.biginsights.analyze.doc/images/bigSQL%20tech%20overview.gif)

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/bigsql_architecture2.jpg)
[image source](http://www.ibmbigdatahub.com/sites/default/files/public_images/Slide1.JPG)



## Hive

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hive_architecture.jpg)
[image source](http://image.slidesharecdn.com/sparkandshark-120620130508-phpapp01/95/spark-and-shark-22-728.jpg?cb=1340197567)

![{{base}}/images/]({{base}}/images/bigdata/hive_architecture2.jpg)
[image source](http://images.slideplayer.com/24/7523812/slides/slide_5.jpg)

![]()
(<a href="#top">Back to top</a>)
<hr>

## Tez
Apache Tez is part of the Stinger initiative.
Tez generalizes the MapReduce paradigm to a more powerful framework based on expressing computations as a dataflow graph. Tez exists to address some of the limitations of MapReduce. For example, in a typical MapReduce, a lot of temporary data is stored (such as each mapper's output, which is a disk I/O), which is an overhead. In the case of Tez, this disk I/O of temporary data is saved, thereby resulting in higher performance compared to the MapReduce model.

Tez is a framework for purpose-built tools such as Hive and Pig.

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/tez_idea2.jpg)
[image source](https://www.safaribooksonline.com/library/view/yarn-essentials/9781784391737/graphics/1737OS_07_27.jpg)

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/tez_idea.jpg)
[image source](http://image.slidesharecdn.com/w-235p-hall1-pandey-140617161536-phpapp01/95/hive-tez-a-performance-deep-dive-9-638.jpg?cb=1403021822)


![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/tez_idea3.jpg)
[image source](http://image.slidesharecdn.com/sparkorhadoop-isitaneither-orproposition-slimbaltagi-150313094837-conversion-gate01/95/spark-or-hadoop-is-it-an-eitheror-proposition-by-slim-baltagi-29-638.jpg?cb=1426240274)


### Tez vs Spark

[Tez vs Spark](https://www.xplenty.com/blog/2015/01/apache-spark-vs-tez-comparison/)
[Flink on Tez](https://ci.apache.org/projects/flink/flink-docs-release-0.9/setup/flink_on_tez.html)

### Hive with LLAP (Live Long and Process)
With 2.1 Hive  introduces LLAP, a daemon layer for sub-second queries. LLAP combines persistent query servers and optimized in-memory caching that allows Hive to launch queries instantly and avoids unnecessary disk I/O. For more information see [http://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/](http://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/tez_llap.png)
[image source](http://hortonworks.com/wp-content/uploads/2016/07/Hive-2.1-blog-MR-vs-Tez-vs-LLAP.png)


### MapReduce vs Tez vs Tez LLAP
Tez LLAP process compared to Tez execution process and MapReduce process
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/llap_architecture.png)
[image source](http://hortonworks.com/wp-content/uploads/2016/07/Hive-2.1-blog-LLAP-Architecture.png)





## Comparison 

### Impala, Hive, Stinger, Pivotal, Teradata, Presto
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/nosql_comparison.jpg)
[image source](http://image.slidesharecdn.com/bigsqlcompetitivesummary2014-aug-20-140820132237-phpapp01/95/big-sql-competitive-summary-vendor-landscape-8-638.jpg?cb=1408971625)

(<a href="#top">Back to top</a>)
<hr>


### Benchmark: Impala, Hive, Spark
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/nosql_comparison2.jpg)
[source](https://integratc.files.wordpress.com/2015/04/which-hadoop-table-4.jpg)

(<a href="#top">Back to top</a>)
<hr>


### Benchmark: Impala, Hive-on-Tez
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/impala_vs_hize_on_tez.png)
[source](http://hortonworks.com/wp-content/uploads/2015/09/fig2_impala_vs_hive.png)


(<a href="#top">Back to top</a>)
<hr>

## Overview
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/nosql_overview.jpg)

[image source](http://wwwcdn2.actian.com/wp-content/uploads/2014/12/SQL-comparison-chart.jpg)

(<a href="#top">Back to top</a>)
<hr>
