```
  ___                    ____  
 / _ \  ___ _____      _|___ \ 
| | | |/ __/ _ \ \ /\ / / __) |
| |_| | (_| (_) \ V  V / / __/ 
 \__\_\\___\___/ \_/\_/ |_____|
```

### Introduction

Qcow2 is a popular disk image format that can be read and used as a file system without having to attach it to a running VM.
The simplest way this could be used is for restoration or hacking or simply recovery from Qcow2 image in case the booting os is corrupted or infected.
Also, when one has information on a backed up virtual image and doesn’t wants to turn on a whole VM in order to access some data held on it :P. (Laziness ++;)

If you’re using a host such as Proxmox then you’ll already have everything installed, 
but if you’re on some other Debian based system then you’ll need to install the required package

```
sudo apt install qemu-utils
```

And on arch the package name is mostly the same and if you have qemu it should be already installed. 
Mounting and interfacing often requires one to have the specific driver loaded. 

```
sudo modprobe nbd
ls /dev/nbd*
# should list about 16 interfaces, which precisely means that
# At most we can have only 16 images mapped or mounted.
```

![](/home/akuma/vimwiki/img/qcow21.png)



And then make sure that the qcow2 image is not in use (running inside VM or anything as such)

![](/home/akuma/vimwiki/img/qcow22.png)

And then go ahead and mount it all in the proper folders



![](/home/akuma/vimwiki/img/qcow23.png)



Ofcourse, It needs a SWAP type FS to mount swap, which I don't have. But others should work just fine. 



#### Things remaining to research:

1. Windows

2. Automation




The thing is, it also means that the data inside the VM is not all that safe either :P

![](/home/akuma/vimwiki/img/qcow2vulns.png)

As a hacker, all you need to do is mount the qcow2 or get it on your machine and retrieve whatever you need XD

### Detach a qcow2 Image Virtual Image File
Once you have finished with the virtual image file,
you’ll want to detach it and release the nbd process used for IO operations for that image. Assuming that any mounts based on the image have been umount‘d use the qemu-nbd command with the -D switch:

`qemu-nbd -d /dev/nbd0`
You can also remove the kernel module if you’ve detached all of your virtual images from their /dev/nbdX device:

`rmmod nbd`


Source: [Access a qcow2 Virtual Disk Image From The Host](https://www.jamescoyle.net/how-to/1818-access-a-qcow2-virtual-disk-image-from-the-host)
