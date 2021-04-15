## 命令简介

accton 命令是 Linux 系统进程管理命令之一，它的作用是打开进程统计，如果命令后面不带任何参数，就是关闭进程统计。

默认系统是没有安装此命令的，需要用户在使用前自行安装，命令如下。

```
#CentOS
[root@centos7 ~]# acct
-bash: acct: command not found
[root@centos7 ~]# yum install psacct -y 
#Debian && Ubuntu
apt-get install acct
#Fedora
dnf install psacct
```

安装完成之后，默认情况下，psacct 服务是关闭状态，在 RHEL/CentOS/Fedora 待系统下，需要用户手动去开启该服务。

```
[root@centos7 ~]# systemctl status psacct.service
● psacct.service - Kernel process accounting
   Loaded: loaded (/usr/lib/systemd/system/psacct.service; disabled; vendor preset: disabled)
   Active: inactive (dead)
[root@centos7 ~]# systemctl start psacct.service
[root@centos7 ~]# systemctl status psacct.service
● psacct.service - Kernel process accounting
   Loaded: loaded (/usr/lib/systemd/system/psacct.service; disabled; vendor preset: disabled)
   Active: active (exited) since Mon 2021-03-29 08:00:51 EDT; 2s ago
  Process: 25987 ExecStart=/usr/sbin/accton /var/account/pacct (code=exited, status=0/SUCCESS)
  Process: 25985 ExecStartPre=/usr/libexec/psacct/accton-create (code=exited, status=0/SUCCESS)
 Main PID: 25987 (code=exited, status=0/SUCCESS)
```

## 语法格式

```
accton [OPTION] on|off|ACCOUNTING_FILE
```

## 选项说明

```
-p filename    #指定密码文件filename
--version  #显示ac版本并退出
--help     #打印命令概要
```

准确的说 acct 是一个工具包，里面包含有**针对用户连接时间、进程执行情况等进行统计**的工具。它可以**记录用户登录信息。用户所执行的程序，程序执行情况信息**等。acct 包含以下工具包命令：

```
ac   #显示登录账号的简要信息
accton    #打开或关闭进程记录功能
last      #显示曾经登录过的用户
lastcomm  #显示已执行过的命令
sa        #进程用户记录信息的摘要
dump-utmp   #输出utmp文件内容
dump-acct   #输出acct或pacct文件内容
```

accton 命令参数

```
on               Activate process accounting and use default file
off              Deactivate process accounting
ACCOUNTING_FILE  Activate (if not active) and save information in
this file
 
The system's default process accounting file is '/var/account/pacct'.
 
Report bugs to <bug-acct@gnu.org>
```

相关的详细信息可查看帮助文件

## 应用举例

```
#显示用户连接时间的统计信息
[root@centos7 ~]# ac
 total      173.79

#输出每天的总登录时间（小时）
[root@centos7 ~]# ac -d
Aug 20 total       13.60
Aug 30 total        3.19
Dec 24 total        0.28
Jan  2 total       21.99
Jan 15 total        1.22
Jan 16 total       23.75
Jan 17 total       31.34
Mar 10 total        7.38
Mar 21 total        2.84
Mar 23 total        0.04
Mar 24 total       24.62
Mar 27 total        0.66
Mar 28 total       22.98
Today total       19.90

#显示每个用户的总登录时间（小时）
[root@centos7 ~]# ac -p
 root                               173.79
 total      173.79
```

显示指定用户的每天登录时长（小时）

```
[root@centos7 ~]# ac -d mingongge
[root@centos7 ~]# ac -d root
Aug 20 total       13.60
Aug 30 total        3.19
Dec 24 total        0.28
Jan  2 total       21.99
Jan 15 total        1.22
Jan 16 total       23.75
Jan 17 total       31.34
Mar 10 total        7.38
Mar 21 total        2.84
Mar 23 total        0.04
Mar 24 total       24.62
Mar 27 total        0.66
Mar 28 total       22.98
Today total       19.98
```

打开或关闭进程账号记录功能

```
[root@centos7 ~]# accton on
Turning on process accounting, file set to the default '/var/account/pacct'.
[root@centos7 ~]# accton off
Turning off process accounting.
```

其它工具包举例

