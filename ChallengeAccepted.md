```
  ____ _           _ _                       
 / ___| |__   __ _| | | ___ _ __   __ _  ___ 
| |   | '_ \ / _` | | |/ _ \ '_ \ / _` |/ _ \
| |___| | | | (_| | | |  __/ | | | (_| |  __/
 \____|_| |_|\__,_|_|_|\___|_| |_|\__, |\___|
                                  |___/      
    _                      _           _ 
   / \   ___ ___ ___ _ __ | |_ ___  __| |
  / _ \ / __/ __/ _ \ '_ \| __/ _ \/ _` |
 / ___ \ (_| (_|  __/ |_) | ||  __/ (_| |
/_/   \_\___\___\___| .__/ \__\___|\__,_|
                    |_|                  
```
* [Chromium OS syscalls](https://chromium.googlesource.com/chromiumos/docs/+/master/constants/syscalls.md)
* [New link: Syscalls](https://chromium.googlesource.com/chromiumos/docs/+/HEAD/constants/syscalls.md)

A system call allows a userspace program to interface with kernel, the protection mechanism prevents  programs from interfering with kernel, thus it needs cooperation with HW/SW interrupts to transition from userspace to kernel space. 
To invoke a syscall, we have a use of multiple registers, basically Each of these registers, contain a parameter, and use that for making the syscall. Before we delve into modus operandi, it is important to know what all registers are generally involved and how they are onvolved as well.

| register | Purpose                                                                           |
| RAX      | Contains syscall number, defined in /usr/include/x86_64-linux-gnu/asm/unistd_64.h |
| RDI      | Contains value of first argument                                                  |
| RSI      | Second Argument                                                                   |
| RDX      | 3rd Argument                                                                      |
| r10      | 4th argument                                                                      |
| r8       | 5th argument                                                                      |
| r9       | 6th argument                                                                      |

The exit syscall is 60, so we move 60 into RAX. The Only argument is exit status, henceforth we put 0 in RDI.

```
mov rax,60
mov rdi,0
```

A simple code to print a message on screen. The write syscall has the underlying signature, 
size_t write(int fd,const void *buf,size_t count)
check man 2 write (if its not in arch, install man-pages package)
First argument is file descriptor, which is 0 for stdin, 1 for stdout and 2 for stderr.
to print a message to screen, we need to write to stdout which means FD 1.
the syscall for write is 1, hence 1 -> RAX.
first argument goes into RDI, henceforth 1 -> RDI (for stdout)
the third argument has the size of the buffer, which we will put in RDX reg.

```
global _start
section .text
_start:
mov rax, 1
mov rdi, 1
mov rsi, my_message
mov rdx, length
syscall
section .data
my_message:db'my first syscall',0xa
length:equ $-my_message
```
In this code we get segfault for sure, because we don't know where to return after executing the syscall, henceforth we gotta add an exit syscall for the same.

```
global _start
section .text
_start:
mov rax, 1
mov rdi, 1
mov rsi, my_message
mov rdx, length
syscall
mov rax, 60
mox rdi, 1
syscall

section .data
my_message:db'my first syscall',0xa
length:equ $-my_message
```

```bash
nasm -f elf64 syscall_write.asm -o syscall_write.o
ld syscall_write.o -o syscall_write
./syscall_write
```

### Fundamental Data types
* Byte - 8 bits
* Word - 16 bits
* Double Word - 32 bits
* Quad Word - 64 bits
* Double Quad word - 128 bits

