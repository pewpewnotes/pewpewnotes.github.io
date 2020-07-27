[###](###) Elastic Search installation

Process is very similar to installation of [Logstash](Logstash)

1. get the signing key `wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -` 
2. put the things in sources.list `sudo sh -c 'echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" > /etc/apt/sources.list.d/elastic-7.x.list'`
3. `sudo apt update && sudo apt install elasticsearch`

#### Verification
simply issue `curl -X GET "http://127.0.0.1:9200"`
