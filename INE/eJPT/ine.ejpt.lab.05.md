```jsx
Lab Name: Scan the Server III
Platform: INE
Lab No: 05
Exam: eJPT (Jr. Penetartion Tester)
```

## Pinging:

```console
┌──(root㉿INE)-[~]
└─# ping -c 4 demo.ine.local
PING demo.ine.local (192.79.3.3) 56(84) bytes of data.
64 bytes from demo.ine.local (192.79.3.3): icmp_seq=1 ttl=64 time=0.100 ms
64 bytes from demo.ine.local (192.79.3.3): icmp_seq=2 ttl=64 time=0.060 ms
64 bytes from demo.ine.local (192.79.3.3): icmp_seq=3 ttl=64 time=0.055 ms
64 bytes from demo.ine.local (192.79.3.3): icmp_seq=4 ttl=64 time=0.062 ms

--- demo.ine.local ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3074ms
rtt min/avg/max/mdev = 0.055/0.069/0.100/0.017 ms
```

## Scanning:

```console
┌──(root㉿INE)-[~]
└─# nmap demo.ine.local -T4 -p-
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-18 00:08 IST
Nmap scan report for demo.ine.local (192.79.3.3)
Host is up (0.000022s latency).
All 65535 scanned ports on demo.ine.local (192.79.3.3) are in ignored states.
Not shown: 65535 closed tcp ports (reset)
MAC Address: 02:42:C0:4F:03:03 (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 2.26 seconds
```

---

```console
nmap demo.ine.local -T4 -sU
```

![image](https://github.com/user-attachments/assets/07f38343-a597-43c1-acdf-245a230b5bc1)

```console
nmap demo.ine.local -T4 -sU -p 161 -A
```

![image](https://github.com/user-attachments/assets/3daa26c9-e359-4ed7-815d-5006bd4cbae6)

![image](https://github.com/user-attachments/assets/9681878e-b96d-4f3a-9a46-4a1de3808a62)

---
