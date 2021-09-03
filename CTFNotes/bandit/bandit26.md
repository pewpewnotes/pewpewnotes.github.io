### Bandit 26

This is the most weird or rather the most exciting one. I remembered a few things from last time but it wasn't working so I ended up having to look up again. 
Basically as we could try, from bandit25 we should cat /etc/passwd and try to see the shell thats being used for bandit26, We figured it was more.
So reduce the terminal size so that it goes in "more" mode and then v then :e /etc/bandit_pass/bandit26 and then we get our sweet flag!
Nope, actually not, remeber we are already in bandit26 we need bandit27!
Welp ;-; I was out of ideas, but it seems that something could be done 
I tried cating /etc/bandit_pass/bandit27 but ofcourse it was a permission denied.
again from vim, we can :shell /bin/bash and then :!ls -al and we see bandit27-do intuitively we know what it does, it does actions like bandit27 user, so all we needed to do was ./bandit27-do cat /etc/bandit_pass/bandit27 and wham!


### Creds
```
bandit26: 5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z
bandit27: 3ba3118a22e93127a4ed485be72ef5ea
```


 ~Kurama
