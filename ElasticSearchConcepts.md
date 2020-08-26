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

in elasticsearch 7+ dont include the type while retrieving the mappings,

`GET /catalog/_mapping` will generate the mappign response in JSON format.

### Inverted Index

Inverted indexes are core data structures of Elasticsearch and any other system supporting full text
search. It is similar to the indexes at the back of the book, for example:

| Document ID |              Document              |
|:-----------:|:----------------------------------:|
|      1      |       It is sunday tomorrow        |
|      2      | Sunday is the last day of the week |
|      3      |        The choice is yours         |
|             |                                    |

Then the inverted index will be, 

| Term     | Frequency  | Documents  |
| :----:   | :--------: | :--------: |
| choice   | 1          | 3          |
| day      | 1          | 2          |
| is       | 3          | 1,2,3      |
| it       | 1          | 1          |
| last     | 1          | 2          |
| of       | 1          | 2          |
| sunday   | 2          | 1,2        |
| the      | 3          | 2,3        |
| tomorrow | 1          | 1          |
| week     | 1          | 2          |
| yours    | 1          | 3          |

*Note:*
* Documents were broken down and punctuations were removed and placed in lowercase
* Terms are sorted alphabetically
* Frequency column captures frequency of occurances
* third column captures occurances.

In most of scenarios, searching is extremely quick and fast, as it is without the overhead of 
parsing the text and more like a dictionary search for a word. For more than one word, union can be used to pinpoint the location.

### CRUD operations


```text
                             +-----------------+
                             |  CRUD API       |
                             +--------+--------+
                                      |
                                      |
                                      |
                                      |
                                      |
                      +----------+----------+----------------+
                      |          |          |                |
                      |          |          |                |
                      |          |          |                |
                      |          |          |                |
             +-------------+  +---------+ +-------+  +---------------+
             | Index API   |  | Update  | | GET   |  |  Delete API   |
             |             |  |         | |       |  |               |
             +-------------+  +---------+ +-------+  +---------------+

```

### Index API

1. Adding/creating a document into a type within an index of ELasticSearch is called an indexing operation.
2. It involves addding the document to the index by parsing all fields within the document and building the inverted index, this is why its called as indexing operations. 
3. There are two methods of indexing, 
    * With ID
    * Without ID

#### Indexing with ID

Basically make a PUT request of type, `/<index>/<type>/<id>` using json

```bash
curl -XPUT -H "content-type:application/json" http://127.0.0.1:9200/catalog/product/1 -d '{
"sku": "SP000001",
"title": "ElasticSearch for hadoop",
"description": "Elasticsearch for hadoop",
"author": "pewpew",
"ISBN": "1772712717",
"price": 26.99
}'

```
#### Indexing without ID
Almost same, just dont send the id :P

```json
POST /catalog/product
{
"sku": "SP000003",
"title": "Pewpew elasticsearch",
"description": "pewpew",
"author": "pewpew akuma",
"price": 54.99
}

```
In such cases ID is basically a hash string, so yay!.

### GET API

GET is useful for retrieving the document whent the id is known to you, it is like a select query basically. 

`GET /catalog/product/<hash>` 

SYNTAX: `GET /<index>/<type>/<id>`


*NOTE:* Types are not supported in ES6+

```
curl -X PUT "localhost:9200/my-index-000001/_bulk?refresh&pretty" -H 'Content-Type: application/json' -d'
{ "index":{ } }
{ "@timestamp": "2099-11-15T14:12:12", "http": { "request": { "method": "get" }, "response": { "bytes": 1070000, "status_code": 200 }, "version": "1.1" }, "message": "GET /search HTTP/1.1 200 1070000", "source": { "ip": "127.0.0.1" }, "user": { "id": "kimchy" } }
{ "index":{ } }
{ "@timestamp": "2099-11-15T14:12:12", "http": { "request": { "method": "get" }, "response": { "bytes": 1070000, "status_code": 200 }, "version": "1.1" }, "message": "GET /search HTTP/1.1 200 1070000", "source": { "ip": "10.42.42.42" }, "user": { "id": "elkbee" } }
{ "index":{ } }
{ "@timestamp": "2099-11-15T14:12:12", "http": { "request": { "method": "get" }, "response": { "bytes": 1070000, "status_code": 200 }, "version": "1.1" }, "message": "GET /search HTTP/1.1 200 1070000", "source": { "ip": "10.42.42.42" }, "user": { "id": "elkbee" } }
'
```



