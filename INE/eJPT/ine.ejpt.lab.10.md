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

Service detection pe
