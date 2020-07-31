```text
 _____ _           _   _                                _     
| ____| | __ _ ___| |_(_) ___   ___  ___  __ _ _ __ ___| |__  
|  _| | |/ _` / __| __| |/ __| / __|/ _ \/ _` | '__/ __| '_ \ 
| |___| | (_| \__ \ |_| | (__  \__ \  __/ (_| | | | (__| | | |
|_____|_|\__,_|___/\__|_|\___| |___/\___|\__,_|_|  \___|_| |_|
                                                              

```

### Definition
***

* Elasticsearch is a real-time, distributed search and analytics engine that is Horizontally
  scalable and capable of solving a wide variety of use cases. It is core search and analytics
  engine.
  
* It is SCHEMALESS and DOCUMENT-ORIENTED.

*Q: Difference between mongo and elasticsearch*

Ans: 
Hypothetically both store data objects that have key-value pair, and allow querying that body of objects. But both come from 2 different camps and are made for different purposes.
MongoDB is a general purpose database, Elasticsearch is a distributed text search engine backed byLucene.

ElasticSearch is very good for specific task — 
indexing and searching big datasets. 
It is used when you have some secondary info about your data and you need to know actual records 
to select.

And since it’s architecture is optimized for this, it’s weaker in some other use cases.
For example, in compare to many NoSQL databases ElasticSearch is slow on adding new data.
In ElasticSearch Indexing semantics is defined on client side, so the actual indexing 
cannot be optimized as well as with real storages.

***

