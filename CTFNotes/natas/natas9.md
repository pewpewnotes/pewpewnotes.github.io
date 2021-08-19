### Natas 9
This one took a bit of time, we were presented with an encoded string and a function.
```
$encodedSecret = "3d3d516343746d4d6d6c315669563362";

function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}
```
In here, we were to decode the string, the operations were simple.
1. Hex -> Bin
2. Bin -> Str
3. Str -> Str reverse
4. base64 decode

which gave us: oubWYf2kBq
and using that gave us the creds.

#### Note
1. Write a program that takes care of such operations, it needs to be very correct and working
2. Learn more python.


### Creds
```
Access granted. The password for natas9 is W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl
```


 ~Kurama
