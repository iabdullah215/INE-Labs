```jsx
Lab Name: Windows Recon: SMB Nmap Scripts
Platform: INE
Lab No: 03
Exam: eJPT (Jr. Penetartion Tester)
```

## Pinging:

```console
┌──(root㉿INE)-[~]
└─# ping -c 5 demo.ine.local
PING demo.ine.local (10.4.27.179) 56(84) bytes of data.
64 bytes from demo.ine.local (10.4.27.179): icmp_seq=1 ttl=125 time=10.2 ms
64 bytes from demo.ine.local (10.4.27.179): icmp_seq=2 ttl=125 time=8.86 ms
64 bytes from demo.ine.local (10.4.27.179): icmp_seq=3 ttl=125 time=8.81 ms
64 bytes from demo.ine.local (10.4.27.179): icmp_seq=4 ttl=125 time=8.97 ms
64 bytes from demo.ine.local (10.4.27.179): icmp_seq=5 ttl=125 time=8.78 ms

--- demo.ine.local ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4005ms
rtt min/avg/max/mdev = 8.775/9.122/10.191/0.538 ms
```

## Scanning:

```console
┌──(root㉿INE)-[~]
└─# nmap demo.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 18:46 IST
Nmap scan report for demo.ine.local (10.4.27.179)
Host is up (0.0088s latency).
Not shown: 992 closed tcp ports (reset)
PORT      STATE SERVICE
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
3389/tcp  open  ms-wbt-server
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown
49155/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 1.36 seconds
```

## SMB Scripts:

```console
┌──(root㉿INE)-[~]
└─# nmap -p445 --script smb-protocols demo.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 18:47 IST
Nmap scan report for demo.ine.local (10.4.27.179)
Host is up (0.0089s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:                                                                                                                                                                       
| smb-protocols: 
|   dialects: 
|     NT LM 0.12 (SMBv1) [dangerous, but default]
|     2:0:2
|     2:1:0
|     3:0:0
|_    3:0:2

Nmap done: 1 IP address (1 host up) scanned in 5.26 seconds
```

---

```console
┌──(root㉿INE)-[~]
└─# nmap -p445 --script smb-security-mode demo.ine.local                                                                                                                                   
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 18:47 IST
Nmap scan report for demo.ine.local (10.4.27.179)
Host is up (0.0088s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)

Nmap done: 1 IP address (1 host up) scanned in 1.19 seconds
```

---

```console
┌──(root㉿INE)-[~]
└─# nmap -p445 --script smb-enum-sessions demo.ine.local                                                                                                                                   
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 18:48 IST
Nmap scan report for demo.ine.local (10.4.27.179)
Host is up (0.0088s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-enum-sessions: 
|   Users logged in
|_    WIN-OMCNBKR66MN\bob since <unknown>

Nmap done: 1 IP address (1 host up) scanned in 3.87 seconds
```

---

```console
┌──(root㉿INE)-[~]
└─# nmap -p445 --script smb-enum-sessions --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local                                                                 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 18:49 IST
Nmap scan report for demo.ine.local (10.4.27.179)
Host is up (0.0087s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-enum-sessions: 
|   Users logged in
|     WIN-OMCNBKR66MN\bob since 2024-08-17T13:12:03
|   Active SMB sessions
|_    ADMINISTRATOR is connected from \\10.10.46.5 for [just logged in, it's probably you], idle for [not idle]

Nmap done: 1 IP address (1 host up) scanned in 3.89 seconds
```

---

