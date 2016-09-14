---
title: "Big Data Concepts Ingestion"
description: "Overview of Hadoop Tools and Concepts - Ingestion"
category: BigData
tags: [BigData]
sidebar:
  nav: "new_side"
---



### Table of contents

* TOC
{:toc}


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

