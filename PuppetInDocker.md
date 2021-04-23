```text
 ____                         _                     _ 
|  _ \ _   _ _ __  _ __   ___| |_    __ _ _ __   __| |
| |_) | | | | '_ \| '_ \ / _ \ __|  / _` | '_ \ / _` |
|  __/| |_| | |_) | |_) |  __/ |_  | (_| | | | | (_| |
|_|    \__,_| .__/| .__/ \___|\__|  \__,_|_| |_|\__,_|
            |_|   |_|                                 
 ____             _             
|  _ \  ___   ___| | _____ _ __ 
| | | |/ _ \ / __| |/ / _ \ '__|
| |_| | (_) | (__|   <  __/ |   
|____/ \___/ \___|_|\_\___|_|   
                                

```


### Installing Stuffs

1. Install docker (duh!)
2. Install composer, might come in handy anyways.
3. pull the following images
```bash
    puppet/puppet-agent-ubuntu
    puppet/puppetserver
    puppet/puppetdb
    puppet/puppetdb-postgres
```
4. Create a docker network, this is to facilitate connection.
```bash
docker network create puppet
```
5. So as to create the puppet server,
```bash
docker run --net puppet --name puppet --hostname puppet-server puppet/puppetserver
```
6. Create the agent,
```bash
docker run --net puppet --name puppet-client --hostname puppet-client puppet/puppet-agent-ubuntu agent --verbose --no-daemonize --summarize
```
7. To install puppet db, clone the repo `https://github.com/puppetlabs/puppetdb` goto docker and then `docker-compose up` to obtain the puppetdb image.
8. 

