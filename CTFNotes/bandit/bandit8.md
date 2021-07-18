### Bandit 8
***
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once
Super simple, grep and uniq \o/
```
bandit8@bandit:~$ cat data.txt | sort | uniq -c | grep "1 "
      1 NEVERgonnaGIVEYOUUPNeverGonnaLetyoudown
bandit8@bandit:~$ 

```