### Shards 
Shards are a lot like indices, they are basically containers. 
Data in Elasticsearch is organized into indices.
Each index is made up of one or more shards.
Each shard is an instance of a Lucene index,
which you can think of as a self-contained search engine that indexes and handles queries for a subset of the data in an Elasticsearch cluster.

As data is written to a shard, it is periodically published into new immutable 
Lucene segments on disk, and it is at this time it becomes available for querying.


### Why is ElasticSearch so AWESOME!! (it really is)

***
In elasticsearch most basic unit of storage is a shard, which is basically logical abstraction of data, like you can just not care about where in the universe data is stored, if its on shard its searchable and you can use it. But the engine, lucene engine makes things a bit different, in elasticsearch shard is a lucene index and each lucene index and each lucene index consists of various lucene segments. 


```text

            Index
+-----------------------------------+
|                                   |                        +------------------------+
|                                   |                        |  +----+      +-----+   |
| +------------+  +--------------+  |                        |  |    |      |     |   |
| |            |  |              |  | Each shard is a lucene |  |  1 |      | 2   |   |
| |            |  |              |-------------------------->|  +----+      +-----+   |
| |  shard 1   |  |  shard 2     |  |      index             |                        |
| |            |  |              |  |                        |  +----+      +-----+   |
| +------------+  +--------------+  |                        |  |    |      |     |   |
|                                   |                        |  |  3 |      | 4   |   |
|                                   |                        |  +----+      +-----+   |
|                                   |                        +------------------------+
|                                   |                      A single shard of ES in lucene's
+-----------------------------------+                              Structure
      Index structure in ES

```


The concept behind segmentation is that whenever a new document is created they are written in new segments,
if they are new,there is no need for modification of any existing segment. 
Upon attempt to deletion, it is flagged as deleted in its original segment, this means it never gets physically deleted from segment. 

As far as updating goes, the previous version is marked as delted in the previous segment and the updated version is kept under the same Document ID in the current segment.

#### Lucene reopen
when Lucene reopen is called, will make the data accumulated available for search. Although the latest data is made available for search, it <u>doesn't</u> guarantee the persistence of the data or that it is not written to the disk.

Lucene commits the data to be safe, for each of the commits the data from different segments is merged and pushed to the disk, making the data persistent. Although commits are ideal way to persist data, the issue is that each commit operation is <u>Resource Expensive</u> Each commit has its own I/O operatios and R/w cycles.

Now here comes the genius of Elasticsearch, 
### Translog
Elastic search addresses the issue of persistance taking a different approach, It introduces a translog(transaction log) in every shard, New documents indexed are passed to this transaction log and an in memory buffer.


```text                                       
                                +--------------------------------------------+
                                |             +-------------+                |
                                |    |------->|             |                |
 +--------+                     |    |        |  Translog   |                |
+--------+|                     |    |        |             |                |
|        || New documennts      |    |        +-------------+                |
|        ||---------------------|--->|                                       |
|        ||    indexing         |    |                                       |
|        ||                     |    |        +-------------+                |
|        |+                     |    |        | In memory   |                |
+--------+                      |    |        |             |                |
                                |    |------->|  Buffer     |                |
                                |             |             |                |
                                |             +-------------+                |
                                |                                            |
                                +--------------------------------------------+
                                                   Shard

```
In elasticsearch the _refresh operation is set to be executed every second by default, during this the in-memory buffer contents is copied to a newly created segment.

Translog handles persistence very nicely, transog pertains to the physical disk memory, It is fsynced and safe, thus we obtain both durability and persistence even for non committed data. In case something bad happens, transaction log can be restored. 


### Searching

* basics of text analysis
* Searching from structured data
* Writing compound queries
* Searching from full text

****

#### Analyzers

Job of analyzer is to take the documents and each field of the document and extract, terms from them. These terms make the index searchable, that is, it ca help us find out which documents contain particular search terms

Core task of the analyzer is to parse the document fields and build the actual index.
Every field of text type needs to be analyzed before the document is indexed, this process of analysis is what maes the documents searchanle by an search term that is used at the time of searching. 
Analyzers can be configured of a per field basis, that is it is possible to have two fields of the type text within the same document, each one using the different analyzers. 


