```jsx
Lab Name: Importing Nmap Scan Results Into MSF
Platform: INE
Lab No: 23
Exam: eJPT (Jr. Penetartion Tester)
```

```shell
nmap -sV -Pn -oX my-scan.xml <ip-address>
```
```shell
service postgresql start
```

```console
msfconsole -q
db_status
db_import my-scan.xml
hosts
services
```

> This commands can be used to import a scan into `msfconsole`
