```
 ____            _     
| __ )  __ _ ___| |__  
|  _ \ / _` / __| '_ \ 
| |_) | (_| \__ \ | | |
|____/ \__,_|___/_| |_|
                       
```

1. Handling Named Arguments

A neat trick is to use the __boolean__ variables to make a certain part of the script print or
not print. Or even better a particular command to execute or not, can we extend it even more?
ofcourse! 

Example Script: 

```
#!/bin/bash
deploy=false
uglify=false

while (( $# > 1 )); do case $1 in
    --deploy) deploy="$2";;
    --uglify) uglify="$2";;
    *) break;
esac;
shift 2
done

$deploy && echo "will deploy .... deploy = $deploy"
$uglify && echo "will uglify .... uglify = $uglify"
```
The best part is when udlify is false, the entire statement wont be printed!

What we learn: 
1) using while loop (._.) I am embarassed to accept but i didnt knew this is how you create
a while loop in bash. 
2) $# is for arguments, which was known to me. 
3) I still dont know whats shift 2 in bash, will check 
```
[akuma@shiro ~]$ help shift
    shift: shift [n]
    Shift positional parameters.
    
    Rename the positional parameters $N+1,$N+2 ... to $1,$2 ...  If N is
    not given, it is assumed to be 1.
    
    Exit Status:
    Returns success unless N is negative or greater than $#.
```
So basically thanks to shift 2 we were able to use that to accep uglify as a sysarg variable too
4) Curious use of && :P

2. List files without using "ls"

This is new stuff!!
```
# files and directories
printf "%s\n" *
# only directories
printf "%s\n" */
# only particular type of files
printf "%s\n" *.{gif,png,jpg}

```
3. To capture a list of files into a variable 
```
files = ( * )
for i in "${files[@]}";do
  echo "$file"
done
```
this is better than using ls in for loop which can be dangerous and very heavy.

4. Using heredoc

If you dont have a file editor, you might not need it :P
```
─❯ cat <<__X >file
heredoc> pewpew
heredoc> I am using a here doc to write this
heredoc> watashi wa sugoy desu!
heredoc> pewpew 
heredoc> __X

─❯ cat file
   1   │ pewpew
   2   │ I am using a here doc to write this
   3   │ watashi wa sugoy desu!
   4   │ pewpew 
```
5. Catting gziped file to one larger file

```
echo "hi" > hello
echo "bye" > bye
gzip hello
gzip bye
cat hello.gz bye.gz > greetings,gz

# This is ofc inefficient 
```
6. Playing with daemon files
```
#!/bin/bash
if [[ ! -e /tmp/test.py.pid ]]; then   # Check if the file already exists
    python test.py &                   #+and if so do not run another process.
    echo $! > /tmp/test.py.pid
else
    echo -n "ERROR: The process is already running with pid "
    cat /tmp/test.py.pid
    echo
fi
```
This will be a great help with kunst and ncmpcpp albumart

7. Mkfifo 
alright so basically most of the time using 
```
cat pew.tmp | grep "lmao"
```
works, and its alright, we can also do 
```
curl pewpew.go > tempFile && cat tempFile | grep -v "kek" > lol
```
this works perfectly but it has a problem, the problem of beign deleted. What if someone who 
doesnt understands whats going on deletes the tempfile, it will simply break lol which is not good. 
hence we have this: 
```
mkfifo mypipe 
echo "hi" > mypipe
cat < mypipe
```
8. Redirection to network address
bash treats `/dev/{udp|tcp}/host/port` as special file, which allows network communications. 
```
execv 3</dev/tcp/www.google.com/80
printf 'GET / HTTP/1.0\r\n\r\n' >&3
cat <&3
```
9. Control structures for bash

```
File Operators            Details
-e "$file"                Returns true if the file exists.
-d "$file"                Returns true if the file exists and is a directory
-f "$file"                Returns true if the file exists and is a regular file
-h "$file"                Returns true if the file exists and is a symbolic link

String Comparators        Details
-z "$str"                 True if length of string is zero
-n "$str                  True if length of string is non-zero
"$str" = "$str2"          True if string $str is equal to string $str2. Not best for integers. It may work but will be inconsitent.
"$str" != "$str2"         True if the strings are not equal

Integer Comparators       Details
"$int1" -eq "$int2"       True if the integers are equal
"$int1" -ne "$int2"       True if the integers are not equals
"$int1" -gt "$int2"       True if int1 is greater than int 2
"$int1" -ge "$int2"       True if int1 is greater than or equal to int2
"$int1" -lt "$int2"       True if int1 is less than int 2
"$int1" -le "$int2"       True if int1 is less than or equal to int2
```
