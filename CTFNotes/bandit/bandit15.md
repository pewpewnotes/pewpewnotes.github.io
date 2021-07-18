### Bandit 15

The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.
```
bandit15@bandit:~$ openssl s_client -connect 127.0.0.1:30001
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
MIICBjCCAW+gAwIBAgIEfftLGTANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDDAls
b2NhbGhvc3QwHhcNMjEwNDEzMDgzODA3WhcNMjIwNDEzMDgzODA3WjAUMRIwEAYD
VQQDDAlsb2NhbGhvc3QwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBAMLfXBVa
jVKDHlA3U+S0hBMJMJlfue3xKECpmx1Ajp4/khUuWwvPB7+wLjqasBO2WfFYJzcq
z9t7FfAPIlYjgvOTQs5X4vQ1aGzanvnNn+1VknpOnFAJQBSFq6ZD3ipWrhwm9XZq
8CgFhTGp9IPthZp8Y0B7OgobhlMtXD/zLaTbAgMBAAGjZTBjMBQGA1UdEQQNMAuC
CWxvY2FsaG9zdDBLBglghkgBhvhCAQ0EPhY8QXV0b21hdGljYWxseSBnZW5lcmF0
ZWQgYnkgTmNhdC4gU2VlIGh0dHBzOi8vbm1hcC5vcmcvbmNhdC8uMA0GCSqGSIb3
DQEBBQUAA4GBAMFH9rsZovwnb5k71/MpyCnXEwGlIhixUu6qfi1kiFvhJ6lJCvaO
weOYxV4oJy1OEB0LSEAQOnSPfzC8dDasijFcdVhuIGGPuQ2GZ05nCiiIZUNnrMRB
0z2RuRxgxMVjOvcSIJyvwyjVH4jY4I434fMyldePLxO1POLd1cxoKNTO
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
    Session-ID: DFB64E1B780E978814B24F096DB398CE8368B366ECA851EC2A489A0F72CBC950
    Session-ID-ctx: 
    Master-Key: 221BE82D7CC8D2B0EE6EBE9E05BBAEE7B4558CFB74E47C81534E21C1E2BD5B3F67DE06320D2B185EA02EC97CACBE4DAD
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - f2 5b 83 7e f0 ca 58 ca-aa f3 8f 83 b9 65 d5 23   .[.~..X......e.#
    0010 - 69 6d 7a a4 5e c5 44 ad-49 24 d3 ef 09 0b 22 be   imz.^.D.I$....".
    0020 - 0d b6 7f 8d 86 80 5b 86-1d 3b bc e7 81 15 de 27   ......[..;.....'
    0030 - ac a1 1c 43 29 49 f0 52-fe fd 93 ce af a4 33 34   ...C)I.R......34
    0040 - e2 1f 51 7f 56 a9 34 da-09 b5 54 b6 d0 8b bb 23   ..Q.V.4...T....#
    0050 - 32 58 e3 48 48 69 eb 35-81 25 a2 3d 1c de 10 92   2X.HHi.5.%.=....
    0060 - c6 78 25 53 53 af 4a 6b-d1 30 ee 59 7c 32 40 1b   .x%SS.Jk.0.Y|2@.
    0070 - 33 4b 0c 25 f3 de 48 8a-48 3f a6 0b e0 d1 c3 d7   3K.%..H.H?......
    0080 - b9 19 65 84 99 54 5e 1a-f4 84 a3 96 63 35 be 73   ..e..T^.....c5.s
    0090 - b8 3a d0 a3 31 fd 03 60-72 f6 1b 5b 62 eb 97 06   .:..1..`r..[b...

    Start Time: 1619180340
    Timeout   : 7200 (sec)
    Verify return code: 18 (self signed certificate)
    Extended master secret: yes
---
BfMYroe26WYalil77FoDi9qh59eK5xNr
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd

closed
bandit15@bandit:~$ 


```
