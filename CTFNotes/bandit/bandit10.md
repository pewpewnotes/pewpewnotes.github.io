### Bandit 10
***
The password for the next level is stored in the file data.txt, which contains base64 encoded data

um, just base64 -d? 
```
bandit10@bandit:~$ ls
data.txt
bandit10@bandit:~$ cat data.txt 
VGhlIHBhc3N3b3JkIGlzIElGdWt3S0dzRlc4TU9xM0lSRnFyeEUxaHhUTkViVVBSCg==
bandit10@bandit:~$ cat data.txt | base64 -d
The password is ThisisNOtaCOrrectPASSWORDFUCKYOU
bandit10@bandit:~$ 

```
