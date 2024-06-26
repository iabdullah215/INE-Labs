```jsx
Lab Name: Provision a Compute Instance - AWS
Platform: INE
Lab No: 07
Exam: ICCA (INE Certified Cloud Associate)
```

## Provision an AWS EC2 instance

- Use your credentials and login to the AWS account.
- Start searching for the EC2 in the search box.
- Select `EC2 instance`.
- Click on _Instances_ and click on `Launch instances`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/1f04e544-824d-4efc-bb02-74e91e843d6e)

- Name: `lab-vm`
- Scroll down to _Application and OS Images_, Choose Amazon Linux as shown in image.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/308b66da-5494-4755-966d-a234eff98451)

- Instance type to be `t2.micro`.
- Click on `Create new key pair`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/299a3521-1f71-4cd5-90f5-f9344ce45654)

- A window will be popped up, now create a key pair with name `lab-vm-key-pair`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/3c38da5e-5449-4d5f-a4eb-c356a18355e9)

- Go to _Network Settings_ and click on `Edit` to add `Security group`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/72b58e9e-8913-44d3-9d6a-1d15f42ba442)

- Click on `Add security group rule`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/ec44036f-1cf1-4aad-a52c-c1bd6a6c70ac)

- Type: `HTTP` and Source Type: `Anywhere`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/4e7455b6-322d-44de-8248-1a072c2974da)

- Go to summary and click on `Launch instance`.
- Once, it is success then click on `View all instances`.
- Check for the `Instance State` Status, refresh the page to update the status. Click on the `Instance ID` to open it.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/a7006230-fed3-4a0b-bcd0-2615eb0e07ad)

- Click on `Connect`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/293a4720-3cc8-49aa-aa6c-588c9b03f053)

- Click on the tab `EC2 instance Connect` and press the button `Connect`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/4c203172-cdba-4e28-9a2b-e2e71606cc47)

- A new tab will be opened on the browser. So, run the below command in the terminal.

`sudo amazon-linux-extras install nginx1`

- Press: `y` to continue.

