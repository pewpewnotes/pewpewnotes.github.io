### ElasticSearch Errors

1. The most prominent issue I experienced was this: 
   
`
-- Unit elasticsearch.service has begun starting up.         
Jul 27 09:03:45 vagrant systemd[1]: elasticsearch.service: Start operation timed out. Terminating.
Jul 27 09:03:46 vagrant systemd[1]: elasticsearch.service: Failed with result 'timeout'.
Jul 27 09:03:46 vagrant systemd[1]: Failed to start Elasticsearch.
\-- Subject: Unit elasticsearch.service has failed
\-- Defined-By: systemd                      
\-- Support: http://www.ubuntu.com/support
\--                     
\-- Unit elasticsearch.service has failed.
\--                       
\-- The result is RESULT.                                         
`

Timeout error, well the timeout for elasticsearch initiation is given as 1 minutes or something, which is not really enough to fix that we gotta modify the entry.
Create service drop-in configuration directory.

`$ sudo mkdir /etc/systemd/system/elasticsearch.service.d`
Then 
`echo -e "[Service]\nTimeoutStartSec=300" | sudo tee /etc/systemd/system/elasticsearch.service.d/startup-timeout.conf`
After that, 
Reload systemd manager configuration.

`$ sudo systemctl daemon-reload` 

Verify ` sudo systemctl show elasticsearch | grep ^Timeout`
and then restart by: 
`sudo systemctl start elasticsearch`
This fixes it, and ofc you must check the journalctl -xe to make sure its the same error.




I like this quote:
"The result is result xD" 

        ~Systemd
        
        


For <u>renaming</u> your index you can use Elasticsearch Snapshot module.

First you have to take snapshot of your index.while restoring it you can rename your index.
```json
    POST /_snapshot/my_backup/snapshot_1/_restore
    {
     "indices": "jal",
     "ignore_unavailable": "true",
     "include_global_state": false,
     "rename_pattern": "jal",
     "rename_replacement": "jal1"
     }
```
rename_replacement :-New indexname in which you want backup your data.

