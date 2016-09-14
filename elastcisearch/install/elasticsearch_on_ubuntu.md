Install Elasticsearch In Ubuntu
=====
# Introduction

Elasticsearch is an Open Source Search Server based on Lucene, A platform for RESTful search and analytics. 

## Features

- Full Text search
- Real Time Data
- Reduce chances of data loss
- Indexing

## Version 

2.3.3


## Before Install Elasticsearch

- Install the OpenJDK runtime supplied by Ubuntu.
- Install the Elasticsearch recommended Java runtime, Oracle Java.

### Install OpenJDK runtime


#### openJDK
	
	apt-get install openjdk-6-jre.

#### Add java repository to ubuntu

	add-apt-repository -y ppa:webupd8team/java
	
Update OS

	apt-get update
	
Install Oracle-Java

	apt-get install oracle-java8-installer
	
Test your Java installation

	java -version
	
輸出顯示

```
java version "1.8.0_66"
Java(TM) SE Runtime Environment (build 1.8.0_66-b17)
Java HotSpot(TM) 64-Bit Server VM (build 25.66-b17, mixed mode)
```

http://www.ubuntuupdates.org/package/webupd8_java/wily/main/base/oracle-java8-installer

## Install Elasticsearch

### Add Elasticsearch repository

參考 [Elasticsearch Repositories](https://www.elastic.co/guide/en/elasticsearch/reference/current/setup-repositories.html) 

#### Download and install the Public Signing Key

	wget -qO - https://packages.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -

#### Update Package

	echo "deb http://packages.elastic.co/elasticsearch/2.x/debian stable main" | sudo tee -a /etc/apt/sources.list.d/elasticsearch-2.x.list

#### Install Elasticsearch

	sudo apt-get update && sudo apt-get install elasticsearch
	
## Config Elasticsearch 

### Path & Files

Open Elasticsearch Configuration file and edit as per requirement

	vim /etc/elasticsearch/elasticsearch.yml
	
Search for `network.host` and replace  to `network.host: localhost`

### Remove Elasticsearch Public Access

編輯設定檔

	vim /etc/elasticsearch/elasticsearch.yml

設定伺服器監聽的 host	

`network.bind_host: localhost`  

插入下面一行設定來啟用 to disable dynamic scripts: 

`script.disable_dynamic: true`

執行下面命令重新啟動

	service elasticsearch restart

## Running as a Service

Configure Elasticsearch to automatically start during bootup. If your distribution is using SysV init, then you will need to run:

	update-rc.d elasticsearch defaults 95 10
	
Restart elasticsearch services

	/etc/init.d/elasticsearch restart
	
### RPM based distributions

#### Using chkconfig

The init script is located at `/etc/init.d/elasticsearch`, where as the configuration file is placed at `/etc/sysconfig/elasticsearch`.

	sudo /sbin/chkconfig --add elasticsearch
	sudo service elasticsearch start
	
#### Using systemd

configuration file is also placed at `/etc/sysconfig/elasticsearch`

	sudo /bin/systemctl daemon-reload
	sudo /bin/systemctl enable elasticsearch.service
	sudo /bin/systemctl start elasticsearch.service

**
Also note that changing the MAX_MAP_COUNT setting in `/etc/sysconfig/elasticsearch` does not have any effect, you will have to change it in `/usr/lib/sysctl.d/elasticsearch.conf` in order to have it applied at startup.
**

## Test Elasticsearch

Test your Elastcsearch is working properly or not!

	curl -X GET 'http://localhost:9200'
	
Sample output message

```
{
  "name" : "Mr. Wu",
  "cluster_name" : "elasticsearch",
  "version" : {
    "number" : "2.1.0",
    "build_hash" : "72cd1f1a3eee09505e036106146dc1949dc5dc87",
    "build_timestamp" : "2015-11-18T22:40:03Z",
    "build_snapshot" : false,
    "lucene_version" : "5.3.1"
  },
  "tagline" : "You Know, for Search"
}
```

There will be two main configuration files: `elasticsearch.yml` and `logging.yml`, configuration files are found in `/etc/elasticsearch`.


## Install Elasticsearch kopf

A gui Admin panel for Elastcisearch

	/usr/share/elasticsearch/bin/plugin install lmenezes/elasticsearch-kopf
	
To get health status of Cluster.

	curl -XGET 'http://localhost:9200/_cluster/health?pretty=true'

	
## Using Elasticsearch 

The Elasticsearch REST APIs are exposed using JSON over HTTP.  
which responds to the usual CRUD commands: Create, Read, Update, and Destroy.

### Basic usage

#### add

- "tutorial" is index of the data in Elasticsearch.
- "helloworld" is the type.
- "1" is the id of our entry under the above index and type.

新增資料

	curl -X POST 'http://localhost:9200/tutorial/helloworld/1' -d '{ "message": "Hello World!" }'

get response
	
	{"_index":"tutorial","_type":"helloworld","_id":"1","_version":1,"_shards":{"total":2,"successful":1,"failed":0},"created":true}
	
#### query

	curl -X GET 'http://localhost:9200/tutorial/helloworld/1'
	
get response

	{"_index":"tutorial","_type":"helloworld","_id":"1","_version":1,"found":true,"_source":{ "message": "Hello World!" }}
	
讓輸出更好閱讀，加上 `?pretty=true`

	curl -X GET 'http://localhost:9200/tutorial/helloworld/1?pretty=true'
	
#### delete

	curl -XDELETE 'http://localhost:9200/tutorial/helloworld/1'
	
get response 

	{"found":true,"_index":"tutorial","_type":"helloworld","_id":"1","_version":2,"_shards":{"total":2,"successful":1,"failed":0}}
	
### Document APIs

This section describes the following CRUD APIs:

Single document APIs

- Index API
- Get API
- Delete API
- Update API

Multi-document APIs

- Multi Get API
- Bulk API

### Search APIs
	