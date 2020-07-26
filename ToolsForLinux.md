#Well this basically includes my tools for linux and stuffs,
##they good
+---------------------------------------------------------+
|                      Applications                       |
+           +---------------------------------------------+
+           +---------------------------------------------+
|           |              System Libraries               |
|-----------+---------------------------------------------+
+---------------------------------------------------------+
|                  System call Interface                  |
+---------------------------------------------------------+
+--------------------------------------------------------+
+-         VFS         -++-    Sockets     -+------------+
+-----------------------++------------------| Scheduler  |
|     File Systems      ||     TCP/UDP      |            |
+-----------------------+-------------------+------------+
+-   Volume Manager    -|        IP         |  Virtual   |
+-----------------------+-------------------|   Memory   |
|     Block device      |     Ethernet      |            |
+--------------------------------------------------------+
|                     Device Drivers                     |
+--------------------------------------------------------+
                         | 
                         |
                         v
            +-------------------------------+
            |          I/O bridge           |
            +-------------------------------+
                         +
                         |
                         |
                         v
<--+-------------------------------------------------+---->
   |                                                 |
   v                                                 v
+-  I/O controller  -+------------------------------------------+
|    [disk/swap]     |        Network Controller [Port]         |
+--------------------+------------------------------------------+

##Tools

1) ``Strace`` 
2) ``ltrace``
3) ``ss``
4) ``Netstat`` for tcp|udp|IP|ethernet|sockets
5) ``iptraf`` Ethernet|IP|TCP|UDP
6) ``tcpdump`` Ethernet
7) ``vmstat`` ``slabtop`` ``free`` [Virtual memory dram]
8) ``top`` ``ps`` cpu
9) ``perf`` ``tiptop`` Memory bus
10) `iostat iotop blktrace` Block device interface
11) `sysdig` syscall interface
12) `swapon` for swap 
13) ``ethtool snmpget lldptool nicstat ip``  Network controller


* Process status listing, ascii tree style
 `ps -ef f`````

* Virtual memory statistics and more 
* `vmstat -Sm -l `
* mpstat for multiprocessor stats
* Main memory usage `free -m`
* strace is syscall tracer 
* `tcpdump` tcpdump -i eth0 -w pewpewfile
* `nicstat` for network stats [**Look into it more**]
* `sar` system activity reporter
* ss -mop socket stats

* For seeing the memory used by a process: 
`ps -o user,%mem,command ax | sort -b -k3 -r | grep "evilvte"`

