```console
┌──(root㉿INE)-[~]
└─# nmap -p445 --script smb-enum-shares demo.ine.local                                                                                                                                                                                     
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 18:49 IST
Nmap scan report for demo.ine.local (10.4.27.179)
Host is up (0.011s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-enum-shares: 
|   account_used: guest
|   \\10.4.27.179\ADMIN$: 
|     Type: STYPE_DISKTREE_HIDDEN
|     Comment: Remote Admin
|     Anonymous access: <none>
|     Current user access: <none>
|   \\10.4.27.179\C: 
|     Type: STYPE_DISKTREE
|     Comment: 
|     Anonymous access: <none>
|     Current user access: READ
|   \\10.4.27.179\C$: 
|     Type: STYPE_DISKTREE_HIDDEN
|     Comment: Default share
|     Anonymous access: <none>
|     Current user access: <none>
|   \\10.4.27.179\D$: 
|     Type: STYPE_DISKTREE_HIDDEN
|     Comment: Default share
|     Anonymous access: <none>
|     Current user access: <none>
|   \\10.4.27.179\Documents: 
|     Type: STYPE_DISKTREE
|     Comment: 
|     Anonymous access: <none>
|     Current user access: READ
|   \\10.4.27.179\Downloads: 
|     Type: STYPE_DISKTREE
|     Comment: 
|     Anonymous access: <none>
|     Current user access: READ
|   \\10.4.27.179\IPC$: 
|     Type: STYPE_IPC_HIDDEN
|     Comment: Remote IPC
|     Anonymous access: <none>
|     Current user access: READ/WRITE
|   \\10.4.27.179\print$: 
|     Type: STYPE_DISKTREE
|     Comment: Printer Drivers
|     Anonymous access: <none>
|_    Current user access: READ

Nmap done: 1 IP address (1 host up) scanned in 46.45 seconds
```

---

```console
┌──(root㉿INE)-[~]
└─# nmap -p445 --script smb-enum-shares --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local                                                                                                                   
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 18:51 IST
Nmap scan report for demo.ine.local (10.4.27.179)
Host is up (0.0096s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-enum-shares: 
|   account_used: administrator
|   \\10.4.27.179\ADMIN$: 
|     Type: STYPE_DISKTREE_HIDDEN
|     Comment: Remote Admin
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\Windows
|     Anonymous access: <none>
|     Current user access: READ/WRITE
|   \\10.4.27.179\C: 
|     Type: STYPE_DISKTREE
|     Comment: 
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\
|     Anonymous access: <none>
|     Current user access: READ
|   \\10.4.27.179\C$: 
|     Type: STYPE_DISKTREE_HIDDEN
|     Comment: Default share
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\
|     Anonymous access: <none>
|     Current user access: READ/WRITE
|   \\10.4.27.179\D$: 
|     Type: STYPE_DISKTREE_HIDDEN
|     Comment: Default share
|     Users: 0
|     Max Users: <unlimited>
|     Path: D:\
|     Anonymous access: <none>
|     Current user access: READ/WRITE
|   \\10.4.27.179\Documents: 
|     Type: STYPE_DISKTREE
|     Comment: 
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\Users\Administrator\Documents
|     Anonymous access: <none>
|     Current user access: READ
|   \\10.4.27.179\Downloads: 
|     Type: STYPE_DISKTREE
|     Comment: 
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\Users\Administrator\Downloads
|     Anonymous access: <none>
|     Current user access: READ
|   \\10.4.27.179\IPC$: 
|     Type: STYPE_IPC_HIDDEN
|     Comment: Remote IPC
|     Users: 1
|     Max Users: <unlimited>
|     Path: 
|     Anonymous access: <none>
|     Current user access: READ/WRITE
|   \\10.4.27.179\print$: 
|     Type: STYPE_DISKTREE
|     Comment: Printer Drivers
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\Windows\system32\spool\drivers
|     Anonymous access: <none>
|_    Current user access: READ/WRITE

Nmap done: 1 IP address (1 host up) scanned in 50.71 seconds
```

---

```console
┌──(root㉿INE)-[~]
└─# nmap -p445 --script smb-enum-users --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local                                                                    
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 18:54 IST
Nmap scan report for demo.ine.local (10.4.27.179)
Host is up (0.010s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-enum-users: 
|   WIN-OMCNBKR66MN\Administrator (RID: 500)
|     Description: Built-in account for administering the computer/domain
|     Flags:       Normal user account, Password does not expire
|   WIN-OMCNBKR66MN\bob (RID: 1010)
|     Flags:       Normal user account, Password does not expire
|   WIN-OMCNBKR66MN\Guest (RID: 501)
|     Description: Built-in account for guest access to the computer/domain
|_    Flags:       Normal user account, Password does not expire, Password not required

Nmap done: 1 IP address (1 host up) scanned in 4.52 seconds
```

