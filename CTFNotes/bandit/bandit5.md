### Bandit 5
***
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

human-readable
1033 bytes in size
not executable
This was a bit tricky, but after few trial and errors I figured out on how to do it.
```
bandit5@bandit:~/inhere$ find . -type f -size 3 -exec ls -ltr {} \;
-rw-r----- 1 root bandit5 1076 May  7  2020 ./maybehere06/-file2
-rwxr-x--- 1 root bandit5 1271 May  7  2020 ./maybehere06/.file1
-rwxr-x--- 1 root bandit5 1148 May  7  2020 ./maybehere16/.file3
-rwxr-x--- 1 root bandit5 1133 May  7  2020 ./maybehere17/-file1
-rwxr-x--- 1 root bandit5 1211 May  7  2020 ./maybehere11/-file1
-rwxr-x--- 1 root bandit5 1077 May  7  2020 ./maybehere08/-file1
-rw-r----- 1 root bandit5 1503 May  7  2020 ./maybehere14/.file2
-rwxr-x--- 1 root bandit5 1382 May  7  2020 ./maybehere14/spaces file1
-rwxr-x--- 1 root bandit5 1039 May  7  2020 ./maybehere00/-file1
-rw-r----- 1 root bandit5 1033 May  7  2020 ./maybehere07/.file2
-rwxr-x--- 1 root bandit5 1237 May  7  2020 ./maybehere10/-file3
-rwxr-x--- 1 root bandit5 1052 May  7  2020 ./maybehere10/-file1
-rw-r----- 1 root bandit5 1423 May  7  2020 ./maybehere13/-file2
-rwxr-x--- 1 root bandit5 1359 May  7  2020 ./maybehere13/-file1
bandit5@bandit:~/inhere$ find . -type f -size 3 -exec ls -ltr {} \; | grep "1033"
-rw-r----- 1 root bandit5 1033 May  7  2020 ./maybehere07/.file2

## ------
# Since I am lazy and I didnt wanted to copy paste the path to cut it.
bandit5@bandit:~/inhere$ cat $(find . -type f -size 3 -exec ls -ltr {} \; | grep "1033" | cut -d " " -f 11)
PEWPEWPREWCJopasjvpia9eofavasiovaeiohfiohsai
                                     
```
