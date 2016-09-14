---
title: "Big Data Concepts Management"
description: "Overview of Hadoop Tools and Concepts - Management"
category: BigData
tags: [BigData]
sidebar:
  nav: "new_side"
---



### Table of contents

* TOC
{:toc}



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


