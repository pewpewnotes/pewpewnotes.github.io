### Princess Slug
Alright, I accept defeat, I am a loser FML.
So this was a directory traversal attack, and I failed to do it. I noticed that there is a 
?p=index | News | Contact page, so that means its getting file, I tried ../ and it said 
```
Warning: file_get_contents(../../../../../../../../../\/\/etc/passwd.html) [function.file-get-contents]: failed to open stream: No such file or directory in pages on line 22
```
After this I was out of ideas on what to do next, and upon checking I found out that to avoid getting that .html at the end we need to use the null terminator for the string. 
`%00` is the null terminator and then 
`../admin.php%00` Allows us to get the login page on main page and upon checking source code we find the php code inside and password was basically if-else :P



### Creds
```
351a4d4d88
```
