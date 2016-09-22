---
title: "Big Data Concepts"
description: "Overview of Hadoop Tools and Concepts"
category: BigData
tags: [BigData]
sidebar:
  nav: "new_side"
---



### Table of contents

* TOC
{:toc}


# General

## Lambda architecture

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/lambda_architecture.png)
[image source](https://lh3.googleusercontent.com/sWNk04rO-YJZP9Hm5tP6Nx-_NTVV0x_0iX8liBFB3M3HKm75-Yvy7r5-o_1HelRrgKRRIQedTXtZ_S7zzZkoZ2USdtx8f6TRZchmbrQAg_BdU5BhL5JT9d5iQhfIbQ4qow)

(<a href="#top">Back to top</a>)
<hr>


# Distributions

## Mapr
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/mapr_distribution.png)
[image source](http://images.slideplayer.com/15/4706189/slides/slide_4.jpg)

(<a href="#top">Back to top</a>)
<hr>

## Cloudera
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/cloudera_distribution.png)
[image source](http://www.techweekly.com/viewpoints/wp-content/uploads/2013/06/Cloudera-hadoop-02.png)

(<a href="#top">Back to top</a>)<hr>

## Hortonworks
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hortonworks_distribution.png)
[image source](http://hortonworks.com/wp-content/uploads/2016/03/asparagus-chart-hdp24.png)

(<a href="#top">Back to top</a>)
<hr>


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

# Engine

## Batch

### Spark


#### Components
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/spark_components.jpg)

[image source](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/3765_07_10.jpg)

#### History server
The Spark History Server displays information about the history of completed Spark applications. It displays information about:

* A list of scheduler stages and tasks
* A summary of RDD sizes and memory usage
* Environmental information.
* Information about the running executors

