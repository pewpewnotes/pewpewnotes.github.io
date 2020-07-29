[###](###) Elastic Search installation

Process is very similar to installation of [Logstash](Logstash)

1. get the signing key `wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -` 
2. put the things in sources.list `sudo sh -c 'echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" > /etc/apt/sources.list.d/elastic-7.x.list'`
3. `sudo apt update && sudo apt install elasticsearch`

#### Verification
simply issue `curl -X GET "http://127.0.0.1:9200"`

###  Alternate Method: 

This one is much better and should be used because its much easier.

```
curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.8.1-amd64.deb
sudo dpkg -i elasticsearch-7.8.1-amd64.deb
sudo /etc/init.d/elasticsearch start
```

If timeout occurs, check error fixing: [ElasticSearchError](ElasticSearchError)




# Note: Always use java 8 atleast for now, java8 is the best for compatibility. 
