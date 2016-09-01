---
title: "Kafka   best practice"
description: "Overview of best practices for Apache Kafka"
category: hadoop
tags: [hadoop, kafka, queue]
sidebar:
  nav: "new_side"
---



# Kafka Best practices

## Components - Producers

[FAQ overview](https://cwiki.apache.org/confluence/display/KAFKA/FAQ#FAQ-Producers)

Config most useful options are:

* producer.type (default sync)
* request.required.acks (default 0)
* compression.codec (default none)
* batch.num.messages (default 200)

all: http://kafka.apache.org/documentation.html#producerconfigs

## Component - Consumers

[Excerpt from FAQs](https://cwiki.apache.org/confluence/display/KAFKA/FAQ#FAQ-Consumers)

*	Should I choose multiple group ids or a single one for the consumers?
*	Can I predict the results of the consumer rebalance?
*	How can I rewind the offset in the consumer?
*	How to improve the throughput of a remote consumer?
*	I don't want my consumer's offsets to be committed automatically. Can I manually manage my consumer's offsets?
*	What is the relationship between fetch.wait.max.ms and socket.timeout.ms on the consumer?
*	How do I get exactly-once messaging from Kafka?
*	Why can't I specify the number of streams parallelism per topic map using wildcard stream as I use static stream handler?
*	How to consume large messages?
*	How do we migrate to committing offsets to Kafka (rather than Zookeeper) in 0.8.2?

[configs options](http://kafka.apache.org/documentation.html#brokerconfig)

most useful are:

*	broker.id: each broker needs unique id

*	logs.dir: log data store (/tmp/kafka-logs)

*	zookeeper.connect: zookeeper connection string

*	host.name: broker hostname

*	num.partitions: default = 1

*	auto.create.topics.enable: default = true

*	default.replication.factor: default = true


## Components - Brokers

[Excerpt from FAQs](https://cwiki.apache.org/confluence/display/KAFKA/FAQ#FAQ-Brokers)

*	How does Kafka depend on Zookeeper?
*	How many topics can I have?
*	How to reduce churns in ISR? When does a broker leave the ISR ?
*	How do I accurately get offsets of messages for a certain timestamp using OffsetRequest?
*	Can I add new brokers dynamically to a cluster?
*	How do I choose the number of partitions for a topic?


## Troubleshooting

### Common cause

[consumer lag](http://www.slideshare.net/miguno/apache-kafka-08-basic-training-verisign slide 50)

*	is a consumer problem, caused by
*	too slow, too much GC, losing connection to ZK
*	bug or design flaw
*	operational mistake

### Brokers

FAQs from [https://cwiki.apache.org/confluence/display/KAFKA/FAQ#FAQ-Brokers](https://cwiki.apache.org/confluence/display/KAFKA/FAQ#FAQ-Brokers).

*	Why do I see error "Should not set log end offset on partition" in the broker log?
*	Why does controlled shutdown fail?
*	Why can't my consumers/producers connect to the brokers?
*	How to replace a failed broker?
*	After bouncing a broker, why do I see LeaderNotAvailable or NotLeaderForPartition exceptions on startup?
*	Why do I see lots of Leader not local exceptions on the broker during controlled shutdown?
*	Why partition leaders migrate themselves some times?

### Producers

FAQs from [https://cwiki.apache.org/confluence/display/KAFKA/FAQ#FAQ-Producers](https://cwiki.apache.org/confluence/display/KAFKA/FAQ#FAQ-Producers)

*	I am using the ZK-based producer in 0.7 and I see data only produced on some of the brokers, but not all, why?
*	Why are my brokers not receiving producer sent messages?
*	Why is data not evenly distributed among partitions when a partitioning key is not specified?
*	Why do I get QueueFullException in my producer when running in async mode?

### Consumers

FAQS via [https://cwiki.apache.org/confluence/display/KAFKA/FAQ#FAQ-Consumers](https://cwiki.apache.org/confluence/display/KAFKA/FAQ#FAQ-Consumers)

*	Why does my consumer never get any data?
*	Why does my consumer get InvalidMessageSizeException?
*	Why some of the consumers in a consumer group never receive any message?
*	Why are there many rebalances in my consumer log?
*	My consumer seems to have stopped, why?
*	Why messages are delayed in my consumer?

### Monitoring tools

To e.g. check consumer offset, dump logs, export zookeeper offsets ([link](https://cwiki.apache.org/confluence/display/KAFKA/System+Tools)):

Visualising using Kibana: https://www.elastic.co/blog/logstash-kafka-intro

Auditing kafka: http://www.slideshare.net/miguno/apache-kafka-08-basic-training-verisign slide 55

every producer writes to "stats" topic how many messages produced

##Topics

*	don't break into sep. topics unless data is truly independent
*	how to add/remove/modify topics
*	https://kafka.apache.org/documentation.html#operations

###Partition

*	keep time-related information in same partition

##Operations

[https://kafka.apache.org/documentation.html#operations](https://kafka.apache.org/documentation.html#operations) covers

*	mirroring data btw. clusters
*	graceful shutdown
*	balancing leadership
*	expanding cluster
*	increasing replication factor

### Testing

#### Integration testing

There is a section here: [https://github.com/miguno/kafka-storm-starter](https://github.com/miguno/kafka-storm-starter)

## Performance tuning

### General

*	often not much tuning required!
*	maybe
*	num.io.threads
*	should be >=#disks (start with == #disks)
*	num.network.threads
*	adjust based on #producers,#consumers + replication factor

### Kernel tuning

*	lots of RAM
*	gives huge page cache & avoid disk I/O

### Disk throughput

*	longer commit intervals
*	increase flush time (Linkedin 120s, default 30s)

### Java/JVM tuning

*	minimize GC pauses
*	use of Oracle JDK solves some problems
*	it uses new G1 garbage-first collector

## References

### User guide
[http://www.confluent.io/blog/stream-data-platform-1/](http://www.confluent.io/blog/stream-data-platform-1/)
[http://www.confluent.io/blog/stream-data-platform-2/](http://www.confluent.io/blog/stream-data-platform-2/)

### extensive best practice guide for Storm & Kafka
[https://community.hortonworks.com/articles/550/unofficial-storm-and-kafka-best-practices-guide.html](https://community.hortonworks.com/articles/550/unofficial-storm-and-kafka-best-practices-guide.html)

### FAQs
[https://cwiki.apache.org/confluence/display/KAFKA/FAQ](https://cwiki.apache.org/confluence/display/KAFKA/FAQ)

### Kafka ecosystem
connectors & hadoop integration: [https://cwiki.apache.org/confluence/display/KAFKA/Ecosystem](https://cwiki.apache.org/confluence/display/KAFKA/Ecosystem)