[source](http://spark.apache.org/docs/latest/monitoring.html)

Extension to history server: [spree](http://www.hammerlab.org/2015/07/25/spree-58-a-live-updating-web-ui-for-spark/)

![{{base}}/images/bigdata/spree_intro.gif]({{base}}/images/bigdata/spree_intro.gif)
[image source](http://www.hammerlab.org/images/spree/intro3.gif)

#### Thrift server
Spark Thrift Server provides JDBC/ODBC access to a Spark cluster and is used to service Spark SQL queries. Tools like Power BI, Tableau etc. use ODBC protocol to communicate with Spark Thrift Server to execute Spark SQL queries as a Spark Application. When a Spark cluster is created, two instances of the Spark Thrift Server are started, one on each head node. Each Spark Thrift Server is visible as a Spark application in the YARN UI.


#### RDD vs dataframe
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/spark_rdd_dataframe.png)
[image source]({{base}}/images/bigdata/spark_components.jpg)

(<a href="#top">Back to top</a>)
<hr>



### MapReduce

#### MapReduce - Job Sumission
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/mapreduce_job_submission.png)

[image source](https://www.safaribooksonline.com/library/view/hadoop-the-definitive/9780596521974/httpatomoreillycomsourceoreillyimages300097.png)

further reading: [here](https://www.google.co.uk/url?sa=i&rct=j&q=&esrc=s&source=imgres&cd=&cad=rja&uact=8&ved=0ahUKEwjauKrMpqfOAhWIDiwKHbahC5MQjhwIBQ&url=https%3A%2F%2Fwww.safaribooksonline.com%2Flibrary%2Fview%2Fhadoop-the-definitive%2F9780596521974%2Fch06.html&psig=AFQjCNE0ZLPAr2Z9x5k8C-hLyKAl6igncQ&ust=1470384324685192).

(<a href="#top">Back to top</a>)
<hr>

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/mapreduce_job_submission2.jpg)

[image source](https://www.safaribooksonline.com/library/view/hadoop-in-practice/9781617292224/01fig10_alt.jpg)

#### Shuffle and Sort
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/mapreduce_shuffle_sort.jpg)
[image source](https://www.safaribooksonline.com/library/view/hadoop-in-practice/9781617292224/01fig07_alt.jpg)


#### Hadoop 1 vs Hadoop 2
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/mapreduce1_2.jpg)

[image source](http://cdn.edureka.co/blog/wp-content/uploads/2014/08/Hadoop1vs2.png)


![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/mapreduce1_2_2.jpg)

[image source](http://image.slidesharecdn.com/hadooparchitecture-091019175427-phpapp01/95/big-data-analytics-with-hadoop-25-638.jpg?cb=1411551606)

(<a href="#top">Back to top</a>)
<hr>

### Comparison
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/engine_comparison.png)

[image source](http://1.bp.blogspot.com/-p08vLljU6t0/ViWpJip29KI/AAAAAAAAASc/GSjD2s9Z2K8/s1600/TeraSort3.png)
[source](http://eastcirclek.blogspot.de/2015/06/terasort-for-spark-and-flink-with-range.html)

(<a href="#top">Back to top</a>)
<hr>

## Streaming


### Overview
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/streaming_overview.png)
[image source](http://blogs.teradata.com/international/wp-content/uploads/2016/08/evolution-of-streaming-tehnologies-3.png)



### Storm


#### History


![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/storm_history.gif)

[image source](http://hortonworks.com/wp-content/uploads/2016/05/History-of-Apache-Storm_Hortonworks-2016-1024x1001.gif)

#### Physical Architecture
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/storm_physical_architecture.jpg)

[image source](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/3765_07_01.jpg)

* Nimbus: Master process that distributes processing across clusters
* Supervisor: Manages worker nodes
* Worker: Executes tasks assigned by Nimbus
* Zookeeper: Coordinates between Nimbus and Supervisors

(<a href="#top">Back to top</a>)
<hr>

#### Data Architecture
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/storm_data_architecture.jpg)

[image source](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/3765_07_02.jpg)

* Spout: Produces Stream or data source
* Bolt: Ingests the Spout tuples then processes it and produces output stream; it can be used to filter, aggregate, or join data, or talk to databases
* Topology: A network graph between Spouts and Bolts

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/strom_topology.jpg)

[image source](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/3765_07_03.jpg)

(<a href="#top">Back to top</a>)
<hr>


### Kafka streams

(<a href="#top">Back to top</a>)
<hr>

### Akka

(<a href="#top">Back to top</a>)
<hr>

### Comparison
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/streaming_comparison.png)

[image source](https://databaseline.files.wordpress.com/2016/03/apache-streaming-technologies3.png)


<img src="https://databaseline.files.wordpress.com/2016/03/apache-streaming-technologies3.png" width="1000px">

(<a href="#top">Back to top</a>)
<hr>




# Ingestion

## Overview
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/ingestion.jpg)

[image source](http://image.slidesharecdn.com/hadoopdataingestion-140602114824-phpapp01/95/hadoop-data-ingestion-2-638.jpg?cb=1401709743)

(<a href="#top">Back to top</a>)
<hr>


## Flume

### Architecture

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/flume_architecture.png)

[image source](http://cdn.guru99.com/images/Big_Data/061114_1038_Introductio2.png)

(<a href="#top">Back to top</a>)
<hr>


## Sqoop

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/sqoop.jpg)

[image source](https://www.safaribooksonline.com/library/view/hadoop-essentials/9781784396688/graphics/3765_06_03.jpg)

(<a href="#top">Back to top</a>)
<hr>


## Kafka

### Cluster
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/kafka_cluster.png)

[image source](https://camo.githubusercontent.com/37760a9ee91e47c3d0a7ceca0524fd5e1629f333/68747470733a2f2f646c2e64726f70626f782e636f6d2f732f643366796570367870316c6e726b622f6b61666b612d636c75737465722d6f766572766965772e706e67)

Overview of our Kafka setup including the current state of the partitions and replicas. The colored boxes represent replicas of partitions. “P0 R1” denotes the replica with ID 1 for partition 0. A bold box frame means that the corresponding broker is the leader for the given partition ([source](http://www.michael-noll.com/blog/2013/03/13/running-a-multi-broker-apache-kafka-cluster-on-a-single-node/)).

(<a href="#top">Back to top</a>)
<hr>


### Relationships between topics, partitions, and replicas
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/kafka_relationships_topics_replicas.png)
[image source](http://www.michael-noll.com/blog/uploads/kafka-topics-partitions-replicas.png)


### Partition offset
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/kafka_partition_offset.jpg)
[image source](http://image.slidesharecdn.com/kafka101training-public-v2-140818033637-phpapp01/95/apache-kafka-08-basic-training-verisign-28-638.jpg?cb=1439479643)



### Tiered Kafka architecture (across data) 
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/kafka_tier_architecture.png)

[image source](https://content.linkedin.com/content/dam/engineering/en-us/blog/migrated/Tier%20Architecture%202.png)

(<a href="#top">Back to top</a>)
<hr>

[multi-broker cluster in single node](http://www.michael-noll.com/blog/2013/03/13/running-a-multi-broker-apache-kafka-cluster-on-a-single-node/)


# Management

## Yarn

### Architecture

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/yarn_architecture.png)

[image source](https://s3.amazonaws.com/files.dezyre.com/images/blog/Hadoop_2.0_and_YARN_Advantages_over_Hadoop_1.0_4.png)

(<a href="#top">Back to top</a>)
<hr>

#### Resource Manager


#### ResourceManager HA

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/yarn_rm_ha.png)

[image source](https://s3.amazonaws.com/files.dezyre.com/images/blog/Hadoop_2.0_and_YARN_Advantages_over_Hadoop_1.0_4.png)

##### Manual transitions and failover

When automatic failover is not enabled, admins have to manually transition one of the RMs to Active. To failover from one RM to the other, they are expected to first transition the Active-RM to Standby and transition a Standby-RM to Active. All this can be done using the “yarn rmadmin” CLI.

##### Automatic failover

The RMs have an option to embed the Zookeeper-based ActiveStandbyElector to decide which RM should be the Active. When the Active goes down or becomes unresponsive, another RM is automatically elected to be the Active which then takes over. Note that, there is no need to run a separate ZKFC daemon as is the case for HDFS because ActiveStandbyElector embedded in RMs acts as a failure detector and a leader elector instead of a separate ZKFC daemon.

[source](https://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/ResourceManagerHA.html)

### Job submission

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/yarn_job_submission.png)
[image source](https://www.safaribooksonline.com/library/view/hadoop-the-definitive/9781491901687/images/hddg_0701.png)

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/yarn_job_submission2.png)
[image source](http://www.ibm.com/developerworks/library/bd-yarn-intro/fig04.png)

(<a href="#top">Back to top</a>)
<hr>

## Slider


## Mesos

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/mesos_architecture.jpg)

[image source](http://mesos.apache.org/assets/img/documentation/architecture3.jpg)

(<a href="#top">Back to top</a>)
<hr>

### Myriad - Yarn and Mesos together

Deploy Yarn applications using Mesos
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/myriad_how_works.png)
[image source](https://dmgpayxepw99m.cloudfront.net/how-it-works-5a9c93e73031b0fc13ef20061f039a69.png)



(<a href="#top">Back to top</a>)
<hr>

## Yarn vs Mesos
Mesos: Manage data center
Yarn: Manage hadoop jobs

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/yarn_mesos.jpg)
[image source](http://image.slidesharecdn.com/mesosvs-160511175623/95/mesos-vs-yarn-an-overview-6-638.jpg?cb=1462989584)


## Aurora
 
Apache Aurora is a service scheduler that runs on top of Apache Mesos, enabling you to run long-running services, cron jobs, and ad-hoc jobs that take advantage of Apache Mesos’ scalability, fault-tolerance, and resource isolation.

(<a href="#top">Back to top</a>)
<hr>

### Components
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/arurora_components.png)
[image source](http://aurora.apache.org/documentation/latest/images/components.png)


* __Aurora scheduler__ The scheduler is your primary interface to the work you run in your cluster. You will instruct it to run jobs, and it will manage them in Mesos for you. You will also frequently use the scheduler’s read-only web interface as a heads-up display for what’s running in your cluster.

* __Aurora client__ The client (aurora command) is a command line tool that exposes primitives that you can use to interact with the scheduler. The client operates on

Aurora also provides an admin client (aurora_admin command) that contains commands built for cluster administrators. You can use this tool to do things like manage user quotas and manage graceful maintenance on machines in cluster.

* __Aurora executor__ The executor (a.k.a. Thermos executor) is responsible for carrying out the workloads described in the Aurora DSL (.aurora files). The executor is what actually executes user processes. It will also perform health checking of tasks and register tasks in ZooKeeper for the purposes of dynamic service discovery.

* __Aurora observer__ The observer provides browser-based access to the status of individual tasks executing on worker machines. It gives insight into the processes executing, and facilitates browsing of task sandbox directories.

* __ZooKeeper__ ZooKeeper is a distributed consensus system. In an Aurora cluster it is used for reliable election of the leading Aurora scheduler and Mesos master. It is also used as a vehicle for service discovery, see Service Discovery

* __Mesos master__ The master is responsible for tracking worker machines and performing accounting of their resources. The scheduler interfaces with the master to control the cluster.

* __Mesos agent__ The agent receives work assigned by the scheduler and executes them. It interfaces with Linux isolation systems like cgroups, namespaces and Docker to manage the resource consumption of tasks. When a user task is launched, the agent will launch the executor (in the context of a Linux cgroup or Docker container depending upon the environment), which will in turn fork user processes.

(<a href="#top">Back to top</a>)
<hr>


### Jobs, tasks, and processes

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/aurora_jobs.png)
[image source](http://aurora.apache.org/documentation/latest/images/aurora_hierarchy.png)

(<a href="#top">Back to top</a>)
<hr>

## Ambari

### Architecture

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/ambari_architecture.jpg)

[image source](http://image.slidesharecdn.com/sako-sposetti-june26-1210pm-210c-130709114227-phpapp01/95/managing-your-hadoop-clusters-with-apache-ambari-13-638.jpg?cb=1373370195)

(<a href="#top">Back to top</a>)
<hr>

### System architecture

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/ambari_system_architecture.jpg)

[image source](http://image.slidesharecdn.com/ambari-summit-bof-2013-06-25-preso-1-overview-130701185125-phpapp01/95/apache-ambari-bof-overview-hadoop-summit-2013-5-638.jpg?cb=1372704835)

(<a href="#top">Back to top</a>)
<hr>

### Metrics collector

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/ambari_metrics_collector.jpg)

[image source](https://cwiki.apache.org/confluence/download/attachments/51812623/ams-arch.jpg?version=1&modificationDate=1430946127000&api=v2)

(<a href="#top">Back to top</a>)
<hr>

## Atlas

### Requirements
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/atlas_requirements.png)

[image source](http://hortonworks.com/wp-content/uploads/2015/04/atlas_1.png)

### Architecture
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/atlas_architecture.png)
[image source](http://hortonworks.com/wp-content/uploads/2015/04/atlas_2.png)

### Type definitions

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/atlas_type_definitions.png)
[image source](http://atlas.incubator.apache.org/images/twiki/guide-class-diagram.png)


### Deep dive

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/atlas_deepdive.jpg)

[image source](http://image.slidesharecdn.com/tareq-151227094907/95/josa-techtalk-metadata-managementin-big-data-19-638.jpg?cb=1451210220)

(<a href="#top">Back to top</a>)
<hr>

## Marmotta
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/marmotta.png)

[image source](http://marmotta.apache.org/images/architecture-big.png)

(<a href="#top">Back to top</a>)
<hr>


## Zookeeper

Apache ZooKeeper is a distributed, fault tolerant, highly available system for managing configuration information, naming, and more (distributed synchronization, anyone?).

ZooKeeper appears like a filesystem to clients, it is a hierarchy of znodes, which are analogous to directories or files, both of which can contain a small amount of data.

ZooKeeper can be used to store Thrift service location information.

(<a href="#top">Back to top</a>)
<hr>

### How writes are handled

The master is the authority for writes: in this way writes can be guaranteed to be persisted in-order, i.e., writes are linear. Each time a client writes to the ensemble, a majority of nodes persist the information: these nodes include the server for the client, and obviously the master. This means that each write makes the server up-to-date with the master. It also means, however, that you cannot have concurrent writes.

The guarantee of linear writes is the reason for the fact that ZooKeeper does not perform well for write-dominant workloads. In particular, it should not be used for interchange of large data, such as media. As long as your communication involves shared data, ZooKeeper helps you. When data could be written concurrently, ZooKeeper actually gets in the way, because it imposes a strict ordering of operations even if not strictly necessary from the perspective of the writers. Its ideal use is for coordination, where messages are exchanged between the clients.

### How reads are handled

This is where ZooKeeper excels: reads are concurrent since they are served by the specific server that the client connects to. However, this is also the reason for the eventual consistency: the "view" of a client may be outdated, since the master updates the corresponding server with a bounded but undefined delay.

[source](http://stackoverflow.com/questions/3662995/explaining-apache-zookeeper)

### Data model

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/zookeeper_data_model.jpg)

[image source](http://image.slidesharecdn.com/zookeeperinthewild-rakesh-150604085733-lva1-app6892/95/zoo-keeper-in-the-wild-6-638.jpg?cb=1433408334)


### Leader selection

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/zookeeper_master_and_slave.png)

[image source](http://www.ebaytechblog.com/wp-content/uploads/2012/09/master_and_slave.png)


### Quorum
A replicated group of servers in the same application is called a quorum, and in replicated mode, all servers in the quorum have copies of the same configuration file

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/quorum-journal-with-zk.png)

[image source](https://hadoopabcd.files.wordpress.com/2015/02/quorum-journal-with-zk.png?w=628&h=400)



# Security

## Knox

## Ranger

### Key management service

stores keys in a file-based Java keystore.

Main functions:

* Key management: create, update + delete keys (via Web UI or REST API)
* Access control policies: manages access control policies.
* Audit

## Kerberos
Based on awesome tutorial from [roguelynn](http://www.roguelynn.com/words/explain-like-im-5-kerberos/).<br>
Name comes from three-headed dog of Hades, who protected access to the underworld.


### Ticket
Goal: You need a ticket (on local machine)

As long as it is valid, you can access the requested service that is within Kerberos realm. Avoids re-entering password.

### Principal
Represents unique identity.
Kerberos assigns tickets to principals

Format: 

user

```sh
user@example.com
```

service principal

```sh
username/fully.qualified.domain.name@YOUR-REALM.COM
```

### Keytab
File containing pairs of Kerberos principals and encrypted copy of that principals' key.

* Are unique to each host (since keys include hostname)
* file is used to authenticate a principal on a host to Kerberos
* keytab file equivalent to password file 
* Access to the file should be tightly secured (access to file allows to act as principal)
* readable by minimal set of users, stored on local disk, not backed up

e.g.

```sh
username/fully.qualified.domain.name@YOUR-REALM.COM   (DES cbc mode with CRC-32)
```

### Key
For user: Key is user password. KDC stores this in encrypted form

For service principals: used to encrypt messages to the client. Usually random key, stored in KDC and Keytab


### Kerberos realm

Defines what Kerberos manages in terms of who can access what.
Both your machine and requested service live in this realm.

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/kerberos_realm.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.001.jpg)


### Key Distribution Center

Stores all secret keys for users and services in database.
relies on symmetric-key cryptography

#### Authentication Server

#### Ticket Granting Server

### Requesting access

* each interaction contains 2 messages: one you can encrypt, the other one you cannot.
* requested service/machine and KDC never communicate directly
* The KDC stores all secret keys for users and services in database
* Secret keys are: password + salt that are hashed


#### You and Authentication Server

send to server

* your name/ID
* name/ID of requested service
* your network address
* requested lifetime for TGT

Authentication server does

* ID lookup in KDC
* randomly generates a key (session key) for you and Ticket Granting Server TGS

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.003.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.003.jpg)


sends back two messages:

TGT, encrypted with TGS Secret Key: 

* your name/ID
* the TGS name/ID
* timestamp
* your network address
* lifetime of TGT
* TGS session key

Ticket granting server session key, encrypted with Client Secret Key:

* TGS name/ID
* timestamp
* lifetime of TGT
* TGS session key (shared key btw. you and TGS)

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.004.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.004.jpg)


Encrypt second message to obtain TGS Session Key.

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.005.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.005.jpg)


#### You and Ticket Granting Server


##### You
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.006.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.006.jpg)

Send messages:

* Authenticator, encrypted with TGS session key
	* your name/ID
	* timestamp
* unencrypted message
	* requested HTTP service name/ID
	* lifetime of ticket for HTTP service
* TGT

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.006.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.006.jpg)

##### Ticket Granting Server

* Checks if service exists
* decrypts TGT with secret key to get TGS session key
* decrypts Authenticator with TGS session key

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.008.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.008.jpg)

will then check

* compare your client ID from the Authenticator to that of the TGT
* compare the timestamp from the Authenticator to that of the TGT (typical Kerberos-system tolerance of difference is 2 minutes, but can be configured otherwise)
* check to see if the TGT is expired (the lifetime element),
* check that the Authenticator is not already in the TGS’s cache (for avoiding replay attacks), and
if the network address in the original request is not null, compares the source’s IP address to your network address (or within the requested list) within the TGT.


prepares two messages

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.009.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.009.jpg)

HTTP Service ticket, encrypted with HTTP Secret Service Key contains:

* your name/ID
* HTTP Service name/ID
* your network address (may be a list of IP addresses for multiple machines, or may be null if wanting to use on any machine)
* timestamp
* lifetime of the validity of the ticket, and
* HTTP Service Session Key


Encrypted with TGS session key

* HTTP Service name/ID,
* timestamp,
* lifetime of the validity of the ticket, and
* HTTP Service Session Key


At this point: 
Can decrypt second message, but not first one

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.010.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.010.jpg)


