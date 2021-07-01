More Will be added eventually 

❯ sudo apt install libiperf
For libiperf missing dependency

❯ Fixing virtualbox guest additions on host or guest.
```
cd ~
wget -c https://download.virtualbox.org/virtualbox/6.1.22/VBoxGuestAdditions_6.1.22.iso -O pew.iso 

sudo mount ~/pew.iso -o loop /mnt

cd /mnt
sudo ./VBoxLinux*.run
```

* "Vagrant was unable to mount VirtualBox shared folders. This is usually
because the filesystem "vboxsf" is not available."
```
virtualbox-guest-utils
or 
mount -t syntax inside the guest
```
