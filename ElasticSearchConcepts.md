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

Source: (Medium link)[https://medium.com/@ranjeetvimal/elasticsearch-vs-mongodb-631f410cd317]
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

