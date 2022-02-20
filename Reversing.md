```

 ____                         _             
|  _ \ _____   _____ _ __ ___(_)_ __   __ _ 
| |_) / _ \ \ / / _ \ '__/ __| | '_ \ / _` |
|  _ <  __/\ V /  __/ |  \__ \ | | | | (_| |
|_| \_\___| \_/ \___|_|  |___/_|_| |_|\__, |
                                      |___/ 
```

### Reversing
<wikipedia reverse engineering>

### Links
* https://www.tenouk.com/Bufferoverflowc/bufferoverflowvulexploitdemo3.html
* Smashing stack for fun and profit, phrack49|14.txt

### Info
1. `segmentation fault (core dumped)` The dump is mostly reported to `ABRT` not dumped in cwd. (ABRT = Automated Bug reporting tool, not abort.) 
   `/var/crash/abrt` Might contain a copy and its distro dependent.
   `systemd in archlinux store coredumps in /var/lib/systemd/coredump/`: Stack overflow.
2. `-fno-stack-protector` Add this to disable stack smash prevention things.
3. ``` This stack frame will be constructed when a function call was triggered. The frame is bounded by the stack frame pointer (ebp) at the bottom and the stack pointer (esp) at the top. The return address, pointed to or hold by the instruction pointer (eip = ebp + 4) will be pushed into the stack after the arguments. During the execution the stack frame may shrink and grow and after the function call completed, the return address will be used to return to the caller and program execution continues. Then, the stack frame will be destroyed, releasing the memory to the system for other use. A simple idea is, if the return address can be changed, the program execution flows also can be changed. ```

* *Q* :Why do we need NOP? 

Well basically, for optimization and faster memory access the compiler 'optimizes' the stack size to a power of 2. Now this is what basically adds empty spaces or unused space on the stack, which can vary.

```
It is clear that the actual allocated buffer is 0x214 (532 bytes = 532 x 8 bits = 4256/32 = 133 words). The default is 4 (2 power to 2 that equal to 16 bytes or 128 bits) for this GCC version. This default stack growth can be changed by using the following GCC option.

-mpreferred-stack-boundary=num

Which the compiler will attempt to keep the stack boundary aligned to a 2 raised to num byte boundary. As the default, the stack is required to be aligned on a 4 byte boundary. Referring to the GCC documentation:

"To ensure proper alignment of these values on the stack, the stack boundary must be as aligned as that required by any value stored on the stack. Further, every function must be generated such that it keeps the stack aligned. Thus calling a function compiled with a higher preferred stack boundary from a function compiled with a lower preferred stack boundary will most likely misalign the stack. It is recommended that libraries that use callbacks always use the default setting.

This extra alignment does consume extra stack space. Code that is sensitive to stack space usage, such as embedded systems and operating system kernels, may want to reduce the preferred alignment to '-mpreferred-stack-boundary=2'."

This thing is very important if the malicious code will be stored in the stack itself as used in the classic stack-based buffer overflow. The actual allocated buffer for the declared array in the program needs to be known so that the string input size and arrangement can be properly prepared and setup. However, in the case where the return address is pointing back to the stack’s buffer, two options are available:

 

1.     Use the -mpreferred-stack-boundary=num gcc option to lower the preferred stack boundary or

2.     Padding more No Operation (NOP) instruction into the shellcode.
```

### Endianness

```
                            === Endiannesss Example ===
                            
Big Endian                   +--------------------------+           Little Endian
    +---+                    |       0x DEADBEEF        |              +---+
a   | DE|                    |                          |              | EF| a
a+1 | AD|                    +--------------------------+              | BE| a+1
a+2 | BE|                                                              | AD| a+2
a+3 | EF|                                                              | DE| a+3
..  |   |                                                              |   |  ..
..  |   |                                                              |   |  ..                                                  +---+                                                              +---|

```

* Get shellcode from objdump:
```
   for i in `objdump -d shellcode.o | tr '\t' ' ' | tr ' ' '\n' | egrep '^[0-9a-f]{2}$' ` ; do echo -n "\x$i" ; done
```
* https://vividmachines.com/shellcode/shellcode.html
* 
