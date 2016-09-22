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


## Data Lake

### Security

#### DMZ

* aka. perimeter network
* contains + exposes organization's external-facing services to larger network
* Purpose: Add additional layer of security
* External nodes need to go through DMZ rather than directly to internal services 

### Goals

* Provide one way (a process) to collect all data* Process, clean, and enrich the data in one location* Store data only once* Access the data using a standard interface

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/data_lake_components.png)

[image source](http://www.roguelynn.com/assets/images/Kerb.003.jpg)


### Firewall settings

#### Data movement
setting firewall rules done by considering the following questions:

* Allow FTP traffic from a few FTP servers to 1/many edge nodes
* Allow worker nodes to connect to 1/more databases + receive data over specified port* Allow data flow from log events from web servers to a set of flume agents over limited number of ports

#### Client traffic

#### Administration traffic

* Logging into cluster machines
* Audit event traffic

### Data movement / Ingestion

consists of several parts:

* Parsing
* Enrichment:  (e.g.DNS resolution, but shouldn't slow down ingestion pipeline)
* Federated data: Bringing data from different data sources together
* Aggregation: compute various types of statistics
* Third-party access: 


### Storage

#### Raw vs. processed data

* Are we storing raw and/or processed records?* If we store processed records, what data format are we going to use?* Do we need to index the data to make data access quicker? (Caching, Pre-computation)* Are we storing context, and if so, how?* Are we enriching some of the records?* How will the data be accessed later?

##### Raw

* Reparse the data, if parsing was incomplete or the parsers were wrong.* Raw data to be shown to the user.* Other data-processing steps will need raw data (e.g.NLP or sentiment analysis)* Raw data is required to be stored by compliance or regulatory mandates.


#### How data is used?

* How much data do we have in total?* How fast does the data need to be ready?* How much data do we query at a time, and how often do we query?* Where is the data located, and where does it come from?* What do you want to do with the data, and how do you access it?
	* Search
	* Analytics
		* Schema: What is the schema for the data?
		* Schema-stability: 
			* Does the schema change over time? 
			* How does it change? 
			* Are there only additions or also deletions of columns/fields? How many? 
			* How often does that occur?
		* Speed: Do we need caching layer (built-in/external)?
		* Data Partitioning: For speed
		* Sub-types:
			* Record-based analytics (BI use cases)
				* Flexibility of schema-on-demand vs speed (e.g. Hive schema-on-demand -> parse on every query)
				* Aggregates: Speed up queries by calc aggregates (OLAP)
			* Relationships (using graphs)
			* Data mining (running algorithms against data)
	* Raw data access
	* Real-time statistics
	* Real-time correlation



#### Parsing data

Three approaches to parse data

* Collection-time parsing
* Batch parsing
* Process-time parsing

#### Types of Data

* Time-series data / log data
* Contextual data


### Where to store data?

relational databases: optimized for either

* fast writes 
* fast reads

but not both (because they indices and overhead produced to guarantee ACID)



# Components

## Edge node

For:

* running client processes

not for: 

* running cluster processes 
* usually storing data (exception data ingestion+staging)


### Hardware

enough CPUs
disk space + memory if staging data for ingest

hardware: [https://community.hortonworks.com/questions/47800/edge-nodes-management.html](https://community.hortonworks.com/questions/47800/edge-nodes-management.html)

Useful links

* [https://community.hortonworks.com/questions/49745/dedicated-edge-nodes.html](https://community.hortonworks.com/questions/49745/dedicated-edge-nodes.html)
* [https://community.hortonworks.com/questions/34872/staging-on-edge-nodes.html](https://community.hortonworks.com/questions/34872/staging-on-edge-nodes.html)


## KMZ
Because the KMS plays such an important role in HDFS encryption, this component should not be collocated on servers running other Hadoop ecosystem components, or servers used as edge nodes for clients. 

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