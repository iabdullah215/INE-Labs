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

```console
┌──(root㉿INE)-[~]
└─# nmap --script ssh2-enum-algos demo.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-23 18:18 IST
Nmap scan report for demo.ine.local (192.254.69.3)
Host is up (0.000023s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
| ssh2-enum-algos: 
|   kex_algorithms: (6)
|       curve25519-sha256@libssh.org
|       ecdh-sha2-nistp256
|       ecdh-sha2-nistp384
|       ecdh-sha2-nistp521
|       diffie-hellman-group-exchange-sha256
|       diffie-hellman-group14-sha1
|   server_host_key_algorithms: (5)
|       ssh-rsa
|       rsa-sha2-512
|       rsa-sha2-256
|       ecdsa-sha2-nistp256
|       ssh-ed25519
|   encryption_algorithms: (6)
|       chacha20-poly1305@openssh.com
|       aes128-ctr
|       aes192-ctr
|       aes256-ctr
|       aes128-gcm@openssh.com
|       aes256-gcm@openssh.com
|   mac_algorithms: (10)
|       umac-64-etm@openssh.com
|       umac-128-etm@openssh.com
|       hmac-sha2-256-etm@openssh.com
|       hmac-sha2-512-etm@openssh.com
|       hmac-sha1-etm@openssh.com
|       umac-64@openssh.com
|       umac-128@openssh.com
|       hmac-sha2-256
|       hmac-sha2-512
|       hmac-sha1
|   compression_algorithms: (2)
|       none
|_      zlib@openssh.com
MAC Address: 02:42:C0:FE:45:03 (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 0.22 seconds
```

```console
┌──(root㉿INE)-[~]
└─# nmap --script ssh-hostkey --script-args ssh hostkey=full demo.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-23 18:20 IST
Failed to resolve "hostkey=full".
Nmap scan report for demo.ine.local (192.254.69.3)
Host is up (0.000023s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
| ssh-hostkey: 
|   2048 b0:2b:8d:3e:4c:de:f9:ab:7f:86:47:fd:c8:d2:e0:a8 (RSA)
|   256 75:6f:7d:4e:d7:f7:6d:ec:23:d1:8e:39:76:94:86:8a (ECDSA)
|_  256 58:16:43:a6:65:2c:0b:0a:22:60:86:31:6f:59:38:12 (ED25519)
MAC Address: 02:42:C0:FE:45:03 (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 0.27 seconds
```

```console
┌──(root㉿INE)-[~]
└─# nmap -p 22 --script ssh-auth-methods --script-args="ssh.user=admin" demo.ine.local         
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-23 18:24 IST
Nmap scan report for demo.ine.local (192.254.69.3)
Host is up (0.000062s latency).

PORT   STATE SERVICE
22/tcp open  ssh
| ssh-auth-methods: 
|   Supported authentication methods: 
|     publickey
|_    password
MAC Address: 02:42:C0:FE:45:03 (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 2.38 seconds
```

```console
┌──(root㉿INE)-[~]
└─# nmap -p 22 --script ssh-auth-methods --script-args="ssh.user=student" demo.ine.localStarting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-23 18:23 IST
Nmap scan report for demo.ine.local (192.254.69.3)
Host is up (0.000053s latency).

PORT   STATE SERVICE
22/tcp open  ssh
| ssh-auth-methods: 
|_  Supported authentication methods: none_auth
MAC Address: 02:42:C0:FE:45:03 (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 0.17 seconds
```

## Exploitation:

```console
┌──(root㉿INE)-[~]
└─# ssh student@demo.ine.local
The authenticity of host 'demo.ine.local (192.254.69.3)' can't be established.
ED25519 key fingerprint is SHA256:usoU91o26EhXVfBuwZIwlQtdpEw/EHXRp7NejBKASWA.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'demo.ine.local' (ED25519) to the list of known hosts.
Welcome to attack defense ssh recon lab!!
Welcome to Ubuntu 16.04.5 LTS (GNU/Linux 6.8.0-40-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

student@demo:~$ ls
FLAG
student@demo:~$ cat FLAG 
`
```
