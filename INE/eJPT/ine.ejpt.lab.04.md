```jsx
Lab Name: Scan the Server II
Platform: INE
Lab No: 04
Exam: eJPT (Jr. Penetartion Tester)
```

## Pinging:

```console
┌──(root㉿INE)-[~]
└─# ping -c 4 demo.ine.local
PING demo.ine.local (192.252.231.3) 56(84) bytes of data.
64 bytes from demo.ine.local (192.252.231.3): icmp_seq=1 ttl=64 time=0.091 ms
64 bytes from demo.ine.local (192.252.231.3): icmp_seq=2 ttl=64 time=0.057 ms
64 bytes from demo.ine.local (192.252.231.3): icmp_seq=3 ttl=64 time=0.060 ms
64 bytes from demo.ine.local (192.252.231.3): icmp_seq=4 ttl=64 time=0.031 ms

--- demo.ine.local ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3076ms
rtt min/avg/max/mdev = 0.031/0.059/0.091/0.021 ms
```

## Scaning:

To begin with, we can perform an Nmap port scan on the target system to identify whether the BIND DNS server is open. This can be done by running the following command:

```console
┌──(root㉿INE)-[~]
└─# nmap demo.ine.local -p 117 -A
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 20:12 IST
Nmap scan report for demo.ine.local (192.252.231.3)
Host is up (0.000057s latency).

PORT    STATE  SERVICE   VERSION
117/tcp closed uucp-path
MAC Address: 02:42:C0:FC:E7:03 (Unknown)
Too many fingerprints match this host to give specific OS details
Network Distance: 1 hop

TRACEROUTE
HOP RTT     ADDRESS
1   0.06 ms demo.ine.local (192.252.231.3)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 1.81 seconds
```

---

```console
┌──(root㉿INE)-[~]
└─# nmap demo.ine.local -p 100-200 -sU                                                                                                                                                     
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 20:20 IST
Nmap scan report for demo.ine.local (192.252.231.3)
Host is up (0.000083s latency).
Not shown: 99 closed udp ports (port-unreach)
PORT    STATE         SERVICE
134/udp open|filtered ingres-net
177/udp open|filtered xdmcp
MAC Address: 02:42:C0:FC:E7:03 (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 104.16 seconds
```

---

```console
┌──(root㉿INE)-[~]
└─# nmap demo.ine.local -p 134,177 -sUV
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 20:39 IST
Nmap scan report for demo.ine.local (192.252.231.3)
Host is up (0.000052s latency).

PORT    STATE         SERVICE    VERSION
134/udp open|filtered ingres-net
177/udp open          domain     ISC BIND 9.10.3-P4 (Ubuntu Linux)
MAC Address: 02:42:C0:FC:E7:03 (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 100.10 seconds
```

---

```console
┌──(root㉿INE)-[~]
└─# nmap demo.ine.local -p 134 -sUV --script=discovery                                                                                                                                                                               
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-17 20:42 IST
Pre-scan script results:
| knx-gateway-discover: 
|_ ERROR: Couldn't get interface for 224.0.23.12
| broadcast-igmp-discovery: 
|   10.1.0.1
|     Interface: eth0
|     Version: 2
|     Group: 224.0.0.106
|     Description: All-Snoopers (rfc4286)
|   192.252.231.1
|     Interface: eth1
|     Version: 2
|     Group: 224.0.0.106
|     Description: All-Snoopers (rfc4286)
|_  Use the newtargets script-arg to add the results as targets
|_http-robtex-shared-ns: *TEMPORARILY DISABLED* due to changes in Robtex's API. See https://www.robtex.com/api/
|_hostmap-robtex: *TEMPORARILY DISABLED* due to changes in Robtex's API. See https://www.robtex.com/api/
| targets-asn: 
|_  targets-asn.asn is a mandatory parameter
Nmap scan report for demo.ine.local (192.252.231.3)
Host is up (0.000032s latency).

PORT    STATE         SERVICE    VERSION
134/udp open|filtered ingres-net
MAC Address: 02:42:C0:FC:E7:03 (Unknown)

Host script results:
|_asn-query: No Answers
|_sniffer-detect: Likely in promiscuous mode (tests: "11111111")
| dns-brute: 
|   DNS Brute-force hostnames: 
|_    demo.ine.local - 192.252.231.3
|_fcrdns: PASS (kv6peft1w77ktby0jt77emswt.temp-network_a-252-231)
Bug in ip-geolocation-geoplugin: no string output.
| resolveall: 
|   Host 'demo.ine.local' also resolves to:
|   Use the 'newtargets' script-arg to add the results as targets
|_  Use the --resolve-all option to scan all resolved addresses without using this script.

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 123.73 seconds
```

---

As shown in below, the authentication with the TFTP server is successful and we are provided with an FTP console.

```console
┌──(root㉿INE)-[~]
└─# tftp demo.ine.local 134            
tftp>
```

We have successfully been able to identify the ports running the BIND DNS server, SNMP server and TFTP server.
