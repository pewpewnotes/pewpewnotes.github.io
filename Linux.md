```text
 _     _                  
| |   (_)_ __  _   ___  __
| |   | | '_ \| | | \ \/ /
| |___| | | | | |_| |>  < 
|_____|_|_| |_|\__,_/_/\_\
                          
```

### Sysfs Notes
* Link: https://www.kernel.org/doc/ols/2005/ols2005v1-pages-321-334.pdf
* Notes: [Sysfs](Sysfs)


***

* For action with Lid or powerbutton with systemd-logind
```
Edit /etc/systemd/logind.conf and make sure you have

HandleLidSwitch=ignore
which will make it ignore the lid being closed. (You may need to also undo the other changes you've made.)

Then, you'll want to reload logind.conf to make your changes go into effect (thanks to Ehtesh Choudhury for pointing this out in the comments):

systemctl restart systemd-logind

```
