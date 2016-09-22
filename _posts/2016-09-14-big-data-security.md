---
title: "Big Data Concepts Security"
description: "Overview of Hadoop Tools and Concepts - Security"
category: BigData
tags: [BigData]
sidebar:
  nav: "new_side"
---



### Table of contents

* TOC
{:toc}


# Security

## Hadoop Security

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/hadoop_security.jpg)

[image source](http://www.slideshare.net/uweseiler/20141127-hadoop-operationsdata2day)

(<a href="#top">Back to top</a>)
<hr>



## Component overview

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Typical_security_flow_via_Knox.png)

[image source](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_Knox_Gateway_Admin_Guide/content/figures/1/figures/Typical_security_flow_via_Knox.png)



## Knox
The goal of the Knox Gateway is to provide a single point of secure access for Hadoop clusters

advantages:

* __Simplified Access__: Extends Hadoops REST/HTTP services by encapsulating Kerberos to within cluster
	* Kerberos encapsulation 	* Extends API reach	* Single access point	* Multi-cluster support	* Single SSL certificate
* __Enhanced Security__: Extends Hadoops REST/HTTP services without revealing network details, providing SSL out of the box
	* Protect network details	* Partial SSL for non-SSL services	* WebApp vulnerability filter
* __Centalized Control__: Enforces REST API security centrally, routing requests to multiple Hadoop clusters
	* Central REST API auditing	* Service-level authorization	* Alternative to SSH “edge node”
		* Previously: SSH into edge node to run API commands there
* __Enterprise Integration__: Supports LDAP, Active Directory, SSO, SAML and more
	* LDAP integration	* Active Directory integration	* SSO integration	* Apache Shiro extensibility	* Custom extensibility

what it isn't:
 
* replacement for strong authentication
* channel for high volume data ingestion/export

(<a href="#top">Back to top</a>)
<hr>


### Available plugins

* WebHDFS
* WebHCat
* Oozie
* HBase
* Hive
* Yarn

(<a href="#top">Back to top</a>)
<hr>


### Masking: Knox Service URLs vs. direct URLs

WebHDFS | http://namenode-host:50070/webhdfs | https://knox-host:8443/webhdfsWebHCat | http://webhcat-host:50111/templeton | https://knox-host:8443/templetonOozie | http://ooziehost:11000/oozie | https://knox-host:8443/oozieHBase | http://hbasehost:60080 | https://knox-host:8443/hbaseHive | http://hivehost:10001/cliservice | https://knox-host:8443/hive(<a href="#top">Back to top</a>)
<hr>


### Performance payoff

1. Authentication and authorization - The additional time required to perform authentication and authorization.
2. Connection creation - The additional time required to setup the connection between Knox and the backend service.
3. Data transport - The additional time required physically move the request and response data through the Knox server unaltered.
4. Request and response processing - The additional time imposed by processing done to the request and response data stream.
5. SSL termination - The additional time imposed by SSL encryption if the direct connection to the service would otherwise not occur over a secure connection.

To speed-up things: Load-balancer

[source](https://community.hortonworks.com/questions/1858/known-performance-issue-while-using-konx.html)

(<a href="#top">Back to top</a>)
<hr>


## Ranger

### Key management service

stores keys in a file-based Java keystore.

Main functions:

* Key management: create, update + delete keys (via Web UI or REST API)
* Access control policies: manages access control policies.
* Audit

Takes care of keys for data encryption.

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/ranger_authorization_auditing.jpg)

