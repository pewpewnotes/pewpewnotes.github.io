### Bandit 30

There are many things that I donot know, and this was one of them. Since its not one of the most commonly used thing, I guess I know why I dont remember solving it

For this we went as far as checking packed-refs but then we dont know how to check it out nor on how to google it.

I know its a limitation, but I figured it out I guess with a little googling for solution.

### Logs
```
bandit30@bandit:/tmp/tmp.42Zh4pwfPr$ ls
bandit30@bandit:/tmp/tmp.42Zh4pwfPr$ git clone ssh://bandit30-git@localhost/home/bandit30-git/repo
Cloning into 'repo'...
Could not create directory '/home/bandit30/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit30/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit30-git@localhost's password: 
remote: Counting objects: 4, done.
remote: Total 4 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (4/4), done.
bandit30@bandit:/tmp/tmp.42Zh4pwfPr$ ls
cdrepo
bandit30@bandit:/tmp/tmp.42Zh4pwfPr$ cd repo/
bandit30@bandit:/tmp/tmp.42Zh4pwfPr/repo$ ls
README.md
bandit30@bandit:/tmp/tmp.42Zh4pwfPr/repo$ cd .git
bandit30@bandit:/tmp/tmp.42Zh4pwfPr/repo/.git$ ls
branches  config  description  HEAD  hooks  index  info  logs  objects  packed-refs  refs
bandit30@bandit:/tmp/tmp.42Zh4pwfPr/repo/.git$ cat packed-refs 
# pack-refs with: peeled fully-peeled 
3aefa229469b7ba1cc08203e5d8fa299354c496b refs/remotes/origin/master
f17132340e8ee6c159e0a4a6bc6f80e1da3b1aea refs/tags/secret
bandit30@bandit:/tmp/tmp.42Zh4pwfPr/repo/.git$ git show 
commit 3aefa229469b7ba1cc08203e5d8fa299354c496b
Author: Ben Dover <noone@overthewire.org>
Date:   Thu May 7 20:14:54 2020 +0200

    initial commit of README.md

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..029ba42
--- /dev/null
+++ b/README.md
@@ -0,0 +1 @@
+just an epmty file... muahaha
bandit30@bandit:/tmp/tmp.42Zh4pwfPr/repo/.git$ git show f17132340e8ee6c159e0a4a6bc6f80e1da3b1aea
47e603bb428404d265f59c42920d81e5
bandit30@bandit:/tmp/tmp.42Zh4pwfPr/repo/.git$ 


```

### Creds
```
- username: bandit31
- password: 47e603bb428404d265f59c42920d81e5
```


 ~Kurama
