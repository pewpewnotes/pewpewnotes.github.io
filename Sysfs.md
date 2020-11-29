```text

 ____            _____ ____    _     _                  
/ ___| _   _ ___|  ___/ ___|  | |   (_)_ __  _   ___  __
\___ \| | | / __| |_  \___ \  | |   | | '_ \| | | \ \/ /
 ___) | |_| \__ \  _|  ___) | | |___| | | | | |_| |>  < 
|____/ \__, |___/_|   |____/  |_____|_|_| |_|\__,_/_/\_\
       |___/                                            
```

#### Abstract
---
* Feature of Linux kernel 2.6+
* Allows kernel code to export information to user process
* Its an in-memory fs (a file system that stays in memory)
* Strict Hierarchy, Ascii files with one value per file.
* Very intuitive by design. 

#### Introduction
---
Sysfs is a mechanism that represents kernel objects, their attributes and their relationship with each other. 
It also provides two components fro kernel programming interface for exporting these items via sysfs.It also provides ui to view and manipulate thee items that map back to kernel objects.

```text
Internal               | External
* Kernel Object        | Directories
* Object Attributes    | Regular Files
* Object Relationships | Symblic Links
```
#### History
---
* Originally based on ramfs
* originally called as ddfs (device driver file system)
* in 2.5.1 it was called driverfs, then evolved into sysfs

#### Navigation
---
* Navigation is simple, with basic tools. Like `ls` `tree` etc.

#### Directory Structure
---

```text
/sys/
├── block
├── bus
├── class
├── dev
├── devices
├── firmware
├── fs
├── hypervisor
├── kernel
├── module
└── power
11 directories, 0 files
```
##### Block
---
* The `block` directory contains subdirectory for every block device that has been discovered.
* Each of them contain attributes that describe many things, including size of device
* dev_t number it maps to and much more.
* There is an interface to I/O scheduler, provides statistics about device request queue
* It also provides tunable features that a user or administrator can use to optimize performance
* including the ability to dynamically change the I/O scheduler to use.

##### Bus
---
```text

/sys/bus/
├── acpi
├── cec
├── clockevents
├── clocksource
├── container
├── cpu
├── dax
├── edac
├── event_source
├── genpd
├── gpio
├── hdaudio
├── hid
├── i2c
├── isa
├── machinecheck
├── mdio_bus
├── media
├── memory
├── mipi-dsi
├── mmc
├── nd
├── node
├── nvmem
├── pci
├── pci-epf
├── pci_express
├── platform
├── pnp
├── scsi
├── sdio
├── serial
├── serio
├── spi
├── usb
├── usb-serial
├── virtio
├── vme
├── wmi
├── workqueue
├── xen
└── xen-backend

42 directories, 0 files
```
* Contains subdirectories for physical bus type that has support registered in the kernel
* Each bus type that is represented has two subdir `devices` `drivers`
* The device directory contains a flat listing of every device discovered on that type of bus in the entire system.
* Devices listed are actually symbolic link that point to the device's directory in the global 
  device tree.
* `drivers` directory contains directories for each device driver that has been registered with the bus type. 
* Within each of the drivers dir, are attributes that allow viewing and manipulation of driver parame  ters, and symbolic links that point to the physical devices (in the global device tree) that the dr  iver is bound to.

##### Class
---

```text

/sys/class
├── ata_device
├── ata_link
├── ata_port
├── backlight
├── bdi
├── block
├── bluetooth
├── bsg
├── dax
...
├── scsi_host
├── sound
├── spi_master
├── spi_slave
├── thermal
├── tty
├── vc
├── video4linux
├── vtconsole
├── wakeup
├── watchdog
└── wmi_bus

62 directories, 0 files
```
* Contains representation fo every device class that is registered with the kernel.
* Each device class contains sdir for each class object that has been allocated and registered with that device class.
* For most of them, they contain symbolic link to the device and driver dir.
* Note that there is not necessarily a 1:1 mapping between class objects and physical devices; a physical device may contain multiple class objects that perform a different logical function.
* For example, a physical mouse device might be mapped to a kernel mosue device as well as a generic "input event" device and possibly a "input debug" device.
* Each class and objects may contain attributes exposing parameters that describe or control the class object.

