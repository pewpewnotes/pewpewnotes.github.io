### Intro 10

Upon closer inspection (searching for password) we find that, 
```
 <script type='text/javascript'>
 document.thecode = 'code123';
 $(function(){
 $('.level form').submit(function(e) 
 {
 e.preventDefault(); 
 if(document.getElementById('password').value == document.thecode) 
 { 
 document.location = '?pass=' + document.thecode; 
 } else { alert('Incorrect password') } })}); </script>
```

further ahead down the code we also find, 

```
document['thecode'] = 
'\x39\x32\x32\x62\x32\x38\x34\x63\x66\x61'
```

Instead of trying to comprehend what it was or running it anywhere, we simply pasted it in js console and wham "922b284cfa" is our password.