---

```console
┌──(root㉿INE)-[~]
└─# nmap -p445 --script smb-server-stats --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local                                                                  
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 18:54 IST
Nmap scan report for demo.ine.local (10.4.27.179)
Host is up (0.0098s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-server-stats: 
|   Server statistics collected since 2024-08-17T13:10:33 (14m19s):
|     94602 bytes (110.13 b/s) sent, 80383 bytes (93.58 b/s) received
|_    34 failed logins, 7 permission errors, 0 system errors, 0 print jobs, 35 files opened

Nmap done: 1 IP address (1 host up) scanned in 1.28 seconds
```

---

```console
┌──(root㉿INE)-[~]
└─# nmap -p445 --script smb-enum-domains --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local                                                                  
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 18:56 IST
Nmap scan report for demo.ine.local (10.4.27.179)
Host is up (0.014s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-enum-domains: 
|   Builtin
|     Groups: Access Control Assistance Operators, Administrators, Backup Operators, Certificate Service DCOM Access, Cryptographic Operators, Distributed COM Users, Event Log Readers, Guests, Hyper-V Administrators, IIS_IUSRS, Network Configuration Operators, Performance Log Users, Performance Monitor Users, Power Users, Print Operators, RDS Endpoint Servers, RDS Management Servers, RDS Remote Access Servers, Remote Desktop Users, Remote Management Users, Replicator, Users
|     Users: n/a
|     Creation time: 2013-08-22T14:47:57
|     Passwords: min length: n/a; min age: n/a days; max age: 42 days; history: n/a passwords
|     Account lockout disabled
|   WIN-OMCNBKR66MN
|     Groups: WinRMRemoteWMIUsers__
|     Users: Administrator, bob, Guest
|     Creation time: 2013-08-22T14:47:57
|     Passwords: min length: n/a; min age: n/a days; max age: 42 days; history: n/a passwords
|     Properties: Complexity requirements exist
|_    Account lockout disabled

Nmap done: 1 IP address (1 host up) scanned in 3.88 seconds
```

---

```console
┌──(root㉿INE)-[~]
└─# nmap -p445 --script smb-enum-groups --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local                                                                   
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 18:56 IST
Nmap scan report for demo.ine.local (10.4.27.179)
Host is up (0.0094s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-enum-groups: 
|   Builtin\Administrators (RID: 544): Administrator, bob
|   Builtin\Users (RID: 545): bob
|   Builtin\Guests (RID: 546): Guest
|   Builtin\Power Users (RID: 547): <empty>
|   Builtin\Print Operators (RID: 550): <empty>
|   Builtin\Backup Operators (RID: 551): <empty>
|   Builtin\Replicator (RID: 552): <empty>
|   Builtin\Remote Desktop Users (RID: 555): bob
|   Builtin\Network Configuration Operators (RID: 556): <empty>
|   Builtin\Performance Monitor Users (RID: 558): <empty>
|   Builtin\Performance Log Users (RID: 559): <empty>
|   Builtin\Distributed COM Users (RID: 562): <empty>
|   Builtin\IIS_IUSRS (RID: 568): <empty>
|   Builtin\Cryptographic Operators (RID: 569): <empty>
|   Builtin\Event Log Readers (RID: 573): <empty>
|   Builtin\Certificate Service DCOM Access (RID: 574): <empty>
|   Builtin\RDS Remote Access Servers (RID: 575): <empty>
|   Builtin\RDS Endpoint Servers (RID: 576): <empty>
|   Builtin\RDS Management Servers (RID: 577): <empty>
|   Builtin\Hyper-V Administrators (RID: 578): <empty>
|   Builtin\Access Control Assistance Operators (RID: 579): <empty>
|   Builtin\Remote Management Users (RID: 580): <empty>
|_  WIN-OMCNBKR66MN\WinRMRemoteWMIUsers__ (RID: 1000): <empty>

Nmap done: 1 IP address (1 host up) scanned in 4.40 seconds
```

