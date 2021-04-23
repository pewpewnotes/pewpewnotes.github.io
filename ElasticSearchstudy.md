```text

 _____ _           _   _      ____                      _     
| ____| | __ _ ___| |_(_) ___/ ___|  ___  __ _ _ __ ___| |__  
|  _| | |/ _` / __| __| |/ __\___ \ / _ \/ _` | '__/ __| '_ \ 
| |___| | (_| \__ \ |_| | (__ ___) |  __/ (_| | | | (__| | | |
|_____|_|\__,_|___/\__|_|\___|____/ \___|\__,_|_|  \___|_| |_|
                                                              
 ____  _             _       
/ ___|| |_ _   _  __| |_   _ 
\___ \| __| | | |/ _` | | | |
 ___) | |_| |_| | (_| | |_| |
|____/ \__|\__,_|\__,_|\__, |
                       |___/ 


```


* Index some test data

```bash
# Creation (C)
curl -X PUT "localhost:9200/customer/_doc/1?pretty" -H 'Content-Type: application/json' -d '{
'name': "John Doe"
}' | jq .
# jq . simply colorizes the output

```

Note 1: If you run the exact same command again, it shows version 2, meaning that the file is modified.

<u>Explanation</u>: This request automatically creates customer index and adds a document that has an ID of 1 and stores and indexes "name" field. The first response shows that version 1 was created. (See note)

<u>Output</u>

```json
{
  "_index": "customer",
  "_type": "_doc",
  "_id": "1",
  "_version": 2,
  "result": "updated",
  "_shards": {
    "total": 2,
    "successful": 1,
    "failed": 0
  },
  "_seq_no": 1,
  "_primary_term": 1
}

```
To obtain it again, 
```bash
# Retrieval (R)
curl "localhost:9200/customer/_doc/1" | jq .

```

Gives the result as:

```json
{
  "_index": "customer",
  "_type": "_doc",
  "_id": "1",
  "_version": 2,
  "_seq_no": 1,
  "_primary_term": 1,
  "found": true,
  "_source": {
    "name": "John Doe"
  }
}

```


There is Bulk update API as well, for that as an example download `accounts.json` file, which has about 1000 account details and they will be added as follows.


```bash
curl -H "Content-Type: application/json" -XPOST "localhost:9200/bank/_bulk?pretty&refresh" --data-binary "@accounts.json"
# To view progress
curl "localhsot:9200/_cat/indices?v"
```


<u>Output</u>: 

```bash
# Upon finishing of command


