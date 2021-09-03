### Natas 12
This one took a hell lot of time for me to solve, it was difficult one
And ofcourse I am an idiot and I had to do it on my own this time. I think I had cheated twice on this one and it feels terrible
So we are greeted with a page and lots of code, understanding the code we see that there is a defaultdata that is being xor encrypted with key
and then is being used to set the cookie. We are basically supposed to hack through xor and get the original key and figure it all out.

We simply know that
`cipher = key ^ plain`
from laws of logic (lol)
`key = cipher ^ plain`
And since from the code we have already seen the plain and cipher, we know how and where to attack.

Rest is documented in below php code snippet

```

function xor_decrypt($in) {
    $key = base64_decode("ClVLIh4ASCsCBE8lAxMacFMZV2hdVVotEhhUJQNVAmhSEV4sFxFeaAw=");
    $text = $in;
    $outText = '';

    // Iterate through each character
    for($i=0;$i<strlen($text);$i++) {
    $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }
    print $outText;
    return $outText;
}
$defaultdata = array( "showpassword"=>"no", "bgcolor"=>"#ffffff");
ClVLIh4ASCsCBE8lAxMacFMZV2hdVVotEhhUJQNVAmhSEV4sFxFeaAw=

function xor_encrypt($in) {
    $key = 'qw8J';
    $text = $in;
    $outText = '';

    // Iterate through each character
    for($i=0;$i<strlen($text);$i++) {
    $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }
    print $outText;
    return $outText;
}

$forgeddata = array( "showpassword"=>"yes", "bgcolor"=>"#ffffff");

$forgeddata = array( "showpassword"=>"yes", "bgcolor"=>"#ffffff");
# Incorrect: I am an idiot, after seeing 
# "qw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jq"
# I thought key was Jqw8 
# MVMEUCUGB1k5AgBXOBVVAmgIEktoXVVaLRIYVCUDVQJoUhFeLBcRXmgM
// With correct key, qw8J
ClVLIh4ASCsCBE8lAxMacFMOXTlTWxooFhRXJh4FGnBTVF4sFxFeLFMK

```
Simply set the cookie and done.


### Creds
```
natas12:EDXp0pS26wLKHZy1rDBPUZk0RKfLGIR3
```


 ~Kurama