[image source](http://image.slidesharecdn.com/hadoopsecurity-150514024026-lva1-app6891/95/hadoop-security-22-638.jpg?cb=1431571324)


(<a href="#top">Back to top</a>)
<hr>

## Kerberos

Based on awesome tutorial from [roguelynn](http://www.roguelynn.com/words/explain-like-im-5-kerberos/).<br>
Name comes from three-headed dog of Hades, who protected access to the underworld.

Provides:

* Authentication (Access from users logged in on cluster gateways)
* Ticket granting service (Access from any other service or daemon (e.g. HCatalog server))
* Access from MapReduce tasks (see Delegation Tokens)

Consists of:

* Client (does majority of processing burden --> distributes work)
* Server (no communication btw Server and KDC)
* trusted third party (Kerberos Key Distribution Center)

(<a href="#top">Back to top</a>)
<hr>


### Components

#### Account database

Kerberos uses the domain's Active Directory as its account database.

#### Kerberos tray 

* Place in memory where TGTs and service tickets are stored
* cannot be swapped out to disk

(<a href="#top">Back to top</a>)
<hr>

#### Principal
Represents unique identity.
Kerberos assigns tickets to principals

Format: 

user

```sh
user@example.com
```

service principal

```sh
username/fully.qualified.domain.name@YOUR-REALM.COM
```

(<a href="#top">Back to top</a>)
<hr>

### Keytab

File containing pairs of Kerberos principals and encrypted copy of that principals' key.

* Are unique to each host (since keys include hostname)
* file is used to authenticate a principal on a host to Kerberos
* keytab file equivalent to password file 
* Access to the file should be tightly secured (access to file allows to act as principal)
* readable by minimal set of users, stored on local disk, not backed up

e.g.

```sh
username/fully.qualified.domain.name@YOUR-REALM.COM   (DES cbc mode with CRC-32)
```

### Key

For user: Key is user password. KDC stores this in encrypted form

For service principals: used to encrypt messages to the client. Usually random key, stored in KDC and Keytab

(<a href="#top">Back to top</a>)
<hr>


### Kerberos realm

Defines what Kerberos manages in terms of who can access what.
Both your machine and requested service live in this realm.

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/kerberos_realm.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.001.jpg)

(<a href="#top">Back to top</a>)
<hr>


### Key Distribution Center

* Stores all secret keys for users and services in database.
* Relies on symmetric-key cryptography
* In an Active Directory network: Active Directory domain controller
* Has keys of all participants (users and services)
* Uses user/service keys to encrypt messages

consists of two services: 

* Authentication Server
* Ticket Granting Server

### Requesting access

* each interaction contains 2 messages: one you can encrypt, the other one you cannot.
* requested service/machine and KDC never communicate directly
* The KDC stores all secret keys for users and services in database
* Secret keys are: password + salt that are hashed


1. Authentication
2. Authorization

Overview picture!

(<a href="#top">Back to top</a>)
<hr>


#### You and Authentication Server

send to server

* your name/ID
* name/ID of requested service
* your network address
* requested lifetime for TGT

Authentication server does

* ID lookup in KDC
* randomly generates a key (session key) for you and Ticket Granting Server TGS

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.003.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.003.jpg)


sends back two messages:

TGT, encrypted with TGS Secret Key: 

* your name/ID
* the TGS name/ID
* timestamp
* your network address
* lifetime of TGT
* TGS session key

Ticket granting server session key, encrypted with Client Secret Key:

* TGS name/ID
* timestamp
* lifetime of TGT
* TGS session key (shared key btw. you and TGS)

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.004.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.004.jpg)


Encrypt second message to obtain TGS Session Key.

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.005.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.005.jpg)

(<a href="#top">Back to top</a>)
<hr>


#### You and Ticket Granting Server


##### You

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.006.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.006.jpg)

Send messages:

* Authenticator, encrypted with TGS session key
	* your name/ID
	* timestamp
* unencrypted message
	* requested HTTP service name/ID
	* lifetime of ticket for HTTP service
* TGT

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.006.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.006.jpg)

(<a href="#top">Back to top</a>)
<hr>

##### Ticket Granting Server

* Checks if service exists
* decrypts TGT with secret key to get TGS session key
* decrypts Authenticator with TGS session key

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.008.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.008.jpg)

will then check

* compare your client ID from the Authenticator to that of the TGT
* compare the timestamp from the Authenticator to that of the TGT (typical Kerberos-system tolerance of difference is 2 minutes, but can be configured otherwise)
* check to see if the TGT is expired (the lifetime element),
* check that the Authenticator is not already in the TGS’s cache (for avoiding replay attacks), and
if the network address in the original request is not null, compares the source’s IP address to your network address (or within the requested list) within the TGT.


