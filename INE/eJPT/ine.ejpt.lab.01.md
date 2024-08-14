```jsx
Lab Name: Windows Recon: Nmap Host Discovery
Platform: INE
Lab No: 01
Exam: eJPT (Jr. Penetartion Tester)
```

## Find System's IP-Address:

```shell
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

So the system's IP-Address is `10.1.0.12` and the subnet is `16`.

