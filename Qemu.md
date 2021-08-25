```
  ___  _____ __  __ _   _ 
 / _ \| ____|  \/  | | | |
| | | |  _| | |\/| | | | |
| |_| | |___| |  | | |_| |
 \__\_\_____|_|  |_|\___/ 
                          
```

Arch: sudo pacman -S qemu (optionally "qemu-arch-extra" for more architectures)
Debian/Ubuntu: sudo apt install qemu
Fedora: sudo dnf install qemu

### To create a virtual image use:

* qemu-img create -f qcow2 Image.img 10G

* (create is to create an image, -f qcow2 sets the format to qcow2, Image.img is our final file and 10G is it's size)

* Launching the VM:

* qemu-system-x86_64 -enable-kvm -cdrom OS_ISO.iso -boot menu=on -drive file=Image.img -m 2G

* (-enable-kvm enables KVM, -cdrom selects an iso to load as a cd, -boot menu=on enables a boot menu, -drive file= selects a file for the drive, -m sets the amount of dedicated RAM)
(Remember! Ctrl + Alt + G to exit capture, Ctrl + Alt + F to fullscreen!)

* That doesn't run so good, what can we do to improve it?

* Basic performance options

* -cpu host (sets the CPU to the hosts' CPU)
*  -smp 2 (sets the numbers of cores)

### Basic Graphics Acceleration

* the -vga option can be used to specify one of various vga card emulators:

* "qxl" offers 2D acceleration but requires kernel modules "qxl" and "bochs_drm" to be enabled:

* -vga qxl

* "virtio" works much better and supports some 3D emulation:

* -vga virtio -display sdl,gl=on
