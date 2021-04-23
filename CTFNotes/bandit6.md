### Bandit 6
***
The password for the next level is stored somewhere on the server and has all of the following properties:

* owned by user bandit7
* owned by group bandit6
* 33 bytes in size

```
bandit6@bandit:/$ find -type f -size 33c -group bandit6
find: ‘./root’: Permission denied
find: ‘./home/bandit28-git’: Permission denied
find: ‘./home/bandit30-git’: Permission denied
find: ‘./home/bandit5/inhere’: Permission denied
find: ‘./home/bandit27-git’: Permission denied
find: ‘./home/bandit29-git’: Permission denied
find: ‘./home/bandit31-git’: Permission denied
find: ‘./lost+found’: Permission denied
find: ‘./etc/ssl/private’: Permission denied
./etc/bandit_pass/bandit6
find: ‘./etc/polkit-1/localauthority’: Permission denied
find: ‘./etc/lvm/archive’: Permission denied
find: ‘./etc/lvm/backup’: Permission denied
find: ‘./sys/fs/pstore’: Permission denied
find: ‘./proc/tty/driver’: Permission denied
find: ‘./proc/8376/task/8376/fdinfo/6’: No such file or directory
find: ‘./proc/8376/fdinfo/5’: No such file or directory
find: ‘./cgroup2/csessions’: Permission denied
find: ‘./boot/lost+found’: Permission denied
find: ‘./tmp’: Permission denied
find: ‘./run/lvm’: Permission denied
find: ‘./run/screen/S-bandit16’: Permission denied
find: ‘./run/screen/S-bandit22’: Permission denied
find: ‘./run/screen/S-bandit4’: Permission denied
find: ‘./run/screen/S-bandit31’: Permission denied
find: ‘./run/screen/S-bandit24’: Permission denied
find: ‘./run/screen/S-bandit21’: Permission denied
find: ‘./run/screen/S-bandit0’: Permission denied
find: ‘./run/screen/S-bandit25’: Permission denied
find: ‘./run/screen/S-bandit23’: Permission denied
find: ‘./run/screen/S-bandit20’: Permission denied
find: ‘./run/shm’: Permission denied
find: ‘./run/lock/lvm’: Permission denied
find: ‘./var/spool/bandit24’: Permission denied
find: ‘./var/spool/cron/crontabs’: Permission denied
find: ‘./var/spool/rsyslog’: Permission denied
find: ‘./var/tmp’: Permission denied
find: ‘./var/lib/apt/lists/partial’: Permission denied
find: ‘./var/lib/polkit-1’: Permission denied
find: ‘./var/log’: Permission denied
find: ‘./var/cache/apt/archives/partial’: Permission denied
find: ‘./var/cache/ldconfig’: Permission denied
bandit6@bandit:/$ cat ./etc/bandit_pass/bandit6
pepwepwpewpwepwppwepwppepwepwepwpepwpewpwpepwepwepw
bandit6@bandit:/$ 
### This ^ was incorrect ;-;
libpam0g:amd64.list
bandit6@bandit:/var/lib/dpkg/info$ ^C
bandit6@bandit:/var/lib/dpkg/info$ ls -ltrh | grep "bandit"
-rw-r----- 1 bandit7 bandit6   33 May  7  2020 bandit7.password
bandit6@bandit:/var/lib/dpkg/info$ cat bandit7.password 
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
bandit6@bandit:/var/lib/dpkg/info$ 



```
