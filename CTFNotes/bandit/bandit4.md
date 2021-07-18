### Bandit 4
***

* This one was simple, but I struggled a bit 
```
bandit4@bandit:~$ ls
inhere
bandit4@bandit:~$ cd inhere/
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
bandit4@bandit:~/inhere$ for i in .
> do
> cat "$i"
> done
cat: .: Is a directory
bandit4@bandit:~/inhere$ cat ./-file0
cat: ./-file0: No such file or directory
bandit4@bandit:~/inhere$ cat ./\-file0
cat: ./-file0: No such file or directory
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
bandit4@bandit:~/inhere$ tree
-bash: tree: command not found
bandit4@bandit:~/inhere$ file -file0
file: Cannot open `ile0' (No such file or directory).
bandit4@bandit:~/inhere$ file \-file0
file: Cannot open `ile0' (No such file or directory).
bandit4@bandit:~/inhere$ file ./-file0
./-file0: cannot open `./-file0' (No such file or directory)
bandit4@bandit:~/inhere$ file ./-file00
./-file00: data
bandit4@bandit:~/inhere$ cat ./-file00
�/`2ғ�%��rL~5�g��� �����bandit4@bandit:~/inhere$ cat ./-file01
��p,k�;��r*��	�.!��C��J	�dx,�bandit4@bandit:~/inhere$ cat ./-file02
e�)�#��5��
          ��p��V�_���ׯ�mmbandit4@bandit:~/inhere$ cat ./-file03
������h!TQO�`�4"aל�߂phT��,�Abandit4@bandit:~/inhere$ cat ./-file04
?�bandit4@bandit:~/inhere$ cat ./-file05
�r�l$�?h�9('���!y�e�#�x�O��=��bandit4@bandit:~/inhere$ cat ./-file06
ly���~��A�f����-E�{���m�����ܗMbandit4@bandit:~/inhere$ cat ./-file07
Pewpewpewpewppewpepwnotgonnatellwhererpasswordis
bandit4@bandit:~/inhere$ cat ./-file08
�T�?�i��j��îP�F�l�n��J����{��@bandit4@bandit:~/inhere$ cat ./-file09
�e�0$�in=��_b�5FA�P7sz��gNbandit4@bandit:~/inhere$ 
```