---

```console
┌──(root㉿INE)-[~]
└─# nmap -p445 --script smb-enum-groups --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local                                                                                                                   
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 18:56 IST
Nmap scan report for demo.ine.local (10.4.27.179)
Host is up (0.0094s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-enum-groups: 
|   Builtin\Administrators (RID: 544): Administrator, bob
|   Builtin\Users (RID: 545): bob
|   Builtin\Guests (RID: 546): Guest
|   Builtin\Power Users (RID: 547): <empty>
|   Builtin\Print Operators (RID: 550): <empty>
|   Builtin\Backup Operators (RID: 551): <empty>
|   Builtin\Replicator (RID: 552): <empty>
|   Builtin\Remote Desktop Users (RID: 555): bob
|   Builtin\Network Configuration Operators (RID: 556): <empty>
|   Builtin\Performance Monitor Users (RID: 558): <empty>
|   Builtin\Performance Log Users (RID: 559): <empty>
|   Builtin\Distributed COM Users (RID: 562): <empty>
|   Builtin\IIS_IUSRS (RID: 568): <empty>
|   Builtin\Cryptographic Operators (RID: 569): <empty>
|   Builtin\Event Log Readers (RID: 573): <empty>
|   Builtin\Certificate Service DCOM Access (RID: 574): <empty>
|   Builtin\RDS Remote Access Servers (RID: 575): <empty>
|   Builtin\RDS Endpoint Servers (RID: 576): <empty>
|   Builtin\RDS Management Servers (RID: 577): <empty>
|   Builtin\Hyper-V Administrators (RID: 578): <empty>
|   Builtin\Access Control Assistance Operators (RID: 579): <empty>
|   Builtin\Remote Management Users (RID: 580): <empty>
|_  WIN-OMCNBKR66MN\WinRMRemoteWMIUsers__ (RID: 1000): <empty>

Nmap done: 1 IP address (1 host up) scanned in 4.40 seconds

┌──(root㉿INE)-[~]
└─# nmap -p445 --script smb-enum-services --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local                                                                                                                 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 18:57 IST
Nmap scan report for demo.ine.local (10.4.27.179)
Host is up (0.0093s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds
| smb-enum-services: 
|   AmazonSSMAgent: 
|     display_name: Amazon SSM Agent
|     state: 
|       SERVICE_CONTINUE_PENDING
|       SERVICE_PAUSED
|       SERVICE_PAUSE_PENDING
|       SERVICE_RUNNING
|     type: 
|       SERVICE_TYPE_WIN32_OWN_PROCESS
|       SERVICE_TYPE_WIN32
|     controls_accepted: 
|       SERVICE_CONTROL_NETBINDENABLE
|       SERVICE_CONTROL_NETBINDADD
|       SERVICE_CONTROL_CONTINUE
|       SERVICE_CONTROL_STOP
|       SERVICE_CONTROL_PARAMCHANGE
|       SERVICE_CONTROL_INTERROGATE
|   DiagTrack: 
|     display_name: Diagnostics Tracking Service
|     state: 
|       SERVICE_CONTINUE_PENDING
|       SERVICE_PAUSED
|       SERVICE_PAUSE_PENDING
|       SERVICE_RUNNING
|     type: 
|       SERVICE_TYPE_WIN32_OWN_PROCESS
|       SERVICE_TYPE_WIN32
|     controls_accepted: 
|       SERVICE_CONTROL_NETBINDENABLE
|       SERVICE_CONTROL_NETBINDADD
|       SERVICE_CONTROL_CONTINUE
|       SERVICE_CONTROL_STOP
|       SERVICE_CONTROL_PARAMCHANGE
|       SERVICE_CONTROL_INTERROGATE
|   Ec2Config: 
|     display_name: Ec2Config
|     state: 
|       SERVICE_CONTINUE_PENDING
|       SERVICE_PAUSED
|       SERVICE_PAUSE_PENDING
|       SERVICE_RUNNING
|     type: 
|       SERVICE_TYPE_WIN32_OWN_PROCESS
|       SERVICE_TYPE_WIN32
|     controls_accepted: 
|       SERVICE_CONTROL_NETBINDENABLE
|       SERVICE_CONTROL_NETBINDADD
|       SERVICE_CONTROL_CONTINUE
|       SERVICE_CONTROL_STOP
|       SERVICE_CONTROL_PARAMCHANGE
|       SERVICE_CONTROL_INTERROGATE
|   MSDTC: 
|     display_name: Distributed Transaction Coordinator
|     state: 
|       SERVICE_CONTINUE_PENDING
|       SERVICE_PAUSED
|       SERVICE_PAUSE_PENDING
|       SERVICE_RUNNING
|     type: 
|       SERVICE_TYPE_WIN32_OWN_PROCESS
|       SERVICE_TYPE_WIN32
|     controls_accepted: 
|       SERVICE_CONTROL_NETBINDENABLE
|       SERVICE_CONTROL_NETBINDADD
|       SERVICE_CONTROL_CONTINUE
|       SERVICE_CONTROL_STOP
|       SERVICE_CONTROL_PARAMCHANGE
|       SERVICE_CONTROL_INTERROGATE
|   Spooler: 
|     display_name: Print Spooler
|     state: 
|       SERVICE_CONTINUE_PENDING
|       SERVICE_PAUSED
|       SERVICE_PAUSE_PENDING
|       SERVICE_RUNNING
|     type: 
|       SERVICE_TYPE_WIN32_OWN_PROCESS
|       SERVICE_TYPE_WIN32
|     controls_accepted: 
|       SERVICE_CONTROL_NETBINDENABLE
|       SERVICE_CONTROL_NETBINDADD
|       SERVICE_CONTROL_CONTINUE
|_      SERVICE_CONTROL_STOP

Nmap done: 1 IP address (1 host up) scanned in 1.32 seconds
```

