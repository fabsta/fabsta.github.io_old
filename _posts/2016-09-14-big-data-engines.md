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


