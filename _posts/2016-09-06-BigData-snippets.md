---
title: "BigData code snippets"
description: "BigData code snippets"
category: Programming
tags: [programming]
sidebar:
  nav: "new_side"
---

# Table of contents

* TOC
{:toc}


# Hive


## Components

### Starting up components
```sh
# Metastore
hive --service metastore &
# Hiveserver2 
hive --service hiveserver2 &
# Hive CLI 
$HIVE_HOME/bin/hive
# Beeline
$HIVE_HOME/bin/beeline
```

(<a href="#top">Back to top</a>)
<hr>

### Execution
```sh
# Hive CLI
$HIVE_HOME/bin/hive
# HiveServer + Beeline
$HIVE_HOME/bin/hiveserver2
$HIVE_HOME/bin/beeline -u jdbc:Hive2://$HiveServer2_HOST:$HiveServer2_PORT
# HCatalog
$HIVE_HOME/hcatalog/sbin/hcat_server.sh
$HIVE_HOME/hcatalog/bin/hcat
# WebHCat
$HIVE_HOME/hcatalog/sbin/webhcat_server.sh
```

(<a href="#top">Back to top</a>)
<hr>

## Command line parameters
```sh
```

(<a href="#top">Back to top</a>)
<hr>

### Configurations
```sh
SET key=value;
```
(<a href="#top">Back to top</a>)
<hr>

## Storage

### Default storage location
```sh
/apps/hive/warehouse
```

(<a href="#top">Back to top</a>)
<hr>

# BigSQL

## Commands

### Connect
```sh
#Jsqsh
/usr/ibmpacks/common-utils/current/jsqsh/bin/jsqsh --setup
/usr/ibmpacks/common-utils/current/jsqsh/bin/jsqsh bigsql
```

(<a href="#top">Back to top</a>)
<hr>

### Tables

#### Create HBase table
```sh
CREATE HBASE TABLE BIGSQLLAB.REVIEWS ( 
REVIEWID 	varchar(10) primary key not null,
PRODUCT		varchar(30), 
RATING		int, 
REVIEWERNAME	varchar(30), 
REVIEWERLOC	varchar(30), 
COMMENT		varchar(100), 
TIP		varchar(100)
) 
COLUMN MAPPING 
(
key		mapped by (REVIEWID), 
summary:product	mapped by (PRODUCT),
summary:rating  mapped by (RATING),
reviewer:name	mapped by (REVIEWERNAME),
reviewer:location  mapped by (REVIEWERLOC),
details:comment    mapped by (COMMENT),
details:tip	   mapped by (TIP) 
);
```

(<a href="#top">Back to top</a>)
<hr>

## Storage

### Log file
```sh
/var/ibm/bigsql/logs/bigsql.log
```

### Hbase data files
```sh
/hbase/data/default/table
```

(<a href="#top">Back to top</a>)
<hr>

## Debugging

```sh
# readers log levels
$BIGSQL_HOME/conf/glog-dfsio.properties
```

# distru

### Get Infos

Has Analyse been run?

```sh
select substr(tabname,1,20) as TABNAME,substr(colname,1,20) as COLNAME, colcard, numnulls from syscat.columns where tabschema='TPCDS';
# or
select substr(tabname,1,20),stats_time,card from syscat.tables where tabschema='TPCDS';
```

CPU limits

```sh
ps -ef | grep bigsql | grep db2
// get process id from db2sysc  and db2fmpr
taskset -p 4109 && taskset -p 4135
```

SORTHEAP SHEAPTHRES_SHR

```sh
SELECT NAME, VALUE, DEFERRED_VALUE, DBPARTITIONNUM FROM SYSIBMADM.DBCFG WHERE DBPARTITIONNUM=0 and (name like '%sort%' or name like '%sheap%');
```

hashjoin information

```sh
select member, total_hash_joins, total_hash_loops, hash_join_overflows, hash_join_small_overflows from table(mon_get_database(-2)) order by member;
```

temporary tablespace paths check

```sh
SELECT member,count(container_name) as count_containers FROM TABLE(MON_GET_CONTAINER('',-2)) AS t where tbsp_name='TEMPSPACE1' group by member ;
```


### Execute job

#### Run on all nodes
```sh
cat /home/bigsql/sqllib/db2nodes.cfg | while read NODE HOST MLN;
do
  echo "## Executing command on $HOST ##"
  ssh -n -f ${HOST} ‘<command to execute>'
done
```

(<a href="#top">Back to top</a>)
<hr>


#### Run from master on all nodes
```sh
cat /home/bigsql/sqllib/db2nodes.cfg | grep -v `hostname `| while read NODE HOST MLN
do
  echo "## Executing command on $HOST ##"
  ssh -n -f ${HOST} ‘<command to execute>'
done
```

(<a href="#top">Back to top</a>)
<hr>

# HBase


## Commands

### Table

```sh
# Create
create 'table1','col_fam1','col_fam2','col_fam3'
# Describe
describe 'table1'
# Disable
disable 'table1'
# Alter
alter 'table1', {NAME => 'col_fam1',COMPRESSION => 'GZ'}
# Cache
alter 'table1', {NAME => 'col_fam1', IN_MEMORY => 'true'}
```

(<a href="#top">Back to top</a>)
<hr>


## Storage

### Default storage location

```sh
/apps/hbase/data/data/default
```

(<a href="#top">Back to top</a>)
<hr>



# Security

## Kerberos

### install

[biginsights](https://www.youtube.com/watch?v=JNSBcbZeai4)


### useful commands

Get new ticket / refresh

```sh
kinit USER
# specific user
kinit alice/admin@EXAMPLE.COM
# keytab file (allows to authenticate without knowledge of password)
kinit -kt alice.keytab alice/admin@EXAMPLE.COM
```

list valid tickets

```sh
klist
```

Destroying credentials cache

```sh
kdestroy
```

#### Principal

```sh
# Adding new principal:
kadmin: addprinc alice@EXAMPLE.COM
# Displaying the details of a principal in the Kerberos database
kadmin: getprinc alice@EXAMPLE.COM
# Deleting a principal from the Kerberos database
kadmin: delprinc alice@EXAMPLE.COM
# Listing all the principals in the Kerberos database
kadmin: listprincs
```

### Kerberos utilities

* kdb5_util: Maintenance utility for Kerberos database. Used for creating Realm etc.
* kadmin: Admin utility for Kerberos which internally uses kadmind. Used for remote administration
* kadmin.local: Admin utility that access the Kerberos database directly
* kadmind: Kerberos admin server daemon
* kinit: Kerberos client to authenticate with Kerberos and retrieve the TGT
* kpasswd: Utility for changing the users password
* klist: Utility to view the Kerberos tickets

### Troubleshooting

* access logs on ticket granting server (TGS)
* display http headers that are send 


# Ambari

## Metrics

### debugging
```sh
# log location
/var/log/ambari-metrics-collector/
# verify available disk space
df -h
# verify available memory 
free -m
# see running processes/cpu usage for user ams
top -u ams
# Check HBase regionserver and HMaster are still running 
ps -ef | grep ams
```

# HDFS

## Job history server

via command line:

```sh
hadoop job -list
```

# Web UIs

```sh
#job history
:8443/gateway/jobhistoryui/history
```



# docker
repository: https://github.com/f-stibane/hdp-cluster-docker

# changes to make

```sh
docker-compose up
localhost:8080

setup-cluster.py
```