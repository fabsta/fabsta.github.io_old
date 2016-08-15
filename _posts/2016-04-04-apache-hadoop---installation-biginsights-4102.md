---
title: "IBM open data platform: Installation (BigInsights v4.102)"
description: ""
category: Hadoop
tags: [Installation, hadoop]
---


## Tutorial on how to install IBM Open Data Platform on RHEL 7

The tutorial consists of the following steps

* setup yum and configure the cluster
* setup access to all cluster nodes
* configure cluster nodes for component installation via Ambari
* install Ambari via yum
* install hadoop components via Ambari Web-UI

## Requirements


Prepare Yum installation

```
yum install httpd
```

#### start the apache webserver

```
apachectl start
```

#### download the repository files

```
// Ambari
wget https://ibm-open-platform.ibm.com/repos/Ambari/rhel/7/x86_64/2.1.x/Updates/2.1.0_Spark-1.5.1/BI-AMBARI-2.1.0-Spark-1.5.1-20160105_1212.el7.x86_64.tar.gz

// IOP
wget https://ibm-open-platform.ibm.com/repos/IOP/rhel/7/x86_64/4.1.x/Updates/4.1.0.0_Spark-1.5.1/IOP-4.1-Spark-1.5.1-20151209_2001.el7.x86_64.tar.gz
// IOP utils
wget https://ibm-open-platform.ibm.com/repos/IOP-UTILS/rhel/7/x86_64/1.1/iop-utils-1.1.0.0.el7.x86_64.tar.gz

```


```
mkdir -p /var/www/html/repos
```

untar the archives into the new directory

```
tar xzvf BI-AMBARI-2.1.0-Spark-1.5.1-20160105_1212.el7.x86_64.tar.gz /var/www/html/repostar xzvf IOP-4.1-Spark-1.5.1-20151209_2001.el7.x86_64.tar.gz /var/www/html/repostar xzvf iop-utils-1.1.0.0.el7.x86_64.tar.gz /var/www/html/repos
```

#### download yum profile
go to 

```
http://www-01.ibm.com/support/knowledgecenter/SSPT3X_4.0.0/com.ibm.swg.im.infosphere.biginsights.install.doc/doc/bi_inst_iop.html?lang=en-us
```and get the following IOP yum repo file:```
IOP-4.1.0.0-1.el7.x86_64.rpm
``` 

#### Install the file under /etc/yum.repos.d/ with:

```
yum install IOP-4.0.0.0.x86_64.rpm
or 
rpm -i IOP-4.0.0.0.x86_64.rpm
```


### In case you want to install from a local Rhel-DVD

open the ambari.repo (that you just installed) and change the baseurl to point to your local mirror

```
vi /etc/yum.repos.d/ambari.repobaseurl=file///var/www/html/repos/Ambari/rhel/7/x86_64/2.1.x/Updates/2.1.0_Spark-1.5.1gpgcheck=0 orgpgkey=https://ibm-open-platform.ibm.com/repos/Ambari/rhel/7/x86_64/2.1.x/GA/2.1/BI-GPG-KEY.public
```

either disable gpgcheck or adjust the gpg key

clean yum before we start the installation process

```
yum clean all
```


## Install Ambari
```
yum install ambari-server
```

if you are using a local mirror, make sure the following settings are for your version.

```
vi /var/lib/ambari-server/resources/stacks/BigInsights/4.1/repos/repoinfo.xml<os type="redhat7"> <repo> <baseurl>http://biginsights01/IOP/RHEL7/x86_64/4.1</baseurl> <repoid>IOP-4.0</repoid> <reponame>IOP</reponame> </repo> <repo> <baseurl>http://biginsights01/IOP-UTILS/RHEL7/x86_64/1.1</baseurl> <repoid>IOP-UTILS-1.0</repoid> <reponame>IOP-UTILS</reponame> </repo> </os>
```

#### Java SDK Path
By default, this should be set correctly, but let's verify that:

```
vi /etc/ambari-server/conf/ambari.propertiesjdk1.7.url=http://ibm-open-platform.ibm.com/repos/IOP-UTILS/rhel/7/x86_64/1.1/openjdk/jdk-1.7.0.tar.gz
jdk1.8.url=http://ibm-open-platform.ibm.com/repos/IOP-UTILS/rhel/7/x86_64/1.1/openjdk/jdk-1.8.0.tar.gz


```


## modify the following files on each machine

#### assign host names to ip addresses
We have 5 machines and don't want to remember the machines ip addresses, so we add 
add domain names to /etc/hosts. 

```
vi /etc/hosts127.0.0.1 localhost.localdomain localhost
127.17.97.140 biginsights01
127.17.97.141 biginsights02
127.17.97.142 biginsights03
127.17.97.143 biginsights04
127.17.97.144 biginsights05

```
If we are on node 127.17.97.140, we can ssh into another node (127.17.97.141) with

```
ssh biginsights02
``` 
but we are asked for a password. The next step allows us to avoid this.

# prepare passwordless ssh into other machines
generate an RSA key pair.

```
ssh-keygen
```

copy public key to all cluster machines + local machine

```
ssh-copy-id -i ~/.ssh/id_rsa.pub root@biginsights01ssh-copy-id -i ~/.ssh/id_rsa.pub root@localhost
```
if this step hangs, it might be because the ip-address associated with biginsights01
isn't known in the network, because intra-node communication is disabled.
Ask your administrator to enable it (you might have to adjust the ip addresse in /etc/hosts). 


#### disable IPv6

```
echo "net.ipv6.conf.all.disable_ipv6 = 1" >> /etc/sysctl.confecho "net.ipv6.conf.lo.disable_ipv6 = 1" >> /etc/sysctl.confecho "net.ipv6.conf.default.disable_ipv6 = 1" >> /etc/sysctl.conf
```

#### check sysctl

```
sysctl -p
```

### disable firewalls

```
//stop firewall
service firewalld stop

//disable firewall
systemctl disable firewalld

```

#### disable THP (transparent huge pages):

```
echo never > /sys/kernel/mm/transparent_hugepage/enabled
```

to disable THP even after reboot:

```
vi /etc/rc.localif test -f /sys/kernel/mm/transparent_hugepage/enabled; then    echo never > /sys/kernel/mm/transparent_hugepage/enabledfi
```

check if NTP (network time protocol) is running.
Important because you want all your computer to use the same time reference.

```
ntpstat
```

and make sure it's turned on after reboot

```
chkconfig ntpd on
```

#### disable selinux

```
vi /etc/selinux/configselinux=disabled
```

to effectively disable it:

```
setenforce 0
```

ok, now we are able to 

```
ssh biginsights02
```

from e.g. biginsights01 without being required to enter a password.

The installation of hadoop components will be done via Ambari:




## Setup ambari server
```
ambari-server setup
```

## clean yum again
```
yum clean all
```

```
ambari-server start
```

## Continue installation in Ambari 
go to the ambari web UI
```
172.17.97.140:8080
```

login with
```
admin:admin
```

As you haven't setup a cluster yet, the ambari agent will guide you
through the installation process. 

You will need to

* Select a cluster name
* confirm hosts (provide content of /etc/hosts + ssh public key)
* choose services
* assign master and slaves
* review
* install

Ambari will give you an installation progress bar. The installation might take >30 minutes.

Happy hadooping!