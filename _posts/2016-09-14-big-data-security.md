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

## Knox

## Ranger

### Key management service

stores keys in a file-based Java keystore.

Main functions:

* Key management: create, update + delete keys (via Web UI or REST API)
* Access control policies: manages access control policies.
* Audit

## Kerberos
Based on awesome tutorial from [roguelynn](http://www.roguelynn.com/words/explain-like-im-5-kerberos/).<br>
Name comes from three-headed dog of Hades, who protected access to the underworld.


### Ticket
Goal: You need a ticket (on local machine)

As long as it is valid, you can access the requested service that is within Kerberos realm. Avoids re-entering password.

### Principal
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


### Kerberos realm

Defines what Kerberos manages in terms of who can access what.
Both your machine and requested service live in this realm.

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/kerberos_realm.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.001.jpg)


### Key Distribution Center

Stores all secret keys for users and services in database.
relies on symmetric-key cryptography

#### Authentication Server

#### Ticket Granting Server

### Requesting access

* each interaction contains 2 messages: one you can encrypt, the other one you cannot.
* requested service/machine and KDC never communicate directly
* The KDC stores all secret keys for users and services in database
* Secret keys are: password + salt that are hashed


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


#### You and HTTP Service

##### You
send

* Authentication message, encrypted with HTTP Service Session key.
	* your name/ID
	* timestamp
* Still encrypted HTTP Service Ticket

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/Kerb.011.jpg)

[image source](http://www.roguelynn.com/assets/images/Kerb.011.jpg)

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

# Other

## JMX architecture

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/jmx.png)

[image source](https://www.safaribooksonline.com/library/view/cassandra-the-definitive/9781491933657/assets/ctdg_1001.png)

(<a href="#top">Back to top</a>)
<hr>

## Thrift 

Thrift provides a great framework for developing and accessing remote services. It allows developers to create services that can be consumed by any application that is written in a language that there are Thrift bindings for (which is...just about every mainstream one, and more).

It manages:

* serialization of data to and from a service
* the protocol that describes a method invocation, response, etc
* Thrift uses TCP (not sure if UDP is/will be supported) and so a given service is bound to a particular port.
 
(<a href="#top">Back to top</a>)
<hr>

### Networking stack

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/thrift_networking_stack.png)

[image source](http://3.bp.blogspot.com/-MuIbUycK0eI/Va6a70JxwjI/AAAAAAAABRo/_UGabAOfkNo/s320/thrift.png)

(<a href="#top">Back to top</a>)
<hr>


### Thrift server
![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata//thrift-server.png)

[image source](http://2.bp.blogspot.com/-gh4wM0lmruQ/Va6qyamHMbI/AAAAAAAABR4/XV9y3L-wgDg/s400/thrift-server.png)

(<a href="#top">Back to top</a>)
<hr>


### Comparison with SOAP and REST

![{{base}}/images/lambda_architecture.png]({{base}}/images/bigdata/rest_soap_thrift.png)

[image source](http://nordicapis.com/microservice-showdown-rest-vs-soap-vs-apache-thrift-and-why-it-matters/)

Analogy sending a letter using REST, SOAP, and Thrift: [http://nordicapis.com/microservice-showdown-rest-vs-soap-vs-apache-thrift-and-why-it-matters/](http://nordicapis.com/microservice-showdown-rest-vs-soap-vs-apache-thrift-and-why-it-matters/).

ZooKeeper can be used to store Thrift service location information and manage its state ([source](https://www.chrismoos.com/2011/05/25/thrift-and-zookeeper/)).

Further reading: [link](http://thatguyfromthisworld.blogspot.de/2015/07/lets-understand-apache-thrift.html)

(<a href="#top">Back to top</a>)
<hr>

## System of record vs system of engagement

### System of record

“Systems of Record” are the ERP-type systems we rely on to run our business (financials, manufacturing, CRM, HR).  They have to be “ correct” and “integrated” so all data is consistent. And they were traditionally designed for people who have no choice but to use them.
[source](http://www.forbes.com/sites/joshbersin/2012/08/16/the-move-from-systems-of-record-to-systems-of-engagement/#6a27371f50c4)

### System of engagement

“Systems of Engagement” are systems which are used directly by employees for “ sticky uses” – like email, collaboration systems, and new social networking and learning systems.  They “engage” employees.
[source](http://www.forbes.com/sites/joshbersin/2012/08/16/the-move-from-systems-of-record-to-systems-of-engagement/#6a27371f50c4)

![{{base}}/images/bigdata/lambda_architecture.png]({{base}}/images/bigdata/system_of_record.jpg)

[image source](http://image.slidesharecdn.com/palmercmomg102813-131128113447-phpapp02/95/supporting-knowledge-workers-with-adaptive-case-management-8-638.jpg?cb=1385638592)


## Schema-on-read vs schema-on-write

## Data governance 