Source: [Medium link](https://medium.com/@ranjeetvimal/elasticsearch-vs-mongodb-631f410cd317)
* Core strength lies in searching capabilities 

  _Searching is like zooming in and finding needle in haystack, Analytics is zooming out and finding that its Haystack of yellow color_

  Meaning seeeing the overall picture is what analytics is. 
  
  It has rich client library and REST API 
  
* Horizontal scalability is ability to scale system by setting up multiple same type of machine, not adding more powerful machines.
* ElasticSearch is both horizontally and vertically scalable. 
* Lightning fast
* Fault tolerant
* Even if there is node failure or network failure, es can work pretty effectively.
* ElasticSearch is excellent with geospatial data and time series data. 
* It works excellently with [Kibana](KibanaConcepts)
* Best part about elasticsearch is that its capable of performing google like searches,
  its used in github, wikipedia etc.
* ElasticSearch can be leveraged against content aggregation platforms which basically crawl 
  and aggregate content from various places. 
  
  
## Getting started with Elastic Search

***

1. ##### Abstractions in Elastic Search

* Indexes
* Types
* Documents
* Clusters
* Nodes
* Shards and Replicas
* mapping and types
* Inverted indexes

So as to send a request using curl command
```bash
curl -XPUT -H "content-type:application/json" http://127.0.0.1:9200/catalog/_doc/1 -d 
'{
"sku": "SP000001",
"title": "Elastic search for pewpew",
"description": "UwU describes stuffs",
"author": "Akuma!",
"ISBN": "123123432432",
"price": 27.90
}' | jq .
# or you can use fx for the same.

```

### Indexes

***
An index is a container that stores and manages documents of a single type in ElasticSearch.
An index can contain document of a single type.


```text

     +----------------------------+
     | index                      |
     |    +---------------------+ |
     |    |  Type               | |
     |    |  +----------------+ | |
     |    |  |Document        | | |
     |    |  +----------------+ | |
     |    +---------------------+ |
     +----------------------------+

```

### Documents
***

Documents contain multiple fields, Each field in the json is of a particular type. 

In the product catalogue example, sku, title, description and price are basically key-value pair.

### Nodes

* Elasticsearch is a distributed system, It consists of multiple processes running across different machines in a network that communicate with the other processes.
* A node precisely corresponds to one instance of Elasticsearch process.

### Clusters

1. A cluster hosts one or more indices and is responsible for providing operations such as 
* searching
* indexing 
* Aggregations
1. A cluster is formed by one or more nodes, Every elasticsearch node is always a part of a cluster. 
2. `config/elasticsearch.yml` has various variables that can be modified.

```yaml
#
# Bootstrap the cluster using an initial set of master-eligible nodes:
#
#cluster.initial_master_nodes: ["node-1", "node-2"]
#
# For more information, consult the discovery and cluster formation module documentation.
#
#
# Bootstrap the cluster using an initial set of master-eligible nodes:
#
#cluster.initial_master_nodes: ["node-1", "node-2"]
#
# For more information, consult the discovery and cluster formation module documentation.
#
# ---------------------------------- Gateway -----------------------------------
#
# Block initial recovery after a full cluster restart until N nodes are started:
#
#gateway.recover_after_nodes: 3
#
# For more information, consult the gateway module documentation.
#
# ---------------------------------- Various -----------------------------------
#
# Require explicit names when deleting indices:
#
#action.destructive_requires_name: true

```

### Shards and replicas
***

* An index contains documents of one or more types. Shards help in distributing an index over cluster
* Shards help in dividing the documents of a single index over multiple nodes
* there is a limit to the amount of data that can be stored, which is very obvious thing if seen carefully. 
* process of dividing data amongst shards is called as sharding, its is inherent and is a way of scaling and parallelization.

#### Benefits: 
1. Better utilisation of Storage
2. Better utilization of processing powers
3. Less burden on each of the systems 

By default index are configured to have 5 shards, but one can specify the number of shards at time of creation. 

```text

     +------------------------+        +------------------------+
     | Node 1                 |        |  Node 2                |
     |    +-------+           |        |   +--------+           |
     |    |  P1   |           |        |   |  P3    |           |
     |    +-------+           |        |   +--------+           |
     |                        |        |                        |
     |         +---------+    |        |        +---------+     |
     |         |  P2     |    |        |        | P4      |     |
     |         +---------+    |        |        +---------+     |
     +------------------------+        +------------------------+

```
  Now if Node 1 goes down then its obvious that the data in p1/2 wont be available but distributed systems are expected to run inspite of any type of failures (network or hardware precisely)

  This is issue is managed and tackled by replicas, Each shard can be configured to have zero or more replica shards. Replica shards are extra copies of original primary shard and they provide high availability. 

```text
  Node 1                            Node 2
 +-------------------+          +-------------------+
 |                   |          |                   |
 | +------+          |          | +------------+    |
 | |   p1 |          |          | |  p3        |    |
 | +------+          |          | +------------+    |
 |     +-------+     |          | |   r2       |    |
 |     | p2    |     |          | +------------+    |
 |     +-------+     |          | |    r3      |    |
 | +--------+        |          | +------------+    |
 | | r1     |        |          | |      r1    |    |
 | +--------+        |          | +------------+    |
 |                   |          |                   |
 +-------------------+          +-------------------+

```

Apart from highavailability and failover, replicas allow to share the workload of search queries and aggregations. This entire distribuition is totally transparent to the user, and even querying. 

This is very much like hadoop's ecosystem. 


### Mapping and datatypes
***

* ES supports a wide vairety of datatypes for different scenarios. 
* These range from text, numbers, booleans, binary objects, arrays, objcers, nested objects, geopoints, geoshapes and many other specialized datatypes, such as IPv4 and IPv6. 

#### List of Datatypes
***

1. String Datatypes:
    * text : useful for supporting fulltext search, these are analyzed before indexing.
    * keyword : enables analytics on string fields.
2. Numeric Datatypes:
    * byte, short, integer and long: 8,16,32,64 bits respectively.
    * float and double
    * half_float
3. Complex Datatypes:
    * Array Datatype
    * Object Datatype
    * Nested Datatype
4. Other Datatypes:
    * Geo point datatype
    * Geo shape datatype
    * IP datatype
(I am too lazy to byheart or even read definitions of these things.)


### Mappings

***

```bash
curl -XPUT -H "content-type:application/json" http://127.0.0.1:9200/catalog/_doc/2 -d 
'{ 
"sku": "SP000002",
"title": "Alienware",
"description": "Hightech tech for hadoop",
"author":"pewpew Akuma",
"ISBN": "1777771281881",
"price": 20006.99,
"os":"Alpine", 
"resolution":"1920x1080" 
}' | jq .
```
