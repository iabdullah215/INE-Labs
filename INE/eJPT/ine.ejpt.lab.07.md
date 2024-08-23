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

## SMB Map:

```console

```