{
  "took": 2881,
  "errors": false,
  "items": [
    {
      "index": {
        "_index": "bank",
        "_type": "_doc",
        "_id": "1",
        "_version": 2,
        "result": "updated",
        "forced_refresh": true,
        "_shards": {
          "total": 2,
          "successful": 1,
          "failed": 0
        },
        "_seq_no": 1000,
        "_primary_term": 1,
        "status": 200

...

```
And upon inspecting the beautified full index

```bash
vagrant@vagrant:~$ curl "localhost:9200/_cat/indices?v" 
health status index     uuid                   pri rep docs.count docs.deleted store.size pri.store.size
yellow open bank      mXhxv0r3RyiLgiC5CYkY7Q   1   1       1000         1000    811.9kb        811.9kb
yellow open catalog   u7jc2R1mRdS7e8ISowUtdQ   1   1          2            0     12.5kb         12.5kb
yellow open vehicles  0lwv1otoQMiPSL8ueao8hw   1   1          1            0      4.4kb          4.4kb
yellow open vehibikes 0ikRWFEaT0STQuqcyy6M2A   1   1          1            0      4.4kb          4.4kb
yellow open customer  pBDz9u_KTa-w49GH5oq4dw   1   1          1            0      3.5kb          3.5kb
vagrant@vagrant:~$ 

```
### Searching
***
Searches can be performed by sending requests to `_search` endpoint, for full suite access one can use the
ElasticSearch Query DSL to specify search criteria. 

To retrieve all the documents in the `bank` index sorted by account number,

```bash

curl -X GET "localhost:9200/bank/_search?pretty" _H "Content-Type: application/json" -d '{
  "query": { "match_all": {}  },
  "sort" : [
    { "account_number": "asc" }
  ]
}'
```
Which results: 
```bash

{
  "took" : 41,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 1000,
      "relation" : "eq"
    },
    "max_score" : null,
    "hits" : [
      {
        "_index" : "bank",
        "_type" : "_doc",
        "_id" : "0",
        "_score" : null,
        "_source" : {
          "account_number" : 0,
          "balance" : 16623,
          "firstname" : "Bradshaw",
          "lastname" : "Mckenzie",
          "age" : 29,
          "gender" : "F",
          "address" : "244 Columbus Place",
          "employer" : "Euron",
          "email" : "bradshawmckenzie@euron.com",
          "city" : "Hobucken",
          "state" : "CO"
        },
        "sort" : [
          0
        ]
      },
      {
        "_index" : "bank",

        ...
```

Response also provides following crucial stuffs,

| key                | Meaning                                                 |
| :-------------:    | :-----------------------------------------------------: |
| `took`             | Time es took to run the query                           |
| `timed_out`        | Whether request was timed out or not                    |
| `shards`           | Number of shards that were searched                     |
| `max_score`        | Score of most relevant document                         |
| `hits.total.value` | how many total matching docs were found                 |
| `hits.sort`        |    Sort position of documents                           |
| `hits._score`      | Docs relevance score (not applicable on `match_all`)    |

Each search request is self contained, stateless basically so as to page through the search hits,
one must specify the from and size params in your request. 

For example, to get the hits 10 through 19,

```bash
curl -X GET "http://localhost:9200/bank/_search" -d '{
  "query": { "match_all": {} },
  "sort": [
      { "account_number": "asc" }
  ],
  "from" : 10,
  "size" : 10,
}'

```
Which basically results in 


```json

{
  "took" : 40,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 1000,
      "relation" : "eq"
    },
    "max_score" : null,
    "hits" : [
      {
        "_index" : "bank",
        "_type" : "_doc",
        "_id" : "10",
        "_score" : null,
        "_source" : {
          "account_number" : 10,
          "balance" : 46170,
          "firstname" : "Dominique",
          "lastname" : "Park",
          "age" : 37,
          "gender" : "F",
          "address" : "100 Gatling Place",
          "employer" : "Conjurica",
          "email" : "dominiquepark@conjurica.com",
          "city" : "Omar",
          "state" : "NJ"
        },
        "sort" : [
          10
        ]
      },
      {
        "_index" : "bank",

...
```

So as to perform a phrase search, instead of matching individual terms, one can use the match_phrase instead of match. 

For example, the following request will only match addresses that contain phrase mill lane: 

```bash
curl -X GET "http://localhost:9200/bank/_search" -d '{
"query": { "match_phrase": {
"address": "mill lane" 
} }
}'
```

Which results in following output: 
```json

{
  "took" : 15,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 1,
      "relation" : "eq"
    },
    "max_score" : 9.507477,
    "hits" : [
      {
        "_index" : "bank",
        "_type" : "_doc",
        "_id" : "136",
        "_score" : 9.507477,
        "_source" : {
          "account_number" : 136,
          "balance" : 45801,
          "firstname" : "Winnie",
          "lastname" : "Holland",
          "age" : 38,
          "gender" : "M",
          "address" : "198 Mill Lane",
          "employer" : "Neteria",
          "email" : "winnieholland@neteria.com",
          "city" : "Urie",
          "state" : "IL"
        }
      }
    ]
  }
}
```
To construct more complex queries, one can use a `bool` query to combine multiple query criteria, 
One can designate criteria as required (must match), desirable (should match), or undesireable (must not match)

For example, following query request searches the bank index for accounts that belong to customers who are40 years old, but excludes anyone who lives in Idaho (ID):

```json

{
  "took" : 15,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 1,
      "relation" : "eq"
    },
    "max_score" : 9.507477,
    "hits" : [
      {
        "_index" : "bank",
        "_type" : "_doc",
        "_id" : "136",
        "_score" : 9.507477,
        "_source" : {
          "account_number" : 136,
          "balance" : 45801,
          "firstname" : "Winnie",
          "lastname" : "Holland",
          "age" : 38,
          "gender" : "M",
          "address" : "198 Mill Lane",
          "employer" : "Neteria",
          "email" : "winnieholland@neteria.com",
          "city" : "Urie",
          "state" : "IL"
        }
      }
    ]
  }
}


```

Following request uses a range filter (gte and lte) to result the accounts with a balance between $20k and $30k

```bash
curl -X GET "localhost:9200/bank/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "query": {
    "bool": {
      "must": { "match_all": {} },
      "filter": {
        "range": {
          "balance": {
            "gte": 20000,
            "lte": 30000
          }
        }
      }
    }
  }
}
'
```


Output: 


```json

