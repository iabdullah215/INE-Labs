```jsx
Lab Name: Windows Recon: Nmap Host Discovery
Platform: INE
Lab No: 01
Exam: eJPT (Jr. Penetartion Tester)
```

## Find System's IP-Address:

```console
┌──(root㉿INE)-[~]
└─# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host proto kernel_lo 
       valid_lft forever preferred_lft forever
2: ip_vti0@NONE: <NOARP> mtu 1480 qdisc noop state DOWN group default qlen 1000
    link/ipip 0.0.0.0 brd 0.0.0.0
5060: eth0@if5061: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:0a:01:00:0c brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 10.1.0.12/16 brd 10.1.255.255 scope global eth0
       valid_lft forever preferred_lft forever
5062: eth1@if5063: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:0a:0a:27:05 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 10.10.39.5/24 brd 10.10.39.255 scope global eth1
       valid_lft forever preferred_lft forever
```

So the system's IP-Address is `10.10.39.5` and the subnet is `24`.

## Host Discovery:

```console
┌──(root㉿INE)-[~]
└─# nmap -sn 10.10.39.5/24
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-14 20:18 IST
Nmap scan report for us-east-8 (10.10.39.1)
Host is up (0.000035s latency).
MAC Address: 02:42:BB:7D:79:BB (Unknown)
Nmap scan report for f7seivbb66a579hk2yaclomzb.aws-bridge (10.10.39.2)
Host is up (0.000033s latency).
MAC Address: 02:42:0A:0A:27:02 (Unknown)
Nmap scan report for 6a4qh6hyqbavqixuo0nf57rlr.aws-bridge (10.10.39.3)
Host is up (0.000022s latency).
MAC Address: 02:42:0A:0A:27:03 (Unknown)
Nmap scan report for 9wx1q1purnk66bizffzvt5llq.aws-bridge (10.10.39.4)
Host is up (0.000026s latency).
MAC Address: 02:42:0A:0A:27:04 (Unknown)
Nmap scan report for 71j8f5zmateb5p1kw4q2ywwau.aws-bridge (10.10.39.6)
Host is up (0.000034s latency).
MAC Address: 02:42:0A:0A:27:06 (Unknown)
Nmap scan report for INE (10.10.39.5)
Host is up.
Nmap done: 256 IP addresses (6 hosts up) scanned in 1.98 seconds
```

We can see there are `5` hosts with the status `up`.

> This step wasn't mentioned in the tasks lists but I just wanted to test it.

## Ping:

First ping the target to check whether its active or not.

```console
┌──(root㉿INE)-[~]
└─# ping 10.10.39.3
PING 10.10.39.3 (10.10.39.3) 56(84) bytes of data.
From 10.10.39.1 icmp_seq=1 Destination Port Unreachable
From 10.10.39.1 icmp_seq=2 Destination Port Unreachable
From 10.10.39.1 icmp_seq=3 Destination Port Unreachable
^C
--- 10.10.39.3 ping statistics ---
3 packets transmitted, 0 received, +3 errors, 100% packet loss, time 2082ms
```

## -Pn Flag:

```console
┌──(root㉿INE)-[~]
└─# nmap -Pn 10.10.39.3
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-14 21:54 IST
Nmap scan report for INE (10.10.39.3)
Host is up (0.0000090s latency).
Not shown: 998 closed tcp ports (reset)
PORT      STATE SERVICE
3389/tcp  open  ms-wbt-server
10000/tcp open  snet-sensor-mgmt

Nmap done: 1 IP address (1 host up) scanned in 0.07 seconds
```

## -sV

```console
┌──(root㉿INE)-[~]
└─# nmap -Pn -sV -p 3389 10.10.39.3                                                                                                                                                        
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-14 21:57 IST
Nmap scan report for INE (10.10.39.3)
Host is up (0.000044s latency).

PORT     STATE SERVICE       VERSION
3389/tcp open  ms-wbt-server xrdp

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.26 seconds
```

## -v

```console
┌──(root㉿INE)-[~]
└─# nmap -Pn -sV -p 3389 10.10.39.3 -v                                                                                                                                                     
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-14 21:59 IST
NSE: Loaded 46 scripts for scanning.
Initiating SYN Stealth Scan at 21:59
Scanning INE (10.10.39.3) [1 port]
Discovered open port 3389/tcp on 10.10.39.3
Completed SYN Stealth Scan at 21:59, 0.02s elapsed (1 total ports)
Initiating Service scan at 21:59
Scanning 1 service on INE (10.10.39.3)
Completed Service scan at 22:00, 11.04s elapsed (1 service on 1 host)
NSE: Script scanning 10.10.39.3.
Initiating NSE at 22:00
Completed NSE at 22:00, 0.00s elapsed
Initiating NSE at 22:00
Completed NSE at 22:00, 0.00s elapsed
Nmap scan report for INE (10.10.39.3)
Host is up (0.000056s latency).

PORT     STATE SERVICE       VERSION
3389/tcp open  ms-wbt-server xrdp

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.27 seconds
           Raw packets sent: 1 (44B) | Rcvd: 2 (88B)
```

> For more visit [Nmap](https://nmap.org/)
