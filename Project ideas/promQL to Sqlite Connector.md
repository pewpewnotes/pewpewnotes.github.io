Prometheus is used extensively with metrics and for querying along with for setting up of alerting. One of the annoying thing is lack of sql like commands to deal with the output.
The script/code is supposed to bridge that gap in general with a sqlite dumping.

Idea here is that we will query the given prometheus server and then go ahead and convert the resulting json into a table on the basis of labels and then use the queries to perform operations on the table and then get their output.

The problem however is the value, how are we going to handle the values and how are they going to be combined? 

for instance

```
node_network_up{}
```

Leads to following result


|Element|Value|
|---|---|
|node_network_up{device="br-3327832c3dee",instance="node-exporter:9100",job="node"}|1|
|node_network_up{device="br-488b0d8cf464",instance="node-exporter:9100",job="node"}|0|
|node_network_up{device="br-48bb53fc044f",instance="node-exporter:9100",job="node"}|0|
|node_network_up{device="docker0",instance="node-exporter:9100",job="node"}|0|
|node_network_up{device="enp45s0",instance="node-exporter:9100",job="node"}|0|
|node_network_up{device="lo",instance="node-exporter:9100",job="node"}|0|
|node_network_up{device="veth4ce3dcf",instance="node-exporter:9100",job="node"}|1|
|node_network_up{device="veth53278c5",instance="node-exporter:9100",job="node"}|1|
|node_network_up{device="veth9827718",instance="node-exporter:9100",job="node"}|1|
|node_network_up{device="vethbc86659",instance="node-exporter:9100",job="node"}|1|
|node_network_up{device="vethd1d1ddf",instance="node-exporter:9100",job="node"}|1|
|node_network_up{device="virbr0",instance="node-exporter:9100",job="node"}|0|
|node_network_up{device="virbr2",instance="node-exporter:9100",job="node"}|0|
|node_network_up{device="wlan0",instance="node-exporter:9100",job="node"}|1|
|node_network_up{device="ztmjfh6oy2",instance="node-exporter:9100",job="node"}|0|

The element can be broken into components on the basis of the labels 

|device| instance | job | values |
| --- | --- | --- | --- | --- |
|wlan0 | node-exporter | node | 1 |

Something like this.

Now let's say we want to combine, 

```
node_disk_info{}
```

|Element|Value|
|---|---|
|node_disk_info{device="nvme0n1",instance="node-exporter:9100",job="node",major="259",minor="0",model="",path="",revision="",serial="",wwn=""}|1|
|node_disk_info{device="sda",instance="node-exporter:9100",job="node",major="8",minor="0",model="",path="",revision="",serial="",wwn=""}|1|

again, this can be dumped as a table, 

|device | instance | job | major | minor | model | path | revision | serial | wwn | values |
| --- | --- | --- | --- | --- | ---| --- | --- | ---| --- |
| nvme | pew | pew | pew | pew | pew | pew | pew | pew | 0 |

now, these two table can be combined with the usual sql model based queries, and the value operation can be defined separately, for instance, `+ / - * || && U I *`
which will be evaluated and presented in the common way. 

This is something that is already been done by tsdb then why are we trying to replicate the same? Well the combining of query from multiple to multiple is not really possible on promql and this should give us some flexibility on that. Having an extensive querying on promql will help. Well, this might be a fun lil project to do in golang.

***

### Beginning with the project

1. What all am I going to need? 
- golang
- nvim
- sqlite connector
- json parser
- mapping 
2. How to use them? 
We will figure it out along the way.
3. Test infra?
We already have a small infrastructure with some metrics for our testing
