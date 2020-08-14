```text

 _  ___ _                         _____                         
| |/ (_) |__   __ _ _ __   __ _  | ____|_ __ _ __ ___  _ __ ___ 
| ' /| | '_ \ / _` | '_ \ / _` | |  _| | '__| '__/ _ \| '__/ __|
| . \| | |_) | (_| | | | | (_| | | |___| |  | | | (_) | |  \__ \
|_|\_\_|_.__/ \__,_|_| |_|\__,_| |_____|_|  |_|  \___/|_|  |___/
                                                                
```

1. Make it accessible over the lan

Solution:
On your kibana.yml look for the line #server.host: "0.0.0.0". It will probably be commented (#).
You must remove the "#" from the line and restart your kibana service. It should allow you to access kibana from your local network ip e.g. "192.168.10.20" and make it discoverable by your other systems.

```text
`I refuse to prove that I exist,’ says Page, `for proof denies faith, and without faith I am nothing.’

`But,’ says Man, `The Babel fish is a dead giveaway, isn’t it? It could not have evolved by chance. It proves you exist, and so therefore, by your own arguments, you don’t. QED.’

`Oh dear,’ says Page, `I hadn’t thought of that,’ and promptly disappears in a puff of logic.

I think its from Hitchikers guide to galaxy, by douglas adam.
```

2. Babel could not write cache to file: /usr/share/kibana/optimize/.babel_register_cache.json due to a permission issue. Cache is disabled.

Solution:
Same thing with 5.0 Alpha 3 (even for a fresh install). Install 5.0 Alpha 3, install x-pack,
the /opt/kibana/optimize/.babelcache.json is root owned and the kibana service will not start up until it is changed to kibana owner.
