### Bandit 31
This one was fairly straight forward.

### Logs
```
bandit31@bandit:/tmp/tmp.L0lJOvK3ib$ git clone ssh://bandit31-git@localhost/home/bandit31-git/repo
Cloning into 'repo'...
Could not create directory '/home/bandit31/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit31/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit31-git@localhost's password: 
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (4/4), done.
bandit31@bandit:/tmp/tmp.L0lJOvK3ib$ ls
repo
bandit31@bandit:/tmp/tmp.L0lJOvK3ib$ cd repo/
bandit31@bandit:/tmp/tmp.L0lJOvK3ib/repo$ ls
README.md
bandit31@bandit:/tmp/tmp.L0lJOvK3ib/repo$ cat README.md 
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master

bandit31@bandit:/tmp/tmp.L0lJOvK3ib/repo$ ls
README.md
bandit31@bandit:/tmp/tmp.L0lJOvK3ib/repo$ echo "May I come in?" > key.txt
bandit31@bandit:/tmp/tmp.L0lJOvK3ib/repo$ git add key.txt 
The following paths are ignored by one of your .gitignore files:
key.txt
Use -f if you really want to add them.
bandit31@bandit:/tmp/tmp.L0lJOvK3ib/repo$ ls
key.txt  README.md
bandit31@bandit:/tmp/tmp.L0lJOvK3ib/repo$ cat .gitignore 
*.txt
bandit31@bandit:/tmp/tmp.L0lJOvK3ib/repo$ git add -f key.txt 
bandit31@bandit:/tmp/tmp.L0lJOvK3ib/repo$ git commit -m "Added keys"
[master f8480ac] Added keys
 1 file changed, 1 insertion(+)
 create mode 100644 key.txt
bandit31@bandit:/tmp/tmp.L0lJOvK3ib/repo$ git push
Could not create directory '/home/bandit31/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit31/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit31-git@localhost's password: 
Counting objects: 3, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 321 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote: ### Attempting to validate files... ####
remote: 
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote: 
remote: Well done! Here is the password for the next level:
remote: 56a9bf19c63d650ce78e6ec0354ee45e
remote: 
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote: 
To ssh://localhost/home/bandit31-git/repo
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'ssh://bandit31-git@localhost/home/bandit31-git/repo'
bandit31@bandit:/tmp/tmp.L0lJOvK3ib/repo$ 


```

### Creds
```
- username: bandit32
- password: 56a9bf19c63d650ce78e6ec0354ee45e
```


 ~Kurama