prepares two messages

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.009.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.009.jpg)

HTTP Service ticket, encrypted with HTTP Secret Service Key contains:

* your name/ID
* HTTP Service name/ID
* your network address (may be a list of IP addresses for multiple machines, or may be null if wanting to use on any machine)
* timestamp
* lifetime of the validity of the ticket, and
* HTTP Service Session Key


Encrypted with TGS session key

* HTTP Service name/ID,
* timestamp,
* lifetime of the validity of the ticket, and
* HTTP Service Session Key


At this point: 
Can decrypt second message, but not first one

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.010.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.010.jpg)

(<a href="#top">Back to top</a>)
<hr>

#### You and HTTP Service

##### You

send

* Authentication message, encrypted with HTTP Service Session key.
	* your name/ID
	* timestamp
* Still encrypted HTTP Service Ticket

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.011.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.011.jpg)

(<a href="#top">Back to top</a>)
<hr>

##### HTTP Service

* Decrypts Ticket with Secret Key to obtain HTTP Service Session Key
* Decrypts Authenticator message with HTTP Service Session Key

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.012.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.012.jpg)


Service checks:

* compares your client ID from the Authenticator to that of the Ticket,
* compares the timestamp from the Authenticator to that of the Ticket (typical Kerberos-system tolerance of difference is 2 minutes, but can be configured otherwise),
* checks to see if the Ticket is expired (the lifetime element),
* checks that the Authenticator is not already in the HTTP Server’s cache (for avoiding replay attacks), and
* if the network address in the original request is not null, compares the source’s IP address to your network address (or within the requested list) within the Ticket.

sends Authenticator message

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.013.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.013.jpg)

##### You

Decrypt authenticator message


# Lightweight Directory Access Protocol (LDAP)

Is an application protocol for:

* querying
* modifying

items in directory service providers like Active Directory

(<a href="#top">Back to top</a>)
<hr>

# Active Directory

Database based system that provides:

* authentication
* directory
* policy
* (other services in windows environment)

(<a href="#top">Back to top</a>)
<hr>


# Simple and Protected GSSAPI Negotiation Mechanism (SPNEGO)

SPNEGO provides mechanism to extends Kerberos to Web applications through standard HTTP protocol.
 

supported web interfaces:

* HDFS
* YARN
* MapReduce2
* HBase
* Oozie

(<a href="#top">Back to top</a>)
<hr>


## SPNEGO authentication

(<a href="#top">Back to top</a>)
<hr>


## Other

### Tokens

### Delegation tokens

Delegation token authentication is a two-party authentication protocol based on Java SASL Digest-MD5. The token is obtained during job submissions and submitted to the JobTracker as part of the job submission. The typical steps are:

1. User authenticates herself to the JobTracker using Kerberos.
2. User authenticates herself (using Kerberos) to the NameNode(s) that the tasks would interact with at runtime. User then gets a delegation token from each of the NameNodes.
3. User passes the tokens to the JobTracker as part of the job submission.

