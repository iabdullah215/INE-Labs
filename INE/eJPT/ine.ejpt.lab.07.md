```jsx
Lab Name: Windows Recon: SMBMap
Platform: INE
Lab No: 07
Exam: eJPT (Jr. Penetartion Tester)
```

## Pinging:

```console
┌──(root㉿INE)-[~]
└─# ping demo.ine.local
PING demo.ine.local (10.4.31.245) 56(84) bytes of data.
64 bytes from demo.ine.local (10.4.31.245): icmp_seq=1 ttl=125 time=9.78 ms
64 bytes from demo.ine.local (10.4.31.245): icmp_seq=2 ttl=125 time=8.85 ms
64 bytes from demo.ine.local (10.4.31.245): icmp_seq=3 ttl=125 time=8.85 ms
64 bytes from demo.ine.local (10.4.31.245): icmp_seq=4 ttl=125 time=8.73 ms
^Z
[1]+  Stopped                 ping demo.ine.local
```

## NMAP Scan:

```console
┌──(root㉿INE)-[~]
└─# nmap demo.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-23 15:23 IST
Nmap scan report for demo.ine.local (10.4.31.245)
Host is up (0.0092s latency).
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

```console
┌──(root㉿INE)-[~]
└─# nmap -p445 --script smb-protocols demo.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-23 15:25 IST
Nmap scan report for demo.ine.local (10.4.31.245)
Host is up (0.0090s latency).

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

## SMB Map:

```console
┌──(root㉿INE)-[~]
└─# smbmap -u administrator -p smbserver_771 -d . -H demo.ine.local

    ________  ___      ___  _______   ___      ___       __         _______
   /"       )|"  \    /"  ||   _  "\ |"  \    /"  |     /""\       |   __ "\
  (:   \___/  \   \  //   |(. |_)  :) \   \  //   |    /    \      (. |__) :)
   \___  \    /\  \/.    ||:     \/   /\   \/.    |   /' /\  \     |:  ____/
    __/  \   |: \.        |(|  _  \  |: \.        |  //  __'  \    (|  /
   /" \   :) |.  \    /:  ||: |_)  :)|.  \    /:  | /   /  \   \  /|__/ \
  (_______/  |___|\__/|___|(_______/ |___|\__/|___|(___/    \___)(_______)
 -----------------------------------------------------------------------------
 SMBMap - Samba Share Enumerator v1.10.2 | Shawn Evans - ShawnDEvans@gmail.com
                     https://github.com/ShawnDEvans/smbmap

[*] Detected 1 hosts serving SMB
[*] Established 1 SMB connections(s) and 1 authentidated session(s)

[+] IP: 10.4.31.245:445 Name: demo.ine.local            Status: ADMIN!!!   
        Disk                                                    Permissions     Comment
        ----                                                    -----------     -------
        ADMIN$                                                  READ, WRITE     Remote Admin
        C                                                       READ ONLY
        C$                                                      READ, WRITE     Default share
        D$                                                      READ, WRITE     Default share
        Documents                                               READ ONLY
        Downloads                                               READ ONLY
        IPC$                                                    READ ONLY       Remote IPC
        print$                                                  READ, WRITE     Printer Drivers
```

```console
┌──(root㉿INE)-[~]
└─# smbmap -u administrator -p smbserver_771 -L -H demo.ine.local

    ________  ___      ___  _______   ___      ___       __         _______
   /"       )|"  \    /"  ||   _  "\ |"  \    /"  |     /""\       |   __ "\
  (:   \___/  \   \  //   |(. |_)  :) \   \  //   |    /    \      (. |__) :)
   \___  \    /\  \/.    ||:     \/   /\   \/.    |   /' /\  \     |:  ____/
    __/  \   |: \.        |(|  _  \  |: \.        |  //  __'  \    (|  /
   /" \   :) |.  \    /:  ||: |_)  :)|.  \    /:  | /   /  \   \  /|__/ \
  (_______/  |___|\__/|___|(_______/ |___|\__/|___|(___/    \___)(_______)
 -----------------------------------------------------------------------------
 SMBMap - Samba Share Enumerator v1.10.2 | Shawn Evans - ShawnDEvans@gmail.com
                     https://github.com/ShawnDEvans/smbmap

[*] Detected 1 hosts serving SMB
[*] Established 1 SMB connections(s) and 1 authentidated session(s)
[+] Host 10.4.31.245 Local Drives: C:\ D:\
[+] Host 10.4.31.245 Net Drive(s):
[*] No mapped network drives
```

