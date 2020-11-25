find / -size +1G -mtime +180 -type f -print

```
I was experiment the same issue some weeks ago, and this procedure was solve the problem.

First, search where is the most space use

    for i in /*; do echo $i; find $i |wc -l; done
Pay attention when some directories take more time to be readed. In my case was the /var/ where take more time searching.

So run that:

    for i in /var/*; do echo $i; find $i |wc -l; done
After that, run the same command to /var/log/* and detect a lot small files on the squid3 logs.

After run an rm -rfv /var/log/squid3/access.log* (and restart squid3) the problem was solved, and the IUSE% change from 100 to 13.

```
