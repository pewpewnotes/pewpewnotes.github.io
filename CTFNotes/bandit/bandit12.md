### bandit 12
The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

Truly loved it, xxd and then all the compression stuffs, Not very difficult but is challenging.

```
bandit12@bandit:/tmp/pewpewAkuma$ xxd -r data.txt 
P�^data2.bin=��BZh91AY&SY�O����ڞOv���}?��}��^���������ߣ��;�����4���h�F�F��4LM
                                                                             @��z��FM��C�hF�C@�4@f��h
                                                                                                     ��i�4hh��=C%�>X�,�k���1��GY��
�J�쌑Oϊ��{RBp�Qix�Y�Z!d��j�(�搿ݳ��/��A�#�A�F��0P��v��`�"3�

                                          ��d�bX?��z��2��<��A �n}
5(3A��
      wO�R����6�XS{�
��9?L�P�yB��=z�m?�L�Nt*�7{qP��̜�%"�w9�qm4�� N3�6���K��H䋑[��}!
                                                             d��3A4$�M~�\ɠJ�C�kUƦ\���\�FSN��&=�[��q	\)�$:��H�t&/�(����]��BB9<s ��h=bandit12@bandit:/tmp/pewpewAkuma$ xxd -r data.txt > pew
bandit12@bandit:/tmp/pewpewAkuma$ file pew
pew: gzip compressed data, was "data2.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix
bandit12@bandit:/tmp/pewpewAkuma$ mv pew data2.bin
bandit12@bandit:/tmp/pewpewAkuma$ gunzip data2.bin
gzip: data2.bin: unknown suffix -- ignored
bandit12@bandit:/tmp/pewpewAkuma$ mv data
data2.bin  data.txt   
bandit12@bandit:/tmp/pewpewAkuma$ mv data
data2.bin  data.txt   
bandit12@bandit:/tmp/pewpewAkuma$ mv data2.bin data2.bin.gz
bandit12@bandit:/tmp/pewpewAkuma$ gunzip data2.bin.gz 
bandit12@bandit:/tmp/pewpewAkuma$ ls
data2.bin  data.txt
bandit12@bandit:/tmp/pewpewAkuma$ file data
data: cannot open `data' (No such file or directory)
bandit12@bandit:/tmp/pewpewAkuma$ file data2.bin 
data2.bin: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/pewpewAkuma$ bunzip2 data2.bin
bunzip2: Can't guess original name for data2.bin -- using data2.bin.out
bandit12@bandit:/tmp/pewpewAkuma$ ls
data2.bin.out  data.txt
bandit12@bandit:/tmp/pewpewAkuma$ file data2.bin.out
data2.bin.out: gzip compressed data, was "data4.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix
bandit12@bandit:/tmp/pewpewAkuma$ mv data2.bin.out data4.bin.gz
bandit12@bandit:/tmp/pewpewAkuma$ gunzip data4.bin.gz 
bandit12@bandit:/tmp/pewpewAkuma$ ls
data4.bin  data.txt
bandit12@bandit:/tmp/pewpewAkuma$ file data4.bin
data4.bin: POSIX tar archive (GNU)
bandit12@bandit:/tmp/pewpewAkuma$ untar data4.bin 
-bash: untar: command not found
bandit12@bandit:/tmp/pewpewAkuma$ tar data4.bin
tar: Old option 'b' requires an argument.
Try 'tar --help' or 'tar --usage' for more information.
bandit12@bandit:/tmp/pewpewAkuma$ tar -x data4.bin
tar: Refusing to read archive contents from terminal (missing -f option?)
tar: Error is not recoverable: exiting now
bandit12@bandit:/tmp/pewpewAkuma$ tar -xf data4.bin
bandit12@bandit:/tmp/pewpewAkuma$ ls
data4.bin  data5.bin  data.txt
bandit12@bandit:/tmp/pewpewAkuma$ file data5.bin 
data5.bin: POSIX tar archive (GNU)
bandit12@bandit:/tmp/pewpewAkuma$ tar -xf data5.bin
bandit12@bandit:/tmp/pewpewAkuma$ ls
data4.bin  data5.bin  data6.bin  data.txt
bandit12@bandit:/tmp/pewpewAkuma$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/pewpewAkuma$ bunzip2 data6.bin
bunzip2: Can't guess original name for data6.bin -- using data6.bin.out
bandit12@bandit:/tmp/pewpewAkuma$ file data6.bin.out 
data6.bin.out: POSIX tar archive (GNU)
bandit12@bandit:/tmp/pewpewAkuma$ tar -xf data6.bin.out
bandit12@bandit:/tmp/pewpewAkuma$ ls
data4.bin  data5.bin  data6.bin.out  data8.bin  data.txt
bandit12@bandit:/tmp/pewpewAkuma$ file data8.bin 
data8.bin: gzip compressed data, was "data9.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix
bandit12@bandit:/tmp/pewpewAkuma$ gunzip data8.bin
gzip: data8.bin: unknown suffix -- ignored
bandit12@bandit:/tmp/pewpewAkuma$ ls
data4.bin  data5.bin  data6.bin.out  data8.bin  data.txt
bandit12@bandit:/tmp/pewpewAkuma$ cp data8.bin data8.bin.gz
bandit12@bandit:/tmp/pewpewAkuma$ gunzip data8.bin.gz 
gzip: data8.bin already exists; do you wish to overwrite (y or n)? n
	not overwritten
bandit12@bandit:/tmp/pewpewAkuma$ ls
data4.bin  data5.bin  data6.bin.out  data8.bin  data8.bin.gz  data.txt
bandit12@bandit:/tmp/pewpewAkuma$ mv data8.bin
data8.bin     data8.bin.gz  
bandit12@bandit:/tmp/pewpewAkuma$ mv data8.bin.gz data9.bin.gz
bandit12@bandit:/tmp/pewpewAkuma$ gunzip data9.bin.gz 
bandit12@bandit:/tmp/pewpewAkuma$ ls
data4.bin  data5.bin  data6.bin.out  data8.bin  data9.bin  data.txt
bandit12@bandit:/tmp/pewpewAkuma$ file data9.bin 
data9.bin: ASCII text
bandit12@bandit:/tmp/pewpewAkuma$ cat data9.bin 
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
bandit12@bandit:/tmp/pewpewAkuma$ 

```
