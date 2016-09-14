---
title: "Big Data Concepts Engines"
description: "Overview of Hadoop Tools and Concepts - Engines"
category: BigData
tags: [BigData]
sidebar:
  nav: "new_side"
---



### Table of contents

* TOC
{:toc}


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

