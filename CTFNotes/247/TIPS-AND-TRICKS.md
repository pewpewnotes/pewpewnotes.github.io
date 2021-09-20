### TIPSANDTRICKS 

I didn't knew on how to send crlf via nc and I was even confused if that could be sent.
I checked a code solution for this to find out that crlf is to be sent and another stack overflow told me that
nc -C is crlf for line endings. 
With equipped with that knowledge, we can proceed to write the code.

### Code
```python3

from pwn import *

SERVER = "21b2d6192bc2a8ee.247ctf.com"
PORT = 50427

r = remote(SERVER, PORT, level = 'debug')
for i in range(0,501):
    print(i)
    print("==="*5)
    received = r.recv().decode('utf8')
    received = received.split(" ")
    standard = received.index('+')
    operand1 = int(received[standard-1])
    operand2 = int(received[standard+1].split("?")[0])
    r.sendline(str(operand1+operand2))
    r.sendline('\r\n')
    

```

### Creds
```
247CTF{6ae15c0aeb45a334b3f01eb0dda5cab1}
```


 ~Kurama
