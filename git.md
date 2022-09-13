### Git 

***

####How to merge changes from original owner of a forked repo

(Basically syncing with original master)

1. In terminal,
```bash 
$ git remote -v
> origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
> origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)

```
2. Specify the new upstream
```bash
git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git

```

4. Verify with `git remote -v`
5. Now to fetch upstream changes: `git fetch upstream`
6. Checkout local master: `git checkout master`
7. Merge the changes: `git merge upstream/master`
8. To force a fork to be same as upstream, 
```bash
git remote add upstream /url/to/original/repo
git fetch upstream
git checkout master
git reset --hard upstream/master  
git push origin master --force
```
 

 
***

#### Git study notes

1. Check logs
* `git log`
* `git log --oneline`
* `git log --oneline --graph`

2. Recover deleted files
* `git reset --hard` Can make you lose changes you made in the files
* `git reset --mixed` Default flag thats used by git, it retains the altered state in current working directory.

3. Branching and Checking out
* `git branch name`
* `git checkout name`
* `git log --decorate --graph --oneline --all` Shows commits across all branches
* `git tag `

4. Merging
* In git, <<<< HEAD is the point where things branched off, and ==== marks the start of the other branch designated by >>>>> branch
```
A
B
C
<<<<<<< HEAD
D
F
G
=======
E
H
>>>>>>> experimental
```
Changed to
```
A
B
C
D
E
F
G
H

```

Resulting in: 
```
*   8950ccc (HEAD -> master) merged experimental
|\  
| * 69d7fb4 (experimental) H
| * b01c60d E
* | 62651d2 G
* | 9f95b66 F
* | 5683361 D
|/  
* 8d8212d C
* de5e880 B
* 5cadd5e A

```
