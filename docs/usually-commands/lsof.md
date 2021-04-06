## 命令简介

lsof 命令用于显示 Linux 系统当前已打开的所有文件列表。查看进程或系统打开的文件会给调试带来极大的帮助。下面简单地介绍[ lsof ](http://mp.weixin.qq.com/s?__biz=MzI0MDQ4MTM5NQ==&mid=2247503220&idx=1&sn=b047892743c92372ccd74a9b9201b0f4&chksm=e918a868de6f217eca0615408ee9ad3299d3f94b711eeb3ed8a8d9578f08f62f5c7ba64dea6d&scene=21#wechat_redirect)常使用的功能。

lsof （list open files）命令用于查看你进程打开的文件，打开文件的进程，进程打开的端口(TCP、UDP),还可以用于找回/恢复被删除的文件。lsof 命令需要访问核心内存和各种文件，所以需要具备 root 超级管理员权限的用户才能执行此命令。

## 语法格式

```
lsof [Options] 
```

## 选项说明

```
-a         #显示打开文件的进程
-c<进程名>  #显示指定进程所打开的文件
-g         #显示GID号进程详情
-d<文件号>  #显示占用该文件号的进程
+d<目录>   #显示目录下被打开的文件
+D<目录>   #递归列出目录下被打开的文件
-n<目录>   #显示使用NFS的文件
-l        #在输出显示用户ID而不是用户名
-i<条件>   #输出符合条件的进程
-p<进程号> #输出指定进程号所打开的文件
-u   #显示指定UID号进程详情
-h   #显示帮助信息
-t   #仅获取进程ID
-U   #获取UNIX套接口地址
-F   #格式化输出结果
-v   #显示版本信息
```

## 应用举例

显示所有连接

```
[root@CentOS7-1 ~]# lsof -i
COMMAND   PID    USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
chronyd   629  chrony    5u  IPv4  16952      0t0  UDP localhost:323 
chronyd   629  chrony    6u  IPv6  16953      0t0  UDP localhost:323 
sshd      866    root    3u  IPv4  19638      0t0  TCP *:ssh (LISTEN)
sshd      866    root    4u  IPv6  19647      0t0  TCP *:ssh (LISTEN)
master    976    root   13u  IPv4  20415      0t0  TCP localhost:smtp (LISTEN)
master    976    root   14u  IPv6  20416      0t0  TCP localhost:smtp (LISTEN)
netdata 18325 netdata    4u  IPv4 114083      0t0  TCP *:dnp-sec (LISTEN)
netdata 18325 netdata    5u  IPv6 114084      0t0  TCP *:dnp-sec (LISTEN)
netdata 18325 netdata   36u  IPv6 114297      0t0  UDP localhost:8125 
netdata 18325 netdata   37u  IPv4 114298      0t0  UDP localhost:8125 
netdata 18325 netdata   38u  IPv6 114302      0t0  TCP localhost:8125 (LISTEN)
netdata 18325 netdata   39u  IPv4 114303      0t0  TCP localhost:8125 (LISTEN)
sshd    18968    root    3u  IPv4 118704      0t0  TCP CentOS7-1:ssh->192.168.1.93:62148 (ESTABLISHED)
```

只显示IPV6的连接信息

```
[root@CentOS7-1 ~]# lsof -i 6
COMMAND   PID    USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
chronyd   629  chrony    6u  IPv6  16953      0t0  UDP localhost:323 
sshd      866    root    4u  IPv6  19647      0t0  TCP *:ssh (LISTEN)
master    976    root   14u  IPv6  20416      0t0  TCP localhost:smtp (LISTEN)
netdata 18325 netdata    5u  IPv6 114084      0t0  TCP *:dnp-sec (LISTEN)
netdata 18325 netdata   36u  IPv6 114297      0t0  UDP localhost:8125 
netdata 18325 netdata   38u  IPv6 114302      0t0  TCP localhost:8125 (LISTEN)
```

只显示IPV4的连接信息

```
[root@CentOS7-1 ~]# lsof -i 4
COMMAND   PID    USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
chronyd   629  chrony    5u  IPv4  16952      0t0  UDP localhost:323 
sshd      866    root    3u  IPv4  19638      0t0  TCP *:ssh (LISTEN)
master    976    root   13u  IPv4  20415      0t0  TCP localhost:smtp (LISTEN)
netdata 18325 netdata    4u  IPv4 114083      0t0  TCP *:dnp-sec (LISTEN)
netdata 18325 netdata   37u  IPv4 114298      0t0  UDP localhost:8125 
netdata 18325 netdata   39u  IPv4 114303      0t0  TCP localhost:8125 (LISTEN)
sshd    18968    root    3u  IPv4 118704      0t0  TCP CentOS7-1:ssh->192.168.1.93:62148 (ESTABLISHED)
```

仅显示TCP连接

```
[root@CentOS7-1 ~]# lsof -i tcp
COMMAND   PID    USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
sshd      866    root    3u  IPv4  19638      0t0  TCP *:ssh (LISTEN)
sshd      866    root    4u  IPv6  19647      0t0  TCP *:ssh (LISTEN)
master    976    root   13u  IPv4  20415      0t0  TCP localhost:smtp (LISTEN)
master    976    root   14u  IPv6  20416      0t0  TCP localhost:smtp (LISTEN)
netdata 18325 netdata    4u  IPv4 114083      0t0  TCP *:dnp-sec (LISTEN)
netdata 18325 netdata    5u  IPv6 114084      0t0  TCP *:dnp-sec (LISTEN)
netdata 18325 netdata   38u  IPv6 114302      0t0  TCP localhost:8125 (LISTEN)
netdata 18325 netdata   39u  IPv4 114303      0t0  TCP localhost:8125 (LISTEN)
sshd    18968    root    3u  IPv4 118704      0t0  TCP CentOS7-1:ssh->192.168.1.93:62148 (ESTABLISHED)
```

仅显示UDP连接

```
[root@CentOS7-1 ~]# lsof -i udp
COMMAND   PID    USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
chronyd   629  chrony    5u  IPv4  16952      0t0  UDP localhost:323 
chronyd   629  chrony    6u  IPv6  16953      0t0  UDP localhost:323 
netdata 18325 netdata   36u  IPv6 114297      0t0  UDP localhost:8125 
netdata 18325 netdata   37u  IPv4 114298      0t0  UDP localhost:8125 
```

显示指定端口的连接信息

```
[root@CentOS7-1 ~]# lsof -i :22
COMMAND   PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
sshd      866 root    3u  IPv4  19638      0t0  TCP *:ssh (LISTEN)
sshd      866 root    4u  IPv6  19647      0t0  TCP *:ssh (LISTEN)
sshd    18968 root    3u  IPv4 118704      0t0  TCP CentOS7-1:ssh->192.168.1.93:62148 (ESTABLISHED)
[root@CentOS7-1 ~]# lsof -i :80
[root@CentOS7-1 ~]# lsof -i :62148
COMMAND   PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
sshd    18968 root    3u  IPv4 118704      0t0  TCP CentOS7-1:ssh->192.168.1.93:62148 (ESTABLISHED)
```

列由某个用户打开的进程或文件

```
[root@CentOS7-1 ~]# lsof -u root | head -5
COMMAND     PID USER   FD      TYPE             DEVICE  SIZE/OFF       NODE NAME
systemd       1 root  cwd       DIR              253,0       262         64 /
systemd       1 root  rtd       DIR              253,0       262         64 /
systemd       1 root  txt       REG              253,0   1628608   16959493 /usr/lib/systemd/systemd
systemd       1 root  mem       REG              253,0     20064    1679454 /usr/lib64/libuuid.so.1.3.0

#列出除了root以外用户打开的文件
[root@CentOS7-1 ~]# lsof -u ^root | head
COMMAND     PID   TID    USER   FD      TYPE             DEVICE SIZE/OFF       NODE NAME
polkitd     618       polkitd  cwd       DIR              253,0      262         64 /
polkitd     618       polkitd  rtd       DIR              253,0      262         64 /
polkitd     618       polkitd  txt       REG              253,0   120432   17108633 /usr/lib/polkit-1/polkitd
polkitd     618       polkitd  mem       REG              253,0    61560      18290 /usr/lib64/libnss_files-2.17.so
polkitd     618       polkitd  mem       REG              253,0    68192      40949 /usr/lib64/libbz2.so.1.0.6
polkitd     618       polkitd  mem       REG              253,0    99952     324334 /usr/lib64/libelf-0.176.so
polkitd     618       polkitd  mem       REG              253,0    19896      46144 /usr/lib64/libattr.so.1.1.0
polkitd     618       polkitd  mem       REG              253,0    20064    1679454 /usr/lib64/libuuid.so.1.3.0
polkitd     618       polkitd  mem       REG              253,0   265576      20649 /usr/lib64/libblkid.so.1.1.0
```

显示指定的连接信息

```
#显示指定到指定主机的连接
[root@CentOS7-1 ~]# lsof -i@192.168.1.100
COMMAND   PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
sshd    18968 root    3u  IPv4 118704      0t0  TCP CentOS7-1:ssh->192.168.1.93:62148 (ESTABLISHED)

#显示指定到指定主机端口的连接
[root@CentOS7-1 ~]# lsof -i@192.168.1.100:22
COMMAND   PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
sshd    18968 root    3u  IPv4 118704      0t0  TCP CentOS7-1:ssh->192.168.1.93:62148 (ESTABLISHED)
```

显示某些状态的端口信息

```
#找出处于监听状态的端口
[root@CentOS7-1 ~]# lsof -i -sTCP:LISTEN
COMMAND   PID    USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
sshd      866    root    3u  IPv4  19638      0t0  TCP *:ssh (LISTEN)
sshd      866    root    4u  IPv6  19647      0t0  TCP *:ssh (LISTEN)
master    976    root   13u  IPv4  20415      0t0  TCP localhost:smtp (LISTEN)
master    976    root   14u  IPv6  20416      0t0  TCP localhost:smtp (LISTEN)
netdata 18325 netdata    4u  IPv4 114083      0t0  TCP *:dnp-sec (LISTEN)
netdata 18325 netdata    5u  IPv6 114084      0t0  TCP *:dnp-sec (LISTEN)
netdata 18325 netdata   38u  IPv6 114302      0t0  TCP localhost:8125 (LISTEN)
netdata 18325 netdata   39u  IPv4 114303      0t0  TCP localhost:8125 (LISTEN)

##找出处于已连接状态的端口
[root@CentOS7-1 ~]# lsof -i -sTCP:ESTABLISHED
COMMAND   PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
sshd    18968 root    3u  IPv4 118704      0t0  TCP CentOS7-1:ssh->192.168.1.93:62148 (ESTABLISHED)
```

终止用户行为

```
[root@CentOS7-1 ~]# lsof -u mingongge
COMMAND   PID      USER   FD   TYPE DEVICE  SIZE/OFF     NODE NAME
bash    20369 mingongge  cwd    DIR  253,0        82   462615 /home/mingongge
bash    20369 mingongge  rtd    DIR  253,0       262       64 /
bash    20369 mingongge  txt    REG  253,0    964536 50333070 /usr/bin/bash
bash    20369 mingongge  mem    REG  253,0 106172832 50333042 /usr/lib/locale/locale-archive
bash    20369 mingongge  mem    REG  253,0     61560    18290 /usr/lib64/libnss_files-2.17.so
bash    20369 mingongge  mem    REG  253,0   2156240    18266 /usr/lib64/libc-2.17.so
bash    20369 mingongge  mem    REG  253,0     19248    18273 /usr/lib64/libdl-2.17.so
bash    20369 mingongge  mem    REG  253,0    174576    20696 /usr/lib64/libtinfo.so.5.9
bash    20369 mingongge  mem    REG  253,0    163312  1679434 /usr/lib64/ld-2.17.so
bash    20369 mingongge  mem    REG  253,0     26970 16806930 /usr/lib64/gconv/gconv-modules.cache
bash    20369 mingongge    0u   CHR  136,1       0t0        4 /dev/pts/1
bash    20369 mingongge    1u   CHR  136,1       0t0        4 /dev/pts/1
bash    20369 mingongge    2u   CHR  136,1       0t0        4 /dev/pts/1
bash    20369 mingongge  255u   CHR  136,1       0t0        4 /dev/pts/1
vim     20391 mingongge  cwd    DIR  253,0        82   462615 /home/mingongge
vim     20391 mingongge  rtd    DIR  253,0       262       64 /
vim     20391 mingongge  txt    REG  253,0   2337192 51061591 /usr/bin/vim
vim     20391 mingongge  mem    REG  253,0     61560    18290 /usr/lib64/libnss_files-2.17.so
vim     20391 mingongge  mem    REG  253,0 106172832 50333042 /usr/lib/locale/locale-archive
vim     20391 mingongge  mem    REG  253,0     11392     8814 /usr/lib64/libfreebl3.so
vim     20391 mingongge  mem    REG  253,0     14424  1679441 /usr/lib64/libutil-2.17.so
vim     20391 mingongge  mem    REG  253,0     40600    18271 /usr/lib64/libcrypt-2.17.so
vim     20391 mingongge  mem    REG  253,0    115816    18278 /usr/lib64/libnsl-2.17.so
vim     20391 mingongge  mem    REG  253,0    109976    18302 /usr/lib64/libresolv-2.17.so
vim     20391 mingongge  mem    REG  253,0     19896    46144 /usr/lib64/libattr.so.1.1.0
vim     20391 mingongge  mem    REG  253,0    402384    20698 /usr/lib64/libpcre.so.1.2.0
vim     20391 mingongge  mem    REG  253,0   2156240    18266 /usr/lib64/libc-2.17.so
vim     20391 mingongge  mem    REG  253,0    142144    18300 /usr/lib64/libpthread-2.17.so
vim     20391 mingongge  mem    REG  253,0   1647328   282389 /usr/lib64/perl5/CORE/libperl.so
vim     20391 mingongge  mem    REG  253,0     19248    18273 /usr/lib64/libdl-2.17.so
vim     20391 mingongge  mem    REG  253,0     27752      669 /usr/lib64/libgpm.so.2.1.0
vim     20391 mingongge  mem    REG  253,0     37064    18281 /usr/lib64/libacl.so.1.1.0
vim     20391 mingongge  mem    REG  253,0    174576    20696 /usr/lib64/libtinfo.so.5.9
vim     20391 mingongge  mem    REG  253,0    155744  1679449 /usr/lib64/libselinux.so.1
vim     20391 mingongge  mem    REG  253,0   1136944    18275 /usr/lib64/libm-2.17.so
vim     20391 mingongge  mem    REG  253,0    163312  1679434 /usr/lib64/ld-2.17.so
vim     20391 mingongge    0u   CHR  136,1       0t0        4 /dev/pts/1
vim     20391 mingongge    1u   CHR  136,1       0t0        4 /dev/pts/1
vim     20391 mingongge    2u   CHR  136,1       0t0        4 /dev/pts/1
vim     20391 mingongge    3u   REG  253,0     12288   462619 /home/mingongge/.test.sh.swp

然后我们使用下面的命令来终止这个用户的这些操作行为
[root@CentOS7-1 ~]# kill -9 `lsof -t -u mingongge`
[root@CentOS7-1 ~]# lsof -u mingongge
#你会发现这个用户的所有操作都被终止了
```

这个命令组合，在日常使用环境下还可以用于检查服务器被攻击的行为，如果有行为异常的用户登录操作，可以使用管理员暂时将此用户的一切操作全部干掉，然后再找出解决方法。