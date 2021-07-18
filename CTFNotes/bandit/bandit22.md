### Bandit 22
***
```
bandit22@bandit:/etc/cron.d$ ls
cronjob_bandit15_root  cronjob_bandit17_root  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  cronjob_bandit25_root
bandit22@bandit:/etc/cron.d$ cat cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
bandit22@bandit:/etc/cron.d$ cat /usr/bin/cron
cronjob_bandit15_root.sh   cronjob_bandit22.sh        cronjob_bandit24.sh        cronjob_bandit25_root.sh~  crontab                    
cronjob_bandit17_root.sh   cronjob_bandit23.sh        cronjob_bandit25_root.sh   cronjob_bandit25_root.sz~  
bandit22@bandit:/etc/cron.d$ cat /usr/bin/cron
cronjob_bandit15_root.sh   cronjob_bandit22.sh        cronjob_bandit24.sh        cronjob_bandit25_root.sh~  crontab                    
cronjob_bandit17_root.sh   cronjob_bandit23.sh        cronjob_bandit25_root.sh   cronjob_bandit25_root.sz~  
bandit22@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh 
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
bandit22@bandit:/etc/cron.d$ echo I am bandit22 | md5sum | cut -d ' ' -f 1
9df51ed43d5675fe899bccaa84604751
bandit22@bandit:/etc/cron.d$ cat /tmp/9df51ed43d5675fe899bccaa84604751
cat: /tmp/9df51ed43d5675fe899bccaa84604751: No such file or directory
bandit22@bandit:/etc/cron.d$ cat /tmp/9df51ed43d5675fe899bccaa84604751
cat: /tmp/9df51ed43d5675fe899bccaa84604751: No such file or directory
bandit22@bandit:/etc/cron.d$ myname=$(whoami)
bandit22@bandit:/etc/cron.d$ mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
bandit22@bandit:/etc/cron.d$ 
bandit22@bandit:/etc/cron.d$ echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"
Copying passwordfile /etc/bandit_pass/bandit22 to /tmp/8169b67bd894ddbb4412f91573b38db3
bandit22@bandit:/etc/cron.d$ 
bandit22@bandit:/etc/cron.d$ cat /etc/bandit_pass/$myname > /tmp/$mytarget
bandit22@bandit:/etc/cron.d$ whoami
bandit22
bandit22@bandit:/etc/cron.d$ cat /tmp/8169b67bd894ddbb4412f91573b38db3
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
bandit22@bandit:/etc/cron.d$ 
bandit22@bandit:/etc/cron.d$ echo I am bandit23 | md5sum | cut -d ' ' -f 1
d7387859980fe85c84d68d50eedd8598
bandit22@bandit:/etc/cron.d$ cat /tmp/d7387859980fe85c84d68d50eedd8598
cat: /tmp/d7387859980fe85c84d68d50eedd8598: No such file or directory
bandit22@bandit:/etc/cron.d$ myname
-bash: myname: command not found
bandit22@bandit:/etc/cron.d$ echo $myname
bandit22
bandit22@bandit:/etc/cron.d$ echo $mytarget
8169b67bd894ddbb4412f91573b38db3
bandit22@bandit:/etc/cron.d$ echo "I am user bandit22" | md5sum | cut -d ' ' -f 1
8169b67bd894ddbb4412f91573b38db3
bandit22@bandit:/etc/cron.d$ echo "I am user bandit23" | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
bandit22@bandit:/etc/cron.d$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
bandit22@bandit:/etc/cron.d$ 


``` 
