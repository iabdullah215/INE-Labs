```jsx
Machine Name: Anthem
Platform: TryHackMe
Difficulty: Easy
```

> _Note: The walkthrough gives a highlevel overview of how the box was solved_

## Walthrough

Machine can be found [here](https://tryhackme.com/r/room/anthem)

## Recon

We'll start the things up with a simple nmap scan.

```console
┌──(MnM㉿kali)-[~/Desktop/THM/Anthem]
└─$ sudo nmap -sV -Pn 10.10.28.4
Starting Nmap 7.94 ( https://nmap.org ) at 2024-07-07 06:05 EDT
Nmap scan report for 10.10.28.4
Host is up (0.21s latency).
Not shown: 998 filtered tcp ports (no-response)
PORT     STATE SERVICE       VERSION
80/tcp   open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
3389/tcp open  ms-wbt-server Microsoft Terminal Services
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 65.90 seconds
```

Let's access the web server.

![image](TryHackMe/images/image1.png)

Let's see the `robots.txt`. To access it type `http://<ip>/robots.txt` in the url section of your browser.

```console
UmbracoIsTheBest!

# Use for all search robots
User-agent: *

# Define the directories not to crawl
Disallow: /bin/
Disallow: /config/
Disallow: /umbraco/
Disallow: /umbraco_client/
```

**Finding the flags**

Flag 4 and 2 were in the sourse code of the `/archive/a-cheers-to-our-it-department/`. Type this in your URL Section to find the flag. `view-source:http://<ip>/archive/a-cheers-to-our-it-department/`

![image](images/TryHackMe/image3.png)

![image](images/TryHackMe/image4.png)

**Flag**: `THM{AN0TH3R_M3TA}`

**Flag**: `THM{G!T_G00D}`

Flag 3 was on the `/authors/jane-doe/` subdomain. Found it in the very start of the challenge while examining the web.

![image](images/TryHackMe/image2.png)

**Flag:** `THM{L0L_WH0_D15}`

Flag 1 was in the sourse code `/archive/we-are-hiring/` subdomain and can be seen by typing `view-source:http://<IP>/archive/we-are-hiring/` in the URL Section.

**Flag:** `THM{L0L_WH0_US3S_M3T4}`

## User Flag:

In order to get the user and the root flag we have to access the machine using the `RDP`. In order to do so use `rdesktop -u <user-name> -p <password> <IP>` command.

```console
┌──(MnM㉿kali)-[~/Desktop/THM/Anthem]
└─$ rdesktop -u SG -p UmbracoIsTheBest! 10.10.28.4
Autoselecting keyboard map 'en-us' from locale

ATTENTION! The server uses and invalid security certificate which can not be trusted for
the following identified reasons(s);

 1. Certificate issuer is not trusted by this system.

     Issuer: CN=WIN-LU09299160F


Review the following certificate info before you trust it to be added as an exception.
If you do not trust the certificate the connection atempt will be aborted:

    Subject: CN=WIN-LU09299160F
     Issuer: CN=WIN-LU09299160F
 Valid From: Sat Jul  6 06:04:29 2024
         To: Sun Jan  5 05:04:29 2025

  Certificate fingerprints:

       sha1: b4676fb261277eb8b90bfbe29190623d5c66c10d
     sha256: a73859404aed5d6fa548bbcca0fd54680a5ae201cf7b9693b38c3e7fa216cdc8


Do you trust this certificate (yes/no)? yes
Failed to initialize NLA, do you have correct Kerberos TGT initialized ?
Core(warning): Certificate received from server is NOT trusted by this system, an exception has been added by the user to trust this specific certificate.
Connection established using SSL.
```

You'll find a `user.txt` file on the desktop with the user flag in it.

**Flag:** `THM{N00T_NO0T}`

## Root Flag:

First we have to locate the root flag in order to privilage escalate. So in order to do so use the following command
