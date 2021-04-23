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
 

