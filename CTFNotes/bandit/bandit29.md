### Bandit 29
1. Get the repo
2. Cat the file
3. Get the branches
4. Switch to dev
5. Et voila!

### Logs
```
bandit29@bandit:/tmp/tmp.WIxYzHZxAF/repo$ git pull
Could not create directory '/home/bandit29/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit29/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit29-git@localhost's password: 
Already up-to-date.
bandit29@bandit:/tmp/tmp.WIxYzHZxAF/repo$ ls
README.md
bandit29@bandit:/tmp/tmp.WIxYzHZxAF/repo$ clear

bandit29@bandit:/tmp/tmp.WIxYzHZxAF/repo$ git branch
  dev
  list
* master
bandit29@bandit:/tmp/tmp.WIxYzHZxAF/repo$ git checkout dev
Switched to branch 'dev'
bandit29@bandit:/tmp/tmp.WIxYzHZxAF/repo$ git pull
Could not create directory '/home/bandit29/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit29/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit29-git@localhost's password: 
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> dev

bandit29@bandit:/tmp/tmp.WIxYzHZxAF/repo$     git branch --set-upstream-to=origin/<branch> dev
-bash: branch: No such file or directory
bandit29@bandit:/tmp/tmp.WIxYzHZxAF/repo$ git branch --set-upstream-to=origin/dev dev2
fatal: branch 'dev2' does not exist
bandit29@bandit:/tmp/tmp.WIxYzHZxAF/repo$ git branch --set-upstream-to=origin/dev dev
Branch dev set up to track remote branch dev from origin.
bandit29@bandit:/tmp/tmp.WIxYzHZxAF/repo$ git pull
Could not create directory '/home/bandit29/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit29/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit29-git@localhost's password: 
Permission denied, please try again.
bandit29-git@localhost's password: 
Updating 208f463..bc83328
Fast-forward
 README.md         | 2 +-
 code/gif2ascii.py | 1 +
 2 files changed, 2 insertions(+), 1 deletion(-)
 create mode 100644 code/gif2ascii.py
bandit29@bandit:/tmp/tmp.WIxYzHZxAF/repo$ cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: 5b90576bedb2cc04c86a9e924ce42faf

bandit29@bandit:/tmp/tmp.WIxYzHZxAF/repo$ 

```


### Creds
```
- username: bandit30
- password: 5b90576bedb2cc04c86a9e924ce42faf

```


 ~Kurama
