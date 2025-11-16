```

    _             _     _ _                  
   / \   _ __ ___| |__ | (_)_ __  _   ___  __
  / _ \ | '__/ __| '_ \| | | '_ \| | | \ \/ /
 / ___ \| | | (__| | | | | | | | | |_| |>  < 
/_/   \_\_|  \___|_| |_|_|_|_| |_|\__,_/_/\_\
                                             
```

### How to repopulate Archlinux keys 
(Very helpful for the vm)

```
sudo pacman -Sy archlinux-keyring
```

```
sudo rm -rf /etc/pacman.d/gnupg
sudo pacman-key --init
sudo pacman-key --populate archlinux
sudo pacman-key --refresh-keys
```