#### You and HTTP Service

##### You
send

* Authentication message, encrypted with HTTP Service Session key.
	* your name/ID
	* timestamp
* Still encrypted HTTP Service Ticket

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.011.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.011.jpg)

##### HTTP Service

* Decrypts Ticket with Secret Key to obtain HTTP Service Session Key
* Decrypts Authenticator message with HTTP Service Session Key

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.012.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.012.jpg)


Service checks:

* compares your client ID from the Authenticator to that of the Ticket,
* compares the timestamp from the Authenticator to that of the Ticket (typical Kerberos-system tolerance of difference is 2 minutes, but can be configured otherwise),
* checks to see if the Ticket is expired (the lifetime element),
* checks that the Authenticator is not already in the HTTP Server’s cache (for avoiding replay attacks), and
* if the network address in the original request is not null, compares the source’s IP address to your network address (or within the requested list) within the Ticket.

sends Authenticator message

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.013.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.013.jpg)

##### You

Decrypt authenticator message

# Other

## JMX architecture

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/jmx.png)

[image source](https://www.safaribooksonline.com/library/view/cassandra-the-definitive/9781491933657/assets/ctdg_1001.png)

(<a href="#top">Back to top</a>)
<hr>

## Thrift 

Thrift provides a great framework for developing and accessing remote services. It allows developers to create services that can be consumed by any application that is written in a language that there are Thrift bindings for (which is...just about every mainstream one, and more).

It manages:

* serialization of data to and from a service
* the protocol that describes a method invocation, response, etc
* Thrift uses TCP (not sure if UDP is/will be supported) and so a given service is bound to a particular port.
 
(<a href="#top">Back to top</a>)
<hr>

### Networking stack

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/thrift_networking_stack.png)

