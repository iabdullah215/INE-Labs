```jsx
Lab Name: Windows Recon: SMB Discover and Mount
Platform: INE
Lab No: 06
Exam: eJPT (Jr. Penetartion Tester)
```

## Finding the IP Address:

![image](/Images/1.png)

## NMAP Scan:

```console
nmap 10.4.31.0/20 --open
```

![image](/Images/2.png)

## Mounting SMB:

In **My Computer Section** Right Click on Network and select the **Map Network Drive** option. Type target machine IP address in Folder field and hit Browse. We can observe, we have discovered a network share on the machine. Select the target machine IP address and we would expect a network credential prompt. Here, we need to enter target machine credentials which are provided to you i.e `administrator:smbserver_771`

![image](/Images/3.png)

We have successfully mounted the target machine shared folders. Write the following command in the CMD to do the same function.

![image](/Images/4.png)

```console
net use Z: \\<ip-address>\C$ smbserver_771 /user:administrator
```
