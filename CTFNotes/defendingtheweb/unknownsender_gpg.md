### Unknownsender_gpg 
First I tried checking the base64 decryption and I got the email, and after a long time of trying with that I realized that it won't work. 
Upon googling I found out that 
[SO answer](https://superuser.com/questions/271509/is-it-possible-to-find-a-senders-public-pgp-gpg-key-from-an-encoded-message)


### Creds
```
gpg --search-keys aiden@defendtheweb.net
gpg: data source: https://162.213.33.8:443
(1)	eldridgedaniel@hotmail.co.uk
	Aiden Lawrence <aiden@defendtheweb.net>
	  2048 bit RSA key D7F7BD21A11B39E4, created: 2020-07-02
(2)	Aiden Lawrence <aiden@defendtheweb.net>
	  4096 bit RSA key 48BF6357AB80EB5E, created: 2019-07-10
Keys 1-2 of 2 for "aiden@defendtheweb.net".  Enter number(s), N)ext, or Q)uit > 

```


 ~Kurama