```text
+--------------------------------------------------------------+
| +----------------------+   +-------------------+             |
| |                      |   |                   |             |
| |  Character filters   +--->   token filters   |-----|       |
| |                      |   |                   |     |       |
| +----------------------+   +-------------------+     |       |
| +------------+                                       |       |
| |            |     Elasticsearch Analyzer            |       |
| |            |                                       |       |
| |   Token    |                                       |       |
| |  filters   |                                       |       |
| |            |                                       |       |
| |            |                                       v       |
| |            |<---------------------------------------       |
| +------------+                                               |
+--------------------------------------------------------------+
```

1. Character filters
A character filter works on a stream of characters from the input field; each character filter can add, remove, or change the characters in the input field.
ElasticSearhc ships with builtin charcater filters and also allows us to create our own filters.


for example, to create a custom filter which allows: 
:) -> _smile_
:( -> _sad_
:D -> _laugh_

```json
"char_filter": {
"my-char-filter": {
"type": "mapping",
"mappings": [
":) => _smile_",
":( => _sad_",
":D => _laugh_"
    ]
  }
}
```

2. Tokenizer

An analyzer ahs exactly one tokenizer, its reponsibility is to take a stream of characters and generate a stream of tokens. These tokens are then used in building the inverted index, it is roughlt equivalent to a word.

```text
Word Oriented Tokenizers
edit

The following tokenizers are usually used for tokenizing full text into individual words:

Standard Tokenizer
    The standard tokenizer divides text into terms on word boundaries, as defined by the Unicode Text Segmentation algorithm. It removes most punctuation symbols. It is the best choice for most languages. 
Letter Tokenizer
    The letter tokenizer divides text into terms whenever it encounters a character which is not a letter. 
Lowercase Tokenizer
    The lowercase tokenizer, like the letter tokenizer, divides text into terms whenever it encounters a character which is not a letter, but it also lowercases all terms. 
Whitespace Tokenizer
    The whitespace tokenizer divides text into terms whenever it encounters any whitespace character. 
UAX URL Email Tokenizer
    The uax_url_email tokenizer is like the standard tokenizer except that it recognises URLs and email addresses as single tokens. 
Classic Tokenizer
    The classic tokenizer is a grammar based tokenizer for the English Language. 
Thai Tokenizer
    The thai tokenizer segments Thai text into words. 

Partial Word Tokenizers
edit

These tokenizers break up text or words into small fragments, for partial word matching:

N-Gram Tokenizer
    The ngram tokenizer can break up text into words when it encounters any of a list of specified characters (e.g. whitespace or punctuation), then it returns n-grams of each word: a sliding window of continuous letters, e.g. quick → [qu, ui, ic, ck]. 
Edge N-Gram Tokenizer
    The edge_ngram tokenizer can break up text into words when it encounters any of a list of specified characters (e.g. whitespace or punctuation), then it returns n-grams of each word which are anchored to the start of the word, e.g. quick → [q, qu, qui, quic, quick]. 

Structured Text Tokenizers
edit

The following tokenizers are usually used with structured text like identifiers, email addresses, zip codes, and paths, rather than with full text:

Keyword Tokenizer
    The keyword tokenizer is a “noop” tokenizer that accepts whatever text it is given and outputs the exact same text as a single term. It can be combined with token filters like lowercase to normalise the analysed terms. 
Pattern Tokenizer
    The pattern tokenizer uses a regular expression to either split text into terms whenever it matches a word separator, or to capture matching text as terms. 
Simple Pattern Tokenizer
    The simple_pattern tokenizer uses a regular expression to capture matching text as terms. It uses a restricted subset of regular expression features and is generally faster than the pattern tokenizer. 
Char Group Tokenizer
    The char_group tokenizer is configurable through sets of characters to split on, which is usually less expensive than running regular expressions. 
Simple Pattern Split Tokenizer
    The simple_pattern_split tokenizer uses the same restricted regular expression subset as the simple_pattern tokenizer, but splits the input at matches rather than returning the matches as terms. 
Path Tokenizer
    The path_hierarchy tokenizer takes a hierarchical value like a filesystem path, splits on the path separator, and emits a term for each component in the tree, e.g. /foo/bar/baz → [/foo, /foo/bar, /foo/bar/baz ]. 



```