```
#显示曾经登录过的用户
[root@centos7 ~]# last
root     pts/2        192.168.1.93     Mon Mar 29 05:57   still logged in   
root     tty1                          Mon Mar 29 05:31   still logged in   
root     pts/1        192.168.1.93     Mon Mar 29 05:12 - 07:56  (02:44)    
root     pts/1        192.168.1.93     Mon Mar 29 05:08 - 05:11  (00:02)    
root     pts/0        192.168.1.93     Mon Mar 29 05:00 - 07:08  (02:08)    
root     pts/1        192.168.1.93     Sun Mar 28 23:42 - 04:59  (05:17)    
root     pts/0        192.168.1.93     Sun Mar 28 12:03 - 05:00  (16:56)    
root     pts/0        192.168.1.93     Sun Mar 28 10:38 - 12:00  (01:22)    
root     pts/0        192.168.1.93     Sun Mar 28 02:10 - 09:22  (07:12)    
root     pts/0        192.168.1.93     Sun Mar 28 02:07 - 02:10  (00:02)    
root     pts/1        192.168.1.93     Sun Mar 28 01:35 - 01:36  (00:00)    
root     pts/0        192.168.1.93     Sat Mar 27 23:20 - 02:07  (02:47)    
reboot   system boot  3.10.0-1127.18.2 Sat Mar 27 04:58 - 08:19 (2+03:20)   
root     pts/0        192.168.1.93     Wed Mar 24 21:09 - crash (2+07:49)   
root     pts/1        192.168.1.93     Wed Mar 24 15:15 - 15:54  (00:39)    
root     pts/0        192.168.1.93     Wed Mar 24 14:49 - 21:08  (06:19)    
root     pts/0        192.168.1.93     Wed Mar 24 05:44 - 14:48  (09:04)    
root     pts/0        192.168.1.93     Wed Mar 24 04:10 - 05:43  (01:33)    
root     pts/0        192.168.1.93     Tue Mar 23 23:57 - 04:10  (04:12)    
reboot   system boot  3.10.0-1127.18.2 Tue Mar 23 23:56 - 08:19 (5+08:22)   
root     pts/0        192.168.1.93     Tue Mar 23 23:27 - crash  (00:29)    
reboot   system boot  3.10.0-1127.18.2 Mon Mar 22 07:22 - 08:19 (7+00:56)   
root     pts/0        192.168.1.93     Sun Mar 21 10:31 - 12:15  (01:43)    
root     pts/0        192.168.1.93     Sun Mar 21 10:07 - 10:30  (00:23)    
root     pts/0        192.168.1.93     Sun Mar 21 01:29 - 02:12  (00:43)    
reboot   system boot  3.10.0-1127.18.2 Sun Mar 21 01:28 - 08:19 (8+06:50)   
root     pts/0        192.168.1.93     Wed Mar 10 11:20 - 14:32  (03:12)    
root     pts/1        192.168.1.93     Wed Mar 10 10:39 - 11:11  (00:32)    
root     pts/1        192.168.1.93     Wed Mar 10 09:14 - 10:38  (01:24)    
root     pts/1        192.168.1.93     Wed Mar 10 09:04 - 09:05  (00:00)    
root     pts/0        192.168.1.93     Wed Mar 10 09:00 - 11:13  (02:13)    
reboot   system boot  3.10.0-1127.18.2 Mon Mar  8 10:20 - 08:19 (20+20:58)  
root     pts/2        centos7          Sun Jan 17 14:30 - 15:31  (01:00)    
root     pts/0        192.168.1.93     Sun Jan 17 14:26 - 15:31  (01:04)    
root     pts/0        192.168.1.93     Sun Jan 17 12:44 - 14:01  (01:16)    
root     tty1                          Sun Jan 17 12:43 - crash (49+21:37)  
root     pts/1        192.168.1.93     Sun Jan 17 08:32 - 14:42  (06:10)    
root     pts/0        192.168.1.93     Sun Jan 17 08:26 - 10:31  (02:05)    
root     pts/0        192.168.1.93     Sat Jan 16 19:34 - 08:25  (12:51)    
root     pts/0        192.168.1.93     Sat Jan 16 16:17 - 19:33  (03:16)    
root     pts/0        192.168.1.93     Sat Jan 16 15:43 - 16:15  (00:31)    
root     pts/0        192.168.1.93     Sat Jan 16 10:28 - 15:43  (05:14)    
root     pts/0        192.168.1.93     Sat Jan 16 09:51 - 10:27  (00:36)    
root     pts/0        192.168.1.93     Sat Jan 16 03:35 - 09:51  (06:15)    
root     pts/0        192.168.1.93     Fri Jan 15 22:46 - 03:23  (04:37)    
reboot   system boot  3.10.0-1127.18.2 Thu Jan 14 05:41 - 08:19 (74+01:37)  
root     pts/0        192.168.1.93     Sat Jan  2 08:42 - 11:04  (02:22)    
root     pts/0        192.168.1.93     Sat Jan  2 06:42 - 08:41  (01:59)    
root     tty1                          Sat Jan  2 06:22 - crash (11+23:19)  
reboot   system boot  3.10.0-1127.18.2 Sat Jan  2 06:21 - 08:19 (86+00:58)  
root     pts/0        192.168.1.93     Thu Dec 24 22:33 - 22:39  (00:06)    
root     tty1                          Thu Dec 24 22:29 - 22:40  (00:10)    
reboot   system boot  3.10.0-1127.18.2 Thu Dec 24 22:28 - 22:40  (00:12)    
root     pts/1        192.168.1.93     Sun Aug 30 03:58 - down   (00:44)    
root     pts/0        192.168.1.93     Sun Aug 30 03:29 - down   (01:13)    
root     tty1                          Sun Aug 30 03:29 - 04:42  (01:13)    
reboot   system boot  3.10.0-1127.18.2 Sun Aug 30 03:28 - 04:42  (01:14)    
root     pts/1        192.168.1.93     Thu Aug 20 11:20 - crash (9+16:08)   
root     pts/0        192.168.1.93     Thu Aug 20 10:46 - 11:39  (00:53)    
reboot   system boot  3.10.0-1062.el7. Thu Aug 20 10:45 - 04:42 (9+17:57)   
root     tty1                          Thu Aug 20 10:42 - 10:45  (00:02)    
reboot   system boot  3.10.0-1062.el7. Thu Aug 20 10:42 - 10:45  (00:03)    

wtmp begins Thu Aug 20 10:42:00 2020

#显示已执行过的命令
[root@centos7 ~]# lastcomm
last                   root     pts/2      0.01 secs Mon Mar 29 08:19
bash              F    root     pts/2      0.00 secs Mon Mar 29 08:19
cat                    root     pts/2      0.00 secs Mon Mar 29 08:18
accton           S     root     pts/2      0.00 secs Mon Mar 29 08:18
accton                 root     pts/2      0.00 secs Mon Mar 29 08:17
accton           S     root     pts/2      0.00 secs Mon Mar 29 08:17
accton                 root     pts/2      0.00 secs Mon Mar 29 08:17
accton           S     root     pts/2      0.00 secs Mon Mar 29 08:17
accton                 root     pts/2      0.00 secs Mon Mar 29 08:17
ac                     root     pts/2      0.00 secs Mon Mar 29 08:15
ac                     root     pts/2      0.00 secs Mon Mar 29 08:15
ac                     root     pts/2      0.00 secs Mon Mar 29 08:13
ac                     root     pts/2      0.00 secs Mon Mar 29 08:13
ac                     root     pts/2      0.00 secs Mon Mar 29 08:13
kworker/0:2       F    root     __         0.00 secs Mon Mar 29 08:07
kworker/0:0       F    root     __         2.36 secs Mon Mar 29 07:20
systemd-cgroups  S     root     __         0.00 secs Mon Mar 29 08:10
crond            SF    root     __         0.01 secs Mon Mar 29 08:10
sadc             S     root     __         0.01 secs Mon Mar 29 08:10
date                   root     __         0.00 secs Mon Mar 29 08:10
date                   root     __         0.00 secs Mon Mar 29 08:10
kworker/0:2       F    root     __         0.22 secs Mon Mar 29 07:47
accton                 root     pts/2      0.00 secs Mon Mar 29 08:03
systemd-cgroups  S     root     __         0.00 secs Mon Mar 29 08:01
crond            SF    root     __         0.02 secs Mon Mar 29 08:01
run-parts              root     __         0.00 secs Mon Mar 29 08:01
logger                 root     __         0.00 secs Mon Mar 29 08:01
basename               root     __         0.00 secs Mon Mar 29 08:01
awk                    root     __         0.00 secs Mon Mar 29 08:01
0anacron               root     __         0.00 secs Mon Mar 29 08:01
date                   root     __         0.00 secs Mon Mar 29 08:01
cat                    root     __         0.00 secs Mon Mar 29 08:01
logger                 root     __         0.00 secs Mon Mar 29 08:01
basename               root     __         0.00 secs Mon Mar 29 08:01
run-parts         F    root     __         0.00 secs Mon Mar 29 08:01
systemctl        S     root     pts/2      0.00 secs Mon Mar 29 08:00
systemctl        S     root     pts/2      0.00 secs Mon Mar 29 08:00
pkttyagent           X root     pts/2      0.03 secs Mon Mar 29 08:00
systemd-tty-ask        root     pts/2      0.01 secs Mon Mar 29 08:00
systemd-cgroups  S     root     __         0.00 secs Mon Mar 29 08:00
accton           S     root     __         0.00 secs Mon Mar 29 08:00

#输出所有的帐户活动信息
[root@centos7 ~]# sa
      42      76.03re       0.04cp         0avio     15376k
      11      52.42re       0.04cp         0avio     22963k   ***other*
       2      23.59re       0.00cp         0avio         0k   kworker/0:2*
       2       0.00re       0.00cp         0avio     32128k   crond*
       8       0.00re       0.00cp         0avio       795k   accton
       5       0.01re       0.00cp         0avio      1092k   ac
       3       0.00re       0.00cp         0avio      2168k   systemd-cgroups
       3       0.00re       0.00cp         0avio     27024k   date
       2       0.01re       0.00cp         0avio     33728k   systemctl
       2       0.00re       0.00cp         0avio     27024k   cat
       2       0.00re       0.00cp         0avio     27008k   logger
       2       0.00re       0.00cp         0avio     27008k   basename
```

这个命令所包含的这些工具包，功能还是非常强大的，在日常工作中可以很大程度提高我们的工作效率，解决一些问题。