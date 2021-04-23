[###](###) == Installation ==

Listerally same process, annoyingly similar. :P

1. `wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -`
2. `echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list`
3. `sudo apt-get update && sudo apt-get install kibana`


### Alternate Installation

This one works very well and brilliantly, also note that it used node,
ITS VERY SLOW, so alwasy be cautious with it. Give it good 30 mins to boot xD

```
curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-7.8.1-linux-x86_64.tar.gz
tar xzvf kibana-7.8.1-linux-x86_64.tar.gz
cd kibana-7.8.1-linux-x86_64/
./bin/kibana
```

Sometimes the server is slow so be patient and it will be alright. 

As a quick note, you can controlC the download and use wget -c to resume from same spot. 