##### Devices
---
* The devices directory contains the global devices global device hierarchy.
* Each of the device is shown as a subordinate device of the device that it is physically subordinate to.
* There are two type of devices that are exceptions to this representation:
  * Platform device
  * System devices
* Platform devices are basically peripherial devices that are inherent to a particular platform, usually have some I/O ports or MMIO that exists at a known, fixed location:
  * Example: A platform device is x86 devices like a serial controller or a floppy controller or the embedded devices of a SOC solution.
* System devices are non-peripheral devices that are integral components of the system. In many ways they are nothing like any other device. They mahy have some hardware register access for configuration, but donot hve the capability to transfer data. They usually donot have drivers which can be bound to them but atleast for those represented through sysfs, have some architecture-specific code that configures them and treats them enough as objects to export them:
  * Examples of system devices are CPU's APICs and timers.
```text
/sys/bus/pci/devices
├── 0000:00:00.0 -> ../../../devices/pci0000:00/0000:00:00.0
├── 0000:00:01.0 -> ../../../devices/pci0000:00/0000:00:01.0
├── 0000:00:01.1 -> ../../../devices/pci0000:00/0000:00:01.1
├── 0000:00:02.0 -> ../../../devices/pci0000:00/0000:00:02.0
```

##### firmware
---
* It contains interfaces for vieweing and manipulating firmware-specific objects and attributes.
* In this case, 'firmware' refers to the platform-specific code tha is executed on system power-on, likethe x86 BIOS, OpenFirmware on PPC platforms, and EFI on ia64 platforms.
* Each directory contains a set of objects and attributes that is specific to the firmware "driver in the kernel"
* For example, in the case of ACPI every object found in the ACPI DSDT table is listed in `firmware/acpi/namespace/` directory.

##### module
---
* The `module` directory contains subdirectories for each module that is loaded into the kernel.
* The name of each directory is the naem of the module -- both the name of the module object file and the internal name of the module. Every module is represented here, regardless of the subsystem it registers an object with. Note that the kernel has a single global namespace for all modules.
* Each module dir is a sdir called `sections`. This sdir contains attributes about the module sections.
* This information is used for debugging and generally not very interesting.
* Each module directory also contains at least one attribute: `refcnt` This attributes displays the current reference count or number of users of the module. This is the same value in the fourth column of `lsmod` output.

##### power
---
* represents power subsystem.
* Currently contains two attriutes:
  * disk: Disk suspension
  * state: Process to enter a low power state
* Reading this displays the state of the system.

### Code Organization
---
* Code resides in `fs/sysfs` and its shared function prototypes are in `include/linux/sysfs.h`
* Realtively small (~2000 lines), but it is divided up among 9 files.
* Files list:
  * `include/linux/sysfs.h` Shared header containing header file containing function prototypes
  * `fs/sysfs/sysfs.h` Internal header file for sysfs, shared locally among the sysfs source.
  * `fs/sysfs/mount.c` This contains the DS, methods and initialization functions necessary for interacting with the VFS layer.
  * `fs/sysfs/inode.c` File contains internal functions shared among the sysfs source for allocating and freeing the core filesystem objects.
  * `fs/sysfs/dir.c` Contains the externally visible sysfs interface responsible for creating and removing directories in the sysfs hierarchy.
  * `fs/sysfs/group.c` Contains a set of externally visible helpers that aide in creation and deletionof multiple regular files at a time.
  * `fs/sysfs/symlink.c` Contains externally visible interface for creating and removing symlink in the sysfs hierarchy.
  * `fs/sysfs/bin.c` Visible sysfs interface responsible for creating and removing binary (non-ASCII)files.

### Initialization

