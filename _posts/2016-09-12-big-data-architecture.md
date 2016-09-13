---
title: "Big Data Architecture thoughts"
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

(<a href="#top">Back to top</a>)
<hr>


# CPU

* at least 1 CPU for 1 HDD -> handle the thread processing the data from this HDD
* better: 2x cores as the amount of HDDs, given compression and intermediate data

e.g. 12-HDD server with 10 HDD -> 20 CPUs

# RAM
The more the better.

More Ram gives servers more OS-level cache.

More HDFS cache available for queries



# HDFS

## NameNode

### RAM
* 1 GB RAM / 1 Mio data blocks

## Datanode

* Temp storage for intermediate results
* with a 3 * X cluster, leave 1 X for temp storage (e.g. HBase region merges, sorting)


## JournalNodes

* relatively lightweight
* can be collocated with e.g. NameNode, JobTracker, YARN ResourceManager
* at least 3 JournalNode daemons, since edit log modifications must be written to majority of JNs (allows to tolerate failure of machine)

# HBase

Considerations
* Heap-size limits due to garbage collector timeouts --> max of 16Gb per Region Server



# Zookeeper

* run in 3 (to allow one failure without data loss) or more nodes. 5 or more is better as it allows 
* ZKFC run on each Namenode


# Spark

## Master nodes

### Thrift server
usually come with a thrift server on each master node.


# Oozie

required for HA

* a database that supports concurrent connections
* a load balancer

# Tests

## Namenode automatic failover
Simulate JVM crash
```sh
kill -9 <pid of NN>
```

Check logs for the  ZKFC daemons as well as NameNode daemons