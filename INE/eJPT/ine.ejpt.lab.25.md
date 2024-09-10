```jsx
Lab Name: Proxy Scaning
Platform: INE
Lab No: 25
Exam: eJPT (Jr. Penetartion Tester)
```

## Pinging:

```console
┌──(root㉿INE)-[~]
└─# ping demo.ine.local
PING demo.ine.local (192.225.127.3) 56(84) bytes of data.
64 bytes from demo.ine.local (192.225.127.3): icmp_seq=1 ttl=64 time=0.089 ms
64 bytes from demo.ine.local (192.225.127.3): icmp_seq=2 ttl=64 time=0.054 ms
64 bytes from demo.ine.local (192.225.127.3): icmp_seq=3 ttl=64 time=0.054 ms
64 bytes from demo.ine.local (192.225.127.3): icmp_seq=4 ttl=64 time=0.106 ms
^C
--- demo.ine.local ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3100ms
rtt min/avg/max/mdev = 0.054/0.075/0.106/0.022 ms
```

## NMAP Scan:

```console
┌──(root㉿INE)-[~]
└─# nmap -sV -script banner demo.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-09-10 11:29 IST
Nmap scan report for demo.ine.local (192.225.127.3)
Host is up (0.000022s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
25/tcp open  smtp    Postfix smtpd
|_banner: 220 openmailbox.xyz ESMTP Postfix: Welcome to our mail server.
MAC Address: 02:42:C0:E1:7F:03 (Unknown)
Service Info: Host:  openmailbox.xyz

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.36 seconds
```

## Enumaration:

```console
┌──(root㉿INE)-[~]
└─# telnet demo.ine.local 25
Trying 192.225.127.3...
Connected to demo.ine.local.
Escape character is '^]'.
220 openmailbox.xyz ESMTP Postfix: Welcome to our mail server.
HELO attacker.xyz
250 openmailbox.xyz
EHLO attacker.xyz
250-openmailbox.xyz
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250-STARTTLS
250-ENHANCEDSTATUSCODES
250-8BITMIME
250-DSN
250 SMTPUTF8
```

```console
┌──(root㉿INE)-[~]
└─# smtp-user-enum -U /usr/share/commix/src/txt/usernames.txt -t demo.ine.local
Starting smtp-user-enum v1.2 ( http://pentestmonkey.net/tools/smtp-user-enum )

 ----------------------------------------------------------
|                   Scan Information                       |
 ----------------------------------------------------------

Mode ..................... VRFY
Worker Processes ......... 5
Usernames file ........... /usr/share/commix/src/txt/usernames.txt
Target count ............. 1
Username count ........... 125
Target TCP port .......... 25
Query timeout ............ 5 secs
Target domain ............ 

######## Scan started at Tue Sep 10 11:48:38 2024 #########
 existse.local: admin
 existse.local: administrator
 existse.local: mail
 existse.local: postmaster
 existse.local: root
 existse.local: sales
 existse.local: support
demo.ine.local: www-data exists
######## Scan completed at Tue Sep 10 11:48:38 2024 #########
8 results.

125 queries in 1 seconds (125.0 queries / sec)
```

![image](https://github.com/user-attachments/assets/f4e749f7-171c-44f5-83a0-ad171861e714)

![image](https://github.com/user-attachments/assets/6f9fec4b-ce33-4812-8ffe-9a4c1dfaef13)

![image](https://github.com/user-attachments/assets/25e87509-052d-4d86-9289-664df8a6fa93)

---