* All TaskTrackers running the jobs’ tasks get a copy of the tokens (via an HDFS location that is private to the user that the MapReduce daemons runs as
* Location of tokens will be exported as environmental variable.


[source](http://hortonworks.com/blog/the-role-of-delegation-tokens-in-apache-hadoop-security/)

### Job tokens


### Block access tokens


## Component-based

### HDFS extended ACL

* Read
* Write
* Execute

(<a href="#top">Back to top</a>)
<hr>

### Hive Authorization Provider


#### ATZ-NG
SQL-based authorization

If hive authorization is enabled, this is how requests will flow (with fine and coarse grained protection):

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/improvements-in-hadoop-security-22-638.jpg)

[image source](http://image.slidesharecdn.com/t-325-210a-nauroth-v8mac-140617143216-phpapp01/95/improvements-in-hadoop-security-22-638.jpg?cb=1403015785)

(<a href="#top">Back to top</a>)
<hr>

## Data encryption

Encryption is at different layers: 

* Application-level
* Database-level
* Filesystem-level
* Disk-level

### When writing a file to HDFS

1. The HDFS client calls create() to write to the new file.2. The NameNode requests the KMS to create a new EDEK using the EZK-id/version.3. The KMS generates a new DEK.4. The KMS retrieves the EZK from the key server.5. The KMS encrypts the DEK, resulting in the EDEK.6. The KMS provides the EDEK to the NameNode.7. The NameNode persists the EDEK as an extended attribute for the file metadata.8. The NameNode provides the EDEK to the HDFS client.9. The HDFS client provides the EDEK to the KMS, requesting the DEK.10. The KMS requests the EZK from the key server.11. The KMS decrypts the EDEK using the EZK.12. The KMS provides the DEK to the HDFS client.13. The HDFS client encrypts data using the DEK.14. The HDFS client writes the encrypted data blocks to HDFS.

### When reading a file from HDFS

1. The HDFS client calls open() to read a file.2. The NameNode provides the EDEK to the client.3. The HDFS client passes the EDEK and EZK-id/version to the KMS.4. The KMS requests the EZK from the key server.
5. The KMS decrypts the EDEK using the EZK.6. The KMS provides the DEK to the HDFS client.7. The HDFS client reads the encrypted data blocks, decrypting them with the DEK.

(<a href="#top">Back to top</a>)
<hr>

### Encryption zone 
Special directory whose content will be

* transparently encrypted upon write  
* transparently decrypted upon read 

(<a href="#top">Back to top</a>)
<hr>

### Keys

* has its own encryption zone key
* each file has its own data encryption key (DEK)
* HDFS only handles encrypted data encryption keys (EDEK)


clients:
decrypts EDEK, use DEK to read/write data

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/ranger_kms_keys.png)

[image source](http://hortonworks.com/wp-content/uploads/2015/06/hdfs_sec_2.png)



(<a href="#top">Back to top</a>)
<hr>

### Hadoop key management server (KMS)

performs three basic responsibilities:

* access to stored encryption zone keys 
* generates new encrypted data encryption keys (EDEK)
* decrypts EDEKs


### CLI

#### MR/PIG/Hive

* run by privileged user
* protect them at coarse grained level with StorageBasedAuthorization



# Authentication methods

| Service        | Protocol       | Methods                                                                                           |
|----------------|----------------|---------------------------------------------------------------------------------------------------|
| HDFS           | RPC            | Kerberos,delegation token                                                                         |
| HDFS           | Web UI         | SPNEGO (Kerberos) pluggable                                                                       |
| HDFS           | REST (WebHDFS) | SPNEGO (Kerberos), delegation token                                                               |
| HDFS           | REST (HttpFS)  | SPNEGO (Kerberos), delegation token                                                               |
| MapReduce      | RPC            | Kerberos, delegation token                                                                        |
| MapReduce      | WebUI          | SPNEGO (Kerberos), pluggable                                                                      |
| YARN           | RPC            | Kerberos, delegation token                                                                        |
| YARN           | WebUI          | SPNEGO (Kerberos), pluggable                                                                      |
| Hive Server 2  | Thrift         | Kerberos, LDAP (username/password)                                                                |
| Hive Metastore | Thrift         | Kerberos, LDAP (username/password)                                                                |
| Impala         | Thrift         | Kerberos, LDAP (username/password)                                                                |
| HBase          | RPC            | Kerberos, delegation token                                                                        |
| HBase          | Thrift Proxy   | None                                                                                              |
| HBase          | REST Proxy     | SPNEGO (Kerberos)                                                                                 |
| Accumulo       | RPC            | Username/password, pluggable                                                                      |
| Accumulo       | Thrift Proxy   | Username/password, pluggable                                                                      |
| Solr           | HTTP           | Based on HTTP container                                                                           |
| Oozie          | REST           | SPNEGO (Kerberos, delegation token)                                                               |
| Hue            | Web UI         | Username/password (database, PAM, LDAP), SAML, OAuth, SPNEGO (Kerberos), remote user (HTTP proxy) |
| ZooKeeper      | RPC            | Digest (username/password), IP, SASL (Kerberos), pluggable                                        |