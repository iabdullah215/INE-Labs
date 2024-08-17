```jsx
Lab Name: Scan the Server 1
Platform: INE
Lab No: 02
Exam: eJPT (Jr. Penetartion Tester)
```

## Pinging:

Check if the target machine is reachable.

```console
ping -c 4 demo.ine.local
```

![image](https://github.com/user-attachments/assets/465459d4-3a6e-497b-a0da-196bf3be6f80)

## Scanning:

We can now perform a default Nmap port scan on the target to identify the open ports on the target system, this can be done by running the following command.

```console
nmap demo.ine.local
```

![image](https://github.com/user-attachments/assets/cf625fb8-2f5d-4645-b62e-f7b3ffc68d8a)

```console
nmap demo.ine.local -p-
```

![image](https://github.com/user-attachments/assets/a8f56865-28d2-4e5a-815f-dd5c256d7ee4)

```console
nmap demo.ine.local -p 6421,41288,55413 -sV
```

![image](https://github.com/user-attachments/assets/d9508a81-56fe-458b-bfe4-9a21270e87d4)

---