```console
   ,     #_
   ~\_  ####_        Amazon Linux 2
  ~~  \_#####\
  ~~     \###|       AL2 End of Life is 2025-06-30.
  ~~       \#/ ___
   ~~       V~' '->
    ~~~         /    A newer version of Amazon Linux is available!
      ~~._.   _/
         _/ _/       Amazon Linux 2023, GA and supported until 2028-03-15.
       _/m/'           https://aws.amazon.com/linux/amazon-linux-2023/

[ec2-user@ip-172-31-30-104 ~]$ sudo amazon-linux-extras install nginx1
Installing nginx
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
Cleaning repos: amzn2-core amzn2extra-docker amzn2extra-kernel-5.10 amzn2extra-nginx1
17 metadata files removed
6 sqlite files removed
0 metadata files removed
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
amzn2-core                                                                      | 3.6 kB  00:00:00     
amzn2extra-docker                                                               | 2.9 kB  00:00:00     
amzn2extra-kernel-5.10                                                          | 3.0 kB  00:00:00     
amzn2extra-nginx1                                                               | 2.9 kB  00:00:00     
(1/9): amzn2-core/2/x86_64/group_gz                                             | 2.7 kB  00:00:00     
(2/9): amzn2-core/2/x86_64/updateinfo                                           | 940 kB  00:00:00     
(3/9): amzn2extra-docker/2/x86_64/updateinfo                                    |  16 kB  00:00:00     
(4/9): amzn2extra-docker/2/x86_64/primary_db                                    | 102 kB  00:00:00     
(5/9): amzn2extra-kernel-5.10/2/x86_64/updateinfo                               |  69 kB  00:00:00     
(6/9): amzn2extra-nginx1/2/x86_64/updateinfo                                    | 3.0 kB  00:00:00     
(7/9): amzn2extra-nginx1/2/x86_64/primary_db                                    |  55 kB  00:00:00     
(8/9): amzn2extra-kernel-5.10/2/x86_64/primary_db                               |  27 MB  00:00:00     
(9/9): amzn2-core/2/x86_64/primary_db                                           |  69 MB  00:00:00     
Resolving Dependencies
--> Running transaction check
---> Package nginx.x86_64 1:1.22.1-1.amzn2.0.3 will be installed
--> Processing Dependency: nginx-core = 1:1.22.1-1.amzn2.0.3 for package: 1:nginx-1.22.1-1.amzn2.0.3.x86_64
--> Processing Dependency: nginx-filesystem = 1:1.22.1-1.amzn2.0.3 for package: 1:nginx-1.22.1-1.amzn2.0.3.x86_64
--> Running transaction check
---> Package nginx-core.x86_64 1:1.22.1-1.amzn2.0.3 will be installed
--> Processing Dependency: libcrypto.so.1.1(OPENSSL_1_1_0)(64bit) for package: 1:nginx-core-1.22.1-1.amzn2.0.3.x86_64
--> Processing Dependency: libssl.so.1.1(OPENSSL_1_1_0)(64bit) for package: 1:nginx-core-1.22.1-1.amzn2.0.3.x86_64
--> Processing Dependency: libssl.so.1.1(OPENSSL_1_1_1)(64bit) for package: 1:nginx-core-1.22.1-1.amzn2.0.3.x86_64
--> Processing Dependency: libcrypto.so.1.1()(64bit) for package: 1:nginx-core-1.22.1-1.amzn2.0.3.x86_64
--> Processing Dependency: libprofiler.so.0()(64bit) for package: 1:nginx-core-1.22.1-1.amzn2.0.3.x86_64
--> Processing Dependency: libssl.so.1.1()(64bit) for package: 1:nginx-core-1.22.1-1.amzn2.0.3.x86_64
---> Package nginx-filesystem.noarch 1:1.22.1-1.amzn2.0.3 will be installed
--> Running transaction check
---> Package gperftools-libs.x86_64 0:2.6.1-1.amzn2 will be installed
---> Package openssl11-libs.x86_64 1:1.1.1g-12.amzn2.0.21 will be installed
--> Processing Dependency: openssl11-pkcs11 for package: 1:openssl11-libs-1.1.1g-12.amzn2.0.21.x86_64
--> Running transaction check
---> Package openssl11-pkcs11.x86_64 0:0.4.10-6.amzn2.0.1 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=======================================================================================================
 Package                 Arch          Version                          Repository                Size
=======================================================================================================
Installing:
 nginx                   x86_64        1:1.22.1-1.amzn2.0.3             amzn2extra-nginx1         55 k
Installing for dependencies:
 gperftools-libs         x86_64        2.6.1-1.amzn2                    amzn2-core               274 k
 nginx-core              x86_64        1:1.22.1-1.amzn2.0.3             amzn2extra-nginx1        559 k
 nginx-filesystem        noarch        1:1.22.1-1.amzn2.0.3             amzn2extra-nginx1         25 k
 openssl11-libs          x86_64        1:1.1.1g-12.amzn2.0.21           amzn2-core               1.4 M
 openssl11-pkcs11        x86_64        0.4.10-6.amzn2.0.1               amzn2-core                61 k

Transaction Summary
=======================================================================================================
Install  1 Package (+5 Dependent packages)

Total download size: 2.4 M
Installed size: 6.7 M
Is this ok [y/d/N]: y
Downloading packages:
(1/6): gperftools-libs-2.6.1-1.amzn2.x86_64.rpm                                 | 274 kB  00:00:00     
(2/6): nginx-1.22.1-1.amzn2.0.3.x86_64.rpm                                      |  55 kB  00:00:00     
(3/6): nginx-core-1.22.1-1.amzn2.0.3.x86_64.rpm                                 | 559 kB  00:00:00     
(4/6): nginx-filesystem-1.22.1-1.amzn2.0.3.noarch.rpm                           |  25 kB  00:00:00     
(5/6): openssl11-pkcs11-0.4.10-6.amzn2.0.1.x86_64.rpm                           |  61 kB  00:00:00     
(6/6): openssl11-libs-1.1.1g-12.amzn2.0.21.x86_64.rpm                           | 1.4 MB  00:00:00     
-------------------------------------------------------------------------------------------------------
Total                                                                  6.7 MB/s | 2.4 MB  00:00:00     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : 1:nginx-filesystem-1.22.1-1.amzn2.0.3.noarch                                        1/6 
  Installing : 1:openssl11-libs-1.1.1g-12.amzn2.0.21.x86_64                                        2/6 
  Installing : openssl11-pkcs11-0.4.10-6.amzn2.0.1.x86_64                                          3/6 
  Installing : gperftools-libs-2.6.1-1.amzn2.x86_64                                                4/6 
  Installing : 1:nginx-core-1.22.1-1.amzn2.0.3.x86_64                                              5/6 
  Installing : 1:nginx-1.22.1-1.amzn2.0.3.x86_64                                                   6/6 
  Verifying  : 1:nginx-1.22.1-1.amzn2.0.3.x86_64                                                   1/6 
  Verifying  : gperftools-libs-2.6.1-1.amzn2.x86_64                                                2/6 
  Verifying  : openssl11-pkcs11-0.4.10-6.amzn2.0.1.x86_64                                          3/6 
  Verifying  : 1:nginx-filesystem-1.22.1-1.amzn2.0.3.noarch                                        4/6 
  Verifying  : 1:nginx-core-1.22.1-1.amzn2.0.3.x86_64                                              5/6 
  Verifying  : 1:openssl11-libs-1.1.1g-12.amzn2.0.21.x86_64                                        6/6 

Installed:
  nginx.x86_64 1:1.22.1-1.amzn2.0.3                                                                    

Dependency Installed:
  gperftools-libs.x86_64 0:2.6.1-1.amzn2             nginx-core.x86_64 1:1.22.1-1.amzn2.0.3            
  nginx-filesystem.noarch 1:1.22.1-1.amzn2.0.3       openssl11-libs.x86_64 1:1.1.1g-12.amzn2.0.21      
  openssl11-pkcs11.x86_64 0:0.4.10-6.amzn2.0.1      

Complete!
  2  httpd_modules            available    [ =1.0  =stable ]
  3  memcached1.5             available    \
        [ =1.5.1  =1.5.16  =1.5.17 ]
  9  R3.4                     available    [ =3.4.3  =stable ]
 10  rust1                    available    \
        [ =1.22.1  =1.26.0  =1.26.1  =1.27.2  =1.31.0  =1.38.0
          =stable ]
 18  libreoffice              available    \
        [ =5.0.6.2_15  =5.3.6.1  =stable ]
 19  gimp                     available    [ =2.8.22 ]
 20 †docker=latest            enabled      \
        [ =17.12.1  =18.03.1  =18.06.1  =18.09.9  =stable ]
 21  mate-desktop1.x          available    \
        [ =1.19.0  =1.20.0  =stable ]
 22  GraphicsMagick1.3        available    \
        [ =1.3.29  =1.3.32  =1.3.34  =stable ]
 24  epel                     available    [ =7.11  =stable ]
 25  testing                  available    [ =1.0  =stable ]
 26  ecs                      available    [ =stable ]
 27 †corretto8                available    \
        [ =1.8.0_192  =1.8.0_202  =1.8.0_212  =1.8.0_222  =1.8.0_232
          =1.8.0_242  =stable ]
 32  lustre2.10               available    \
        [ =2.10.5  =2.10.8  =stable ]
 33 †java-openjdk11           available    [ =11  =stable ]
 34  lynis                    available    [ =stable ]
 36  BCC                      available    [ =0.x  =stable ]
 37  mono                     available    [ =5.x  =stable ]
 38  nginx1=latest            enabled      [ =stable ]
 40  mock                     available    [ =stable ]
 43  livepatch                available    [ =stable ]
 44 †python3.8                available    [ =stable ]
 45  haproxy2                 available    [ =stable ]
 46  collectd                 available    [ =stable ]
 47  aws-nitro-enclaves-cli   available    [ =stable ]
 48  R4                       available    [ =stable ]
  _  kernel-5.4               available    [ =stable ]
 50  selinux-ng               available    [ =stable ]
 52  tomcat9                  available    [ =stable ]
 53  unbound1.13              available    [ =stable ]
 54 †mariadb10.5              available    [ =stable ]
 55  kernel-5.10=latest       enabled      [ =stable ]
 56  redis6                   available    [ =stable ]
 58 †postgresql12             available    [ =stable ]
 59 †postgresql13             available    [ =stable ]
 60  mock2                    available    [ =stable ]
 61  dnsmasq2.85              available    [ =stable ]
 62  kernel-5.15              available    [ =stable ]
 63 †postgresql14             available    [ =stable ]
 64  firefox                  available    [ =stable ]
 65  lustre                   available    [ =stable ]
 66 †php8.1                   available    [ =stable ]
 67  awscli1                  available    [ =stable ]
 68 †php8.2                   available    [ =stable ]
 69  dnsmasq                  available    [ =stable ]
 70  unbound1.17              available    [ =stable ]
 72  collectd-python3         available    [ =stable ]
† Note on end-of-support. Use 'info' subcommand.
```


- Now start `nginx` by running `sudo systemctl start nginx`.

- Now verify it by running `curl localhost`.

```console
[ec2-user@ip-172-31-30-104 ~]$ curl localhost
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>       
```

- Now, logout from terminal by using `exit`

- Come back to the summary page and copy the External `Public IPv4 address`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/ef4cbc05-e420-4124-8404-dfc3c8aad4a0)

- Open a new browser tab and navigate to the IP address - Verify that a welcome page is returned.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/dc4ac607-430c-44f3-a07e-1e9eb9198cfd)

- Terminate the insance.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/958bb803-e72d-4774-8916-f70e716df6ae)


_**Successfully we have completed our Task.**_

---
