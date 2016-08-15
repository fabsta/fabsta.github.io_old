---
title: "Oozie   file triggered workflow execution"
description: "Overview of how to trigger a workflow execution with files in Apache Oozie"
category: hadoop
tags: [oozie, workflow]
---

# Oozie
Oozie ([https://oozie.apache.org](https://oozie.apache.org)) is 

>  a workflow scheduler system to manage Apache Hadoop jobs.

It allows you to automate common tasks, e.g.

* web server log analysis 
* hive ETL jobs

## Components: workflow + coordinator
A **workflow** is a piece of code that Oozie can run. This can be e.g. a bash script that transforms a file and saves in it another location.

A **coordinator** job is a wrapper around one/many workflow that adds one or both of the following constraints

* run a workflow at given time intervals (e.g. every 6 hours).
* start the workflow when a new file is present in HDFS.

## Example: trigger a workflow when a new file is stored in HDFS.

The following example ([source code](https://github.com/fabsta/oozie_hive_file_trigger)) shows 

* how to start a coordinator job that is waiting for the existence of a file in HDFS. 
* runs a hive job that creates an external table on the new file.



### become oozie user

all actions will be executed as user oozie

```
su - oozie
```
define oozie server url

```
export OOZIE_URL=http://192.168.100.141:11000/oozie
```
go to project folder

```
cd /home/oozie/examples/apps/oozie-hive.
```

you will find the following files:

* job.properties: namenode, jobtracker (please adjust these) as well as URI of workflow || coordinator app
* coordinator.xml: infos about scheduling and file trigger
* script.q: example hive script
* workflow.xml: the coordinator will execute what is in the workflow.xml (script.q) once the file exists


copy files to hdfs

all project files - except job.properties - are expected to be on hdfs. So we copy the files to hdfs

```
hdfs dfs -put -f /home/oozie/examples/apps/oozie-hive/ /user/oozie/examples/apps/
```

### start job

```
oozie job -config job.properties -run
```

returns the job id. e.g. 0000000-160331163827649-oozie-oozi-C

What happens under the hood:

* oozie reads job.properties and the get the url of the wf (workflow) or coord (coordinator) application (on hdfs).
* (the only file not in hdfs is the job.properties file. keep that in mind when editing files. Update the hdfs via (hdfs dfs -put -f examples/apps/oozie-hive/ /user/oozie/examples/apps/))
* oozie starts the wf/coord job.

Ok, the job is now running.

### check job log

There are two ways to check what your oozie jobs are doing: via command line and via web interface

#### command line

```
oozie job  -log 0000000-160331163827649-oozie-oozi-C
```

#### web interface

```
http://172.17.97.141:11000/oozie/
```

Checking the log wills tell you that the job is currently waiting for the following file:

```
hdfs://biginsights01:8020/user/oozie/examples/input-data/rawLogs/2016/03/31//_SUCCESS
```

So, to start the job, we create the file with:

```
hdfs dfs -put /home/oozie/_SUCCESS /user/oozie/examples/input-data/rawLogs/2016/03/31/
```

now if you check the file log again it should tell that it has found the file and that the job is running.

### hive action + job verification

the example hive-script (script.q) is supposed to create a 'test' table in hive. To verify that the workflow has worked, just do a

### hive -e 'show tables'

if there is a table *test*, the workflow was successful. 