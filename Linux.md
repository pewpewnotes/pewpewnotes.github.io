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

```text
Edit /etc/systemd/logind.conf and make sure you have

HandleLidSwitch=ignore
which will make it ignore the lid being closed. (You may need to also undo the other changes you've made.)

Then, you'll want to reload logind.conf to make your changes go into effect (thanks to Ehtesh Choudhury for pointing this out in the comments):

systemctl restart systemd-logind
```

* For disabling linux laptop keyboard

```text
You can use xinput to float the input device under X.

Execute the command xinput list to list your input devices.
Locate AT Translated Set 2 keyboard and take note of its id number; this will be used to disable the keyboard. Also, take note of the number at the end, [slave keyboard (#)]; this is the id number of the master, which will be used to re-enable your keyboard.
To disable the keyboard, execute the command xinput float <id#>, where <id#> is your keyboard's id number. For example, if the id was 10, then the command would be xinput float 10.
To re-enable the keyboard, execute the command xinput reattach <id#> <master#>, where master is that second number we noted down. So if the number was 3, you would do xinput reattach 10 3.
```

### Remaking Grub entry
* In case grub got borked somehow

```
sudo mkdir -p /mnt/boot/efi
sudo mount /dev/sda1 /mnt/boot/efi
cd /mnt/boot/efi
cat Recovery.txt
cd efi
sudo grub-install --target=x86_64-efi --efi-directory=/mnt/boot/efi
sudo grub-install --target=x86_64-efi --efi-directory=/mnt/boot/efi --bootloader-id=grub
sudo grub-mkconfig -o /mnt/boot/efi
os-prober
sudo os-prober

```

### Importing a CA cert in Arch
```
Use the trust command provided by the p11-kit package:

sudo trust anchor --store ~/my-ca-cert.crt

## Source: https://unix.stackexchange.com/questions/373492/installing-certificates-on-arch
```