```console
┌──(root㉿INE)-[~]
└─# smbmap -u administrator -p smbserver_771 -H demo.ine.local -r 'C$'

    ________  ___      ___  _______   ___      ___       __         _______
   /"       )|"  \    /"  ||   _  "\ |"  \    /"  |     /""\       |   __ "\
  (:   \___/  \   \  //   |(. |_)  :) \   \  //   |    /    \      (. |__) :)
   \___  \    /\  \/.    ||:     \/   /\   \/.    |   /' /\  \     |:  ____/
    __/  \   |: \.        |(|  _  \  |: \.        |  //  __'  \    (|  /
   /" \   :) |.  \    /:  ||: |_)  :)|.  \    /:  | /   /  \   \  /|__/ \
  (_______/  |___|\__/|___|(_______/ |___|\__/|___|(___/    \___)(_______)
 -----------------------------------------------------------------------------
 SMBMap - Samba Share Enumerator v1.10.2 | Shawn Evans - ShawnDEvans@gmail.com
                     https://github.com/ShawnDEvans/smbmap

[*] Detected 1 hosts serving SMB                                                                                                  
[*] Established 1 SMB connections(s) and 1 authentidated session(s)                                                      

[+] IP: 10.4.31.245:445 Name: demo.ine.local            Status: ADMIN!!!   
        Disk                                                    Permissions     Comment
        ----                                                    -----------     -------
        ADMIN$                                                  READ, WRITE     Remote Admin
        C                                                       READ ONLY
        C$                                                      READ, WRITE     Default share
        ./C$
        dr--r--r--                0 Sat Sep  5 13:26:00 2020    $Recycle.Bin
        fw--w--w--           398356 Wed Aug 12 10:47:41 2020    bootmgr
        fr--r--r--                1 Wed Aug 12 10:47:40 2020    BOOTNXT
        dr--r--r--                0 Wed Aug 12 10:47:41 2020    Documents and Settings
        fr--r--r--               32 Mon Dec 21 21:27:10 2020    flag.txt
        fr--r--r--       8589934592 Fri Aug 23 15:20:27 2024    pagefile.sys
        dr--r--r--                0 Wed Aug 12 10:49:32 2020    PerfLogs
        dw--w--w--                0 Wed Aug 12 10:49:32 2020    Program Files
        dr--r--r--                0 Sat Sep  5 14:35:45 2020    Program Files (x86)
        dr--r--r--                0 Sat Sep  5 14:35:45 2020    ProgramData
        dr--r--r--                0 Sat Sep  5 09:16:57 2020    System Volume Information
        dw--w--w--                0 Sat Dec 19 11:14:55 2020    Users
        dr--r--r--                0 Fri Aug 23 15:31:13 2024    Windows
        D$                                                      READ, WRITE     Default share
        Documents                                               READ ONLY
        Downloads                                               READ ONLY
        IPC$                                                    READ ONLY       Remote IPC
        print$                                                  READ, WRITE     Printer Drivers
```

```console
┌──(root㉿INE)-[~]
└─# smbmap -u administrator -p smbserver_771 -H demo.ine.local --download 'C$\flag.txt'

    ________  ___      ___  _______   ___      ___       __         _______
   /"       )|"  \    /"  ||   _  "\ |"  \    /"  |     /""\       |   __ "\
  (:   \___/  \   \  //   |(. |_)  :) \   \  //   |    /    \      (. |__) :)
   \___  \    /\  \/.    ||:     \/   /\   \/.    |   /' /\  \     |:  ____/
    __/  \   |: \.        |(|  _  \  |: \.        |  //  __'  \    (|  /
   /" \   :) |.  \    /:  ||: |_)  :)|.  \    /:  | /   /  \   \  /|__/ \
  (_______/  |___|\__/|___|(_______/ |___|\__/|___|(___/    \___)(_______)
 -----------------------------------------------------------------------------
 SMBMap - Samba Share Enumerator v1.10.2 | Shawn Evans - ShawnDEvans@gmail.com
                     https://github.com/ShawnDEvans/smbmap

[*] Detected 1 hosts serving SMB
[*] Established 1 SMB connections(s) and 1 authentidated session(s)
[+] Starting download: C$\flag.txt (32 bytes)
[+] File output to: /root/10.4.31.245-C_flag.txt
```

```console
┌──(root㉿INE)-[~]
└─# cat /root/10.4.31.245-C_flag.txt
25f492dbef8453cdca69a173a75790f0
```

---
