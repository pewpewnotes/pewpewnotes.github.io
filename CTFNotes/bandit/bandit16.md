### Bandit 16
*** 
```
bandit16@bandit:~$ export TERM=xterm
bandit16@bandit:~$ clear

bandit16@bandit:~$ ls
bandit16@bandit:~$ nmap -A -p31000-32000 127.0.0.1 

Starting Nmap 7.40 ( https://nmap.org ) at 2021-05-04 17:13 CEST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00044s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
| ssl-cert: Subject: commonName=localhost
| Subject Alternative Name: DNS:localhost
| Not valid before: 2021-04-13T08:39:02
|_Not valid after:  2022-04-13T08:39:02
|_ssl-date: TLS randomness does not represent time
31691/tcp open  echo
31790/tcp open  ssl/unknown
| fingerprint-strings: 
|   FourOhFourRequest, GenericLines, GetRequest, HTTPOptions, Help, Kerberos, LDAPSearchReq, LPDString, RTSPRequest, SIPOptions, SSLSessionReq, TLSSessionReq: 
|_    Wrong! Please enter the correct current password
| ssl-cert: Subject: commonName=localhost
| Subject Alternative Name: DNS:localhost
| Not valid before: 2021-04-13T08:39:02
|_Not valid after:  2022-04-13T08:39:02
|_ssl-date: TLS randomness does not represent time
31960/tcp open  echo
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port31790-TCP:V=7.40%T=SSL%I=7%D=5/4%Time=609164A5%P=x86_64-pc-linux-gn
SF:u%r(GenericLines,31,"Wrong!\x20Please\x20enter\x20the\x20correct\x20cur
SF:rent\x20password\n")%r(GetRequest,31,"Wrong!\x20Please\x20enter\x20the\
SF:x20correct\x20current\x20password\n")%r(HTTPOptions,31,"Wrong!\x20Pleas
SF:e\x20enter\x20the\x20correct\x20current\x20password\n")%r(RTSPRequest,3
SF:1,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x20password\n
SF:")%r(Help,31,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x2
SF:0password\n")%r(SSLSessionReq,31,"Wrong!\x20Please\x20enter\x20the\x20c
SF:orrect\x20current\x20password\n")%r(TLSSessionReq,31,"Wrong!\x20Please\
SF:x20enter\x20the\x20correct\x20current\x20password\n")%r(Kerberos,31,"Wr
SF:ong!\x20Please\x20enter\x20the\x20correct\x20current\x20password\n")%r(
SF:FourOhFourRequest,31,"Wrong!\x20Please\x20enter\x20the\x20correct\x20cu
SF:rrent\x20password\n")%r(LPDString,31,"Wrong!\x20Please\x20enter\x20the\
SF:x20correct\x20current\x20password\n")%r(LDAPSearchReq,31,"Wrong!\x20Ple
SF:ase\x20enter\x20the\x20correct\x20current\x20password\n")%r(SIPOptions,
SF:31,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x20password\
SF:n");

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 89.62 seconds
bandit16@bandit:~$ openssl s_client connect -connect 127.0.0.1:300001
s_client: Use -help for summary.
bandit16@bandit:~$ openssl s_client -connect 127.0.0.1:300001
140198454288448:error:0200206F:system library:connect:Connection refused:../crypto/bio/b_sock2.c:108:
140198454288448:error:2008A067:BIO routines:BIO_connect:connect error:../crypto/bio/b_sock2.c:109:
connect:errno=111
bandit16@bandit:~$ openssl s_client -connect 127.0.0.1:31790
CONNECTED(00000003)
depth=0 CN = localhost
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
---
Certificate chain
 0 s:/CN=localhost
   i:/CN=localhost
---
Server certificate
-----BEGIN CERTIFICATE-----
MIICBjCCAW+gAwIBAgIEAVEaADANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDDAls
b2NhbGhvc3QwHhcNMjEwNDEzMDgzOTAyWhcNMjIwNDEzMDgzOTAyWjAUMRIwEAYD
VQQDDAlsb2NhbGhvc3QwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBAMSNMcd2
/JHQJIG6WVZ1VjJUi7NU2N/tkFLsLv7Y3slHaQAHLaC2aqILEQwYjDAhkvCogSwx
nvyWicMmNAUie9JaHNqKbRXPawKvKpr3bMgH5Gwbj/aUt18FZlzGUVJJfGzlWPkr
A2nwgzcVLkJKWR/2bV1C9gh/VqTYtUxPi7RtAgMBAAGjZTBjMBQGA1UdEQQNMAuC
CWxvY2FsaG9zdDBLBglghkgBhvhCAQ0EPhY8QXV0b21hdGljYWxseSBnZW5lcmF0
ZWQgYnkgTmNhdC4gU2VlIGh0dHBzOi8vbm1hcC5vcmcvbmNhdC8uMA0GCSqGSIb3
DQEBBQUAA4GBAGcuQr3/eWigw9h33i60xbf62wgXV8lcX6BuQ5xvOgd8eyvFIohp
usJHhSNGtdA+V0cw2qRuwWCmC/+unVvDWyC5OX2ka3XuF1Z9Z9282z+BCsuSAYHS
P3Oibv3/cEqa3kPuswuHOn2LkJmL/a/Kwwkzwfi/j9RIR/jm9FEOVlgm
-----END CERTIFICATE-----
subject=/CN=localhost
issuer=/CN=localhost
---
No client certificate CA names sent
Peer signing digest: SHA512
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1019 bytes and written 269 bytes
Verification error: self signed certificate
---
New, TLSv1.2, Cipher is ECDHE-RSA-AES256-GCM-SHA384
Server public key is 1024 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-AES256-GCM-SHA384
    Session-ID: 2A5F3FAD196E055C262FBD026A0AFB9102CD3BE4A27DC093E3FBCF82FBFD72F8
    Session-ID-ctx: 
    Master-Key: CDA4133CCE90989409FB0E6FBFD8CD2F369E2472D9EA95248156AF2655DA152487297E9DC853DC8A4E25612200BDBD1A
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 03 83 6e 86 7a 68 2a 2b-55 2d 9b 9e 6d 2f ce e5   ..n.zh*+U-..m/..
    0010 - 50 95 48 2c ac b2 89 ff-b1 aa 2d 79 8c 05 6b 24   P.H,......-y..k$
    0020 - 0a 8b f5 e3 0e 2b 23 ca-b1 45 ad 25 04 4d f0 09   .....+#..E.%.M..
    0030 - f8 02 88 11 b2 b1 8e 9a-b3 47 02 d4 ad 71 90 e0   .........G...q..
    0040 - a7 bd 7e 75 03 cc c7 e4-b7 13 7a ab 85 03 e1 54   ..~u......z....T
    0050 - b2 26 e5 6e 80 54 b9 e3-66 de 0a 3c 67 a3 f8 2e   .&.n.T..f..<g...
    0060 - fb f3 39 ee 0c 2e 4b 4a-90 16 5e 93 d1 ea 93 90   ..9...KJ..^.....
    0070 - c4 5d 84 91 1e 64 30 af-15 8c e7 04 37 41 60 85   .]...d0.....7A`.
    0080 - 55 81 ee 1f 0f f5 c9 9c-76 d6 7c 63 53 5c a0 4c   U.......v.|cS\.L
    0090 - a7 b4 d9 b8 6b 49 5f 5d-f4 79 d5 2c 1b 9d 71 13   ....kI_].y.,..q.

    Start Time: 1620141431
    Timeout   : 7200 (sec)
    Verify return code: 18 (self signed certificate)
    Extended master secret: yes
---
cluFn7wTiGryunymYOu4RcffSxQluehd
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----

closed
bandit16@bandit:~$ 


```
