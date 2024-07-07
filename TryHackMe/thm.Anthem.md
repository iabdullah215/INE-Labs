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

![image](Images/TryHackMe/image1.png)

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