{
  "took" : 38,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 217,
      "relation" : "eq"
    },
    "max_score" : 1.0,
    "hits" : [
      {
        "_index" : "bank",
        "_type" : "_doc",
        "_id" : "49",
        "_score" : 1.0,
        "_source" : {
          "account_number" : 49,
          "balance" : 29104,
          "firstname" : "Fulton",
          "lastname" : "Holt",
          "age" : 23,
          "gender" : "F",
          "address" : "451 Humboldt Street",
          "employer" : "Anocha",
          "email" : "fultonholt@anocha.com",
          "city" : "Sunriver",
          "state" : "RI"
        }
      },
      {
        "_index" : "bank",
        "_type" : "_doc",
        "_id" : "102",
        "_score" : 1.0,
        "_source" : {
          "account_number" : 102,
          "balance" : 29712,
          "firstname" : "Dena",
          "lastname" : "Olson",
          "age" : 27,
          "gender" : "F",
          "address" : "759 Newkirk Avenue",
          "employer" : "Hinway",
          "email" : "denaolson@hinway.com",
          "city" : "Choctaw",
          "state" : "NJ"
        }
      },
      {
        "_index" : "bank",
        "_type" : "_doc",
        "_id" : "133",
        "_score" : 1.0,
        "_source" : {

```
### Aggregations

Elasticsearch aggregations allow us to obtain metainfo about our search result and help us in answering questions like "How many account holders are in texas?" or "whats the average balance of accounts in Tennessee"

Example: Following request uses a "terms" aggregation to group all of the accounts in bank index by state and returns the 10 states with most accounts in descending order:


```bash
curl -X GET "localhost:9200/bank/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "size": 0,
  "aggs": {
    "group_by_state": {
      "terms": {
        "field": "state.keyword"
      }
    }
  }
}
'
```

Results into: 


```json

{
  "took" : 698,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 1000,
      "relation" : "eq"
    },
    "max_score" : null,
    "hits" : [ ]
  },
  "aggregations" : {
    "group_by_state" : {
      "doc_count_error_upper_bound" : 0,
      "sum_other_doc_count" : 743,
      "buckets" : [
        {
          "key" : "TX",
          "doc_count" : 30
        },
        {
          "key" : "MD",
          "doc_count" : 28
        },
        {
          "key" : "ID",
          "doc_count" : 27
        },
        {
          "key" : "AL",
          "doc_count" : 25
        },
        {
          "key" : "ME",
          "doc_count" : 25
        },
        {
          "key" : "TN",
          "doc_count" : 25
        },
        {
          "key" : "WY",
          "doc_count" : 25
        },
        {
          "key" : "DC",
          "doc_count" : 24
        },
        {
          "key" : "MA",
          "doc_count" : 24
        },
        {
          "key" : "ND",
...
```
We can also combine the aggregations to build more complex summaries of our data, for example the following request nests an average aggregation within the previous group_by_state and calculates the average account balances for each of the states


```bash
curl -X GET "localhost:9200/bank/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "size": 0,
  "aggs": {
    "group_by_state": {
      "terms": {
        "field": "state.keyword"
      },
      "aggs": {
        "average_balance": {
          "avg": {
            "field": "balance"
          }
        }
      }
    }
  }
}
'
```

### Search format
Example is from udemy course.
```curl
GET /courses/_search
{
"query": {
"bool": {
"must":[
{"match": {"name": "Accounting"}},
{"mathc": {"room": "E3"}}
],
"must_not":[{"match": {"room": "e3"}}]
}
}
}

```
