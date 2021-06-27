### Logstash installation 

So basically the methods might change in further future but then for reference steps and things like that, here is how you do it

* First get the Public keys 
  `wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -`
  
  In here 
  * -q -> quiet mode, 
  * O -> Output to 
  * - -> stdout 
  * pipe it to apt-key and add from stdin
* then add it in the source.list 
  `echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list`
* On debian you will need `apt-transport-https` package as well
* Once thats done simply go ahead and roll in action: 
 `sudo apt-get update && sudo apt-get install logstash` 
 
 If you encounter Errors just refer to Logstash error from main page.


Do note that you need java for logstash and every other dependency, for that
`sudo apt install openjdk-8-jdk`
You will have to find ways if you are on older machine, As per LogstashError, I think its better to stick to java11, which is default-jdk