[image source](http://3.bp.blogspot.com/-MuIbUycK0eI/Va6a70JxwjI/AAAAAAAABRo/_UGabAOfkNo/s320/thrift.png)

(<a href="#top">Back to top</a>)
<hr>


### Thrift server
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata//thrift-server.png)

[image source](http://2.bp.blogspot.com/-gh4wM0lmruQ/Va6qyamHMbI/AAAAAAAABR4/XV9y3L-wgDg/s400/thrift-server.png)

(<a href="#top">Back to top</a>)
<hr>


### Comparison with SOAP and REST

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/rest_soap_thrift.png)

[image source](http://nordicapis.com/microservice-showdown-rest-vs-soap-vs-apache-thrift-and-why-it-matters/)

Analogy sending a letter using REST, SOAP, and Thrift: [http://nordicapis.com/microservice-showdown-rest-vs-soap-vs-apache-thrift-and-why-it-matters/](http://nordicapis.com/microservice-showdown-rest-vs-soap-vs-apache-thrift-and-why-it-matters/).

ZooKeeper can be used to store Thrift service location information and manage its state ([source](https://www.chrismoos.com/2011/05/25/thrift-and-zookeeper/)).

Further reading: [link](http://thatguyfromthisworld.blogspot.de/2015/07/lets-understand-apache-thrift.html)

(<a href="#top">Back to top</a>)
<hr>

## System of record vs system of engagement

### System of record

“Systems of Record” are the ERP-type systems we rely on to run our business (financials, manufacturing, CRM, HR).  They have to be “ correct” and “integrated” so all data is consistent. And they were traditionally designed for people who have no choice but to use them.
[source](http://www.forbes.com/sites/joshbersin/2012/08/16/the-move-from-systems-of-record-to-systems-of-engagement/#6a27371f50c4)

### System of engagement

“Systems of Engagement” are systems which are used directly by employees for “ sticky uses” – like email, collaboration systems, and new social networking and learning systems.  They “engage” employees.
[source](http://www.forbes.com/sites/joshbersin/2012/08/16/the-move-from-systems-of-record-to-systems-of-engagement/#6a27371f50c4)

![{{base}}/images/bigdata/lambda_architecture.png]({{base}}/images/bigdata/system_of_record.jpg)

[image source](http://image.slidesharecdn.com/palmercmomg102813-131128113447-phpapp02/95/supporting-knowledge-workers-with-adaptive-case-management-8-638.jpg?cb=1385638592)


## Schema-on-read vs schema-on-write

## Data governance 

