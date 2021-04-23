# TryMeHacking
# Vulnversity

 #### Recon and Stuffs
```
❯ nmap -sV 10.10.196.235

Starting Nmap 7.60 ( https://nmap.org ) at 2020-04-16 16:57 IST
Note: Host seems down. If it is really up, but blocking our ping probes, try -Pn
Nmap done: 1 IP address (0 hosts up) scanned in 5.67 seconds
❯ nmap -sV -Pn 10.10.196.235

Starting Nmap 7.60 ( https://nmap.org ) at 2020-04-16 16:58 IST

❯ nmap -Pn 10.10.196.235

Starting Nmap 7.60 ( https://nmap.org ) at 2020-04-16 16:59 IST
Nmap scan report for 10.10.196.235
Host is up (0.14s latency).
Not shown: 994 closed ports
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3128/tcp open  squid-http
3333/tcp open  dec-notes

Nmap done: 1 IP address (1 host up) scanned in 21.90 seconds
❯ nmap -A -Pn 10.10.196.235

Starting Nmap 7.60 ( https://nmap.org ) at 2020-04-16 17:00 IST

❯ nmap -A 400 10.10.196.235

Starting Nmap 7.60 ( https://nmap.org ) at 2020-04-16 17:01 IST
Strange read error from 0.0.1.144 (22 - 'Invalid argument')
Strange read error from 0.0.1.144 (22 - 'Invalid argument')

❯ nmap -A -p400 10.10.196.235

Starting Nmap 7.60 ( https://nmap.org ) at 2020-04-16 17:01 IST
Nmap scan report for 10.10.196.235
Host is up (0.17s latency).

PORT    STATE  SERVICE  VERSION
400/tcp closed work-sol

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 2.65 seconds
❯ nmap -A -p3128 10.10.196.235

Starting Nmap 7.60 ( https://nmap.org ) at 2020-04-16 17:01 IST
Nmap scan report for 10.10.196.235
Host is up (0.19s latency).

PORT     STATE SERVICE    VERSION
3128/tcp open  http-proxy Squid http proxy 3.5.12
|_http-server-header: squid/3.5.12
|_http-title: ERROR: The requested URL could not be retrieved

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 32.39 seconds
❯ nmap -p-400 10.10.196.235

Starting Nmap 7.60 ( https://nmap.org ) at 2020-04-16 17:02 IST
Nmap scan report for 10.10.196.235
Host is up (0.14s latency).
Not shown: 397 closed ports
PORT    STATE SERVICE
21/tcp  open  ftp
22/tcp  open  ssh
139/tcp open  netbios-ssn

Nmap done: 1 IP address (1 host up) scanned in 4.52 seconds
❯ nmap --help | grep "-n"

```
 #### For OS and service version
```
❯ cat dump | grep "\-n"
  -n/-R: Never do DNS resolution/Always resolve [default: sometimes]
  --no-stylesheet: Prevent associating of XSL stylesheet w/XML output
❯ nc 10.10.196.235 8080
❯ nc 10.10.196.235 8000
❯ nc 10.10.196.235 80
❯ nmap -A 10.10.196.235

Starting Nmap 7.60 ( https://nmap.org ) at 2020-04-16 17:05 IST
Nmap scan report for 10.10.196.235
Host is up (0.14s latency).
Not shown: 994 closed ports
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 3.0.3
22/tcp   open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 5a:4f:fc:b8:c8:76:1c:b5:85:1c:ac:b2:86:41:1c:5a (RSA)
|   256 ac:9d:ec:44:61:0c:28:85:00:88:e9:68:e9:d0:cb:3d (ECDSA)
|_  256 30:50:cb:70:5a:86:57:22:cb:52:d9:36:34:dc:a5:58 (EdDSA)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
3128/tcp open  http-proxy  Squid http proxy 3.5.12
|_http-server-header: squid/3.5.12
|_http-title: ERROR: The requested URL could not be retrieved
3333/tcp open  http        Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Vuln University
Service Info: Host: VULNUNIVERSITY; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_nbstat: NetBIOS name: VULNUNIVERSITY, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: vulnuniversity
|   NetBIOS computer name: VULNUNIVERSITY\x00
|   Domain name: \x00
|   FQDN: vulnuniversity
|_  System time: 2020-04-16T07:35:53-04:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2020-04-16 17:05:54
|_  start_date: 1601-01-01 05:53:28

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 58.24 seconds


```

 ### Directory Scanning
```
===============================================================
❯ gobuster dir -u http://10.10.196.235:3333 -w ./small.txt
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.196.235:3333
[+] Threads:        10
[+] Wordlist:       ./small.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2020/04/16 18:19:50 Starting gobuster
===============================================================
/css (Status: 301)
/images (Status: 301)
/internal (Status: 301)
/js (Status: 301)
===============================================================
2020/04/16 18:20:05 Finished
===============================================================
❯ gobuster dir -u http://10.10.196.235:3333 -w ./big.txt
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.196.235:3333
[+] Threads:        10
[+] Wordlist:       ./big.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2020/04/16 18:20:14 Starting gobuster
===============================================================
/.htaccess (Status: 403)
/.htpasswd (Status: 403)
/css (Status: 301)
/fonts (Status: 301)
/images (Status: 301)
/internal (Status: 301)
/js (Status: 301)
/server-status (Status: 403)
===============================================================
2020/04/16 18:25:23 Finished
===============================================================

╭─░▒▓    ~/So/Hac/wordlists 

```

# Note

