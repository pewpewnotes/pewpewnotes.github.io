### Installation 
***

``sudo apk add shadow postgresql postgresql-contrib postgresql-client ``
(install bash as well if missing)
```
useradd -m -G wheel postgres
su - postgres
initdb -d Data
pg_ctl start -d Data
```

psql -At -c 'SELECT version();'
should spoyut some data


if it fails: 


On alpine Machine. 

init.d system I suppose

Patrick Lindeman wrote:



>> I'm trying to start my postgres server and it gives me the following
>> errror
>>
>> FATAL:  could not create lock file
>> "/var/run/postgresql/.s.PGSQL.5432.lock":
>> Permission denied
>>



This looks like an Ubuntu or similar install. I believe the standard
PostgreSQL default for unix_socket_directory is /tmp but this can be
changed at build-time. The build Ubuntu provides defaults to
/var/run/postgresql. Other Debian-based distros may do something similar.



In any case, the normal PostgreSQL install for your distro should start
fine via the init scripts such as (Ubuntu style):



sudo /etc/init.d/postgresql-8.2 start



But if you are trying a to run an instance of the PostgreSQL server
owned by your local user, you need to ensure that the unix socket
directory is writable by the user that owns the PostgreSQL server
process. Try:



unix_socket_directory='/tmp'



Cheers,
Steve


Or else

* `chown -R postgres:postgres /var/run/postgresql`
