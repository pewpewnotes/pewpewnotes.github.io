### Nmap cheatsheet

listing ip adddress from system

1. nmap -sn 192.168.0.0/24 
2. nmap 192.168.0.0/24                | Service scan report
3. nmap -v [ip]                       | Verbose scanning
4. nmap [ip1] [ip2] [ip3]             | Scanning Multiple Host
5. nmap 192.168.0.\*                  | Scanning an entire subnet
6. nmap 192.168.0.101,102,103,104     | Scanning multiple systems
7. nmap -iL file.txt                  | A file which contains ip
8. nmap 192.168.0.101-110             | Range of ip
9. nmap [ip] --exclude [ipx]          | Exclude ipx
10. nmap -A [ip]                      | OS detection, traceroute etc
11. nmap -O [ip]                      | Os guessing
12. nmap -sA [ip]                     | detects if firewall is being used
13. nmap -sP 192.168.0.\*             | check alive nodes in network
14. -F                                | Fast scan
15. -V                                | Version
16. -r                                | Scan ports consecutively
17. --iflist                          | Host interface and route info
18. -p T/U[ports]                     | scan specific (T/U)cp/dp port