---

```console
┌──(root㉿INE)-[~]
└─# nmap -p445 --script smb-enum-shares,smb-ls --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local                                                                                                            
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 18:58 IST
Nmap scan report for demo.ine.local (10.4.27.179)
Host is up (0.0094s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-ls: Volume \\10.4.27.179\ADMIN$
|   maxfiles limit reached (10)
| SIZE   TIME                 FILENAME
| <DIR>  2013-08-22T13:36:16  .
| <DIR>  2013-08-22T13:36:16  ..
| <DIR>  2013-08-22T15:39:31  ADFS
| <DIR>  2013-08-22T15:39:31  ADFS\ar
| <DIR>  2013-08-22T15:39:31  ADFS\bg
| <DIR>  2013-08-22T15:39:31  ADFS\cs
| <DIR>  2013-08-22T15:39:31  ADFS\da
| <DIR>  2013-08-22T15:39:31  ADFS\de
| <DIR>  2013-08-22T15:39:31  ADFS\el
| <DIR>  2013-08-22T15:39:31  ADFS\en
| 
| 
| Volume \\10.4.27.179\C
|   maxfiles limit reached (10)
| SIZE   TIME                 FILENAME
| <DIR>  2013-08-22T15:39:30  PerfLogs
| <DIR>  2013-08-22T13:36:16  Program Files
| <DIR>  2014-05-17T10:36:57  Program Files\Amazon
| <DIR>  2013-08-22T13:36:16  Program Files\Common Files
| <DIR>  2014-10-15T05:58:49  Program Files\DIFX
| <DIR>  2013-08-22T15:39:31  Program Files\Internet Explorer
| <DIR>  2014-07-10T18:40:15  Program Files\Update Services
| <DIR>  2020-08-12T04:13:47  Program Files\Windows Mail
| <DIR>  2013-08-22T15:39:31  Program Files\Windows NT
| <DIR>  2013-08-22T15:39:31  Program Files\WindowsPowerShell
| 
| 
| Volume \\10.4.27.179\C$
|   maxfiles limit reached (10)
| SIZE   TIME                 FILENAME
| <DIR>  2013-08-22T15:39:30  PerfLogs
| <DIR>  2013-08-22T13:36:16  Program Files
| <DIR>  2014-05-17T10:36:57  Program Files\Amazon
| <DIR>  2013-08-22T13:36:16  Program Files\Common Files
| <DIR>  2014-10-15T05:58:49  Program Files\DIFX
| <DIR>  2013-08-22T15:39:31  Program Files\Internet Explorer
| <DIR>  2014-07-10T18:40:15  Program Files\Update Services
| <DIR>  2020-08-12T04:13:47  Program Files\Windows Mail
| <DIR>  2013-08-22T15:39:31  Program Files\Windows NT
| <DIR>  2013-08-22T15:39:31  Program Files\WindowsPowerShell
| 
| 
| Volume \\10.4.27.179\Documents
| SIZE   TIME                 FILENAME
| <DIR>  2020-09-10T09:50:27  .
| <DIR>  2020-09-10T09:50:27  ..
| 
| 
| Volume \\10.4.27.179\Downloads
| SIZE   TIME                 FILENAME
| <DIR>  2020-09-10T09:50:27  .
| <DIR>  2020-09-10T09:50:27  ..
| 
| 
| Volume \\10.4.27.179\print$
|   maxfiles limit reached (10)
| SIZE    TIME                 FILENAME
| <DIR>   2013-08-22T15:39:31  .
| <DIR>   2013-08-22T15:39:31  ..
| <DIR>   2013-08-22T15:39:31  color
| 1058    2013-08-22T06:54:44  color\D50.camp
| 1079    2013-08-22T06:54:44  color\D65.camp
| 797     2013-08-22T06:54:44  color\Graphics.gmmp
| 838     2013-08-22T06:54:44  color\MediaSim.gmmp
| 786     2013-08-22T06:54:44  color\Photo.gmmp
| 822     2013-08-22T06:54:44  color\Proofing.gmmp
| 218103  2013-08-22T06:54:44  color\RSWOP.icm
|_
| smb-enum-shares: 
|   account_used: administrator
|   \\10.4.27.179\ADMIN$: 
|     Type: STYPE_DISKTREE_HIDDEN
|     Comment: Remote Admin
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\Windows
|     Anonymous access: <none>
|     Current user access: READ/WRITE
|   \\10.4.27.179\C: 
|     Type: STYPE_DISKTREE
|     Comment: 
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\
|     Anonymous access: <none>
|     Current user access: READ
|   \\10.4.27.179\C$: 
|     Type: STYPE_DISKTREE_HIDDEN
|     Comment: Default share
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\
|     Anonymous access: <none>
|     Current user access: READ/WRITE
|   \\10.4.27.179\D$: 
|     Type: STYPE_DISKTREE_HIDDEN
|     Comment: Default share
|     Users: 0
|     Max Users: <unlimited>
|     Path: D:\
|     Anonymous access: <none>
|     Current user access: READ/WRITE
|   \\10.4.27.179\Documents: 
|     Type: STYPE_DISKTREE
|     Comment: 
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\Users\Administrator\Documents
|     Anonymous access: <none>
|     Current user access: READ
|   \\10.4.27.179\Downloads: 
|     Type: STYPE_DISKTREE
|     Comment: 
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\Users\Administrator\Downloads
|     Anonymous access: <none>
|     Current user access: READ
|   \\10.4.27.179\IPC$: 
|     Type: STYPE_IPC_HIDDEN
|     Comment: Remote IPC
|     Users: 1
|     Max Users: <unlimited>
|     Path: 
|     Anonymous access: <none>
|     Current user access: READ/WRITE
|   \\10.4.27.179\print$: 
|     Type: STYPE_DISKTREE
|     Comment: Printer Drivers
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\Windows\system32\spool\drivers
|     Anonymous access: <none>
|_    Current user access: READ/WRITE

Nmap done: 1 IP address (1 host up) scanned in 58.39 seconds
```

---
