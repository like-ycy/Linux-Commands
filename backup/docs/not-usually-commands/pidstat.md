## 命令简介

pidstat 是著名的采集软件 systat 的组件之一。用于监控全部或指定进程的 CPU、内存、线程、设备 IO 等系统资源的占用情况。

pidstat 首次运行时显示自系统启动开始的各项统计信息，之后运行 pidstat 将显示自上次运行该命令以后的统计信息。用户可以通过指定统计的次数和时间来获得所需的统计信息。

```
[root@centos7 ~]# pidstat
-bash: pdistat: command not found
[root@centos7 ~]# yum install sysstat -y
```

## 语法格式

```
 pidstat [ options ] [ <interval> [ <count> ] ]
```

## 选项说明

```
-u  #显示各个进程的cpu使用统计
-r  #显示各个进程的内存使用统计
-d  #显示各个进程的IO使用情况
-p  #指定进程号
-w  #显示每个进程的上下文切换情况
-t  #显示选择任务的线程的统计信息外的额外信息
-V  #版本号
-h  #在一行上显示了所有活动，这样其他程序可以容易解析
-I  #在SMP环境，表示任务的CPU使用率/内核数量
-l  #显示命令名和所有参数
-T { TASK | CHILD | ALL }  #指定了pidstat监控的
-C <command>  #查看对应command进程的状态
[ <interval> [ <count> ]
interval #显示间隔，单位s
count    #显示次数，默认一直显示
```

## 应用举例

显示所有进程使用 cpu 的情况

```
[root@centos7 ~]# pidstat -u -p ALL
Linux 3.10.0-1127.18.2.el7.x86_64 (centos7)  03/29/2021  _x86_64_ (1 CPU)

09:50:17 AM   UID       PID    %usr %system  %guest    %CPU   CPU  Command
09:50:17 AM     0         1    0.01    0.02    0.00    0.03     0  systemd
09:50:17 AM     0         2    0.00    0.00    0.00    0.00     0  kthreadd
09:50:17 AM     0         4    0.00    0.00    0.00    0.00     0  kworker/0:0H
09:50:17 AM     0         6    0.00    0.03    0.00    0.03     0  ksoftirqd/0
09:50:17 AM     0         7    0.00    0.00    0.00    0.00     0  migration/0
09:50:17 AM     0         8    0.00    0.00    0.00    0.00     0  rcu_bh
09:50:17 AM     0         9    0.00    0.02    0.00    0.02     0  rcu_sched
09:50:17 AM     0        10    0.00    0.00    0.00    0.00     0  lru-add-drain
09:50:17 AM     0        11    0.00    0.01    0.00    0.01     0  watchdog/0
09:50:17 AM     0        13    0.00    0.00    0.00    0.00     0  kdevtmpfs
09:50:17 AM     0        14    0.00    0.00    0.00    0.00     0  netns
09:50:17 AM     0        15    0.00    0.00    0.00    0.00     0  khungtaskd
09:50:17 AM     0        16    0.00    0.00    0.00    0.00     0  writeback
09:50:17 AM     0        17    0.00    0.00    0.00    0.00     0  kintegrityd
09:50:17 AM     0        18    0.00    0.00    0.00    0.00     0  bioset
09:50:17 AM     0        19    0.00    0.00    0.00    0.00     0  bioset
09:50:17 AM     0        20    0.00    0.00    0.00    0.00     0  bioset
09:50:17 AM     0        21    0.00    0.00    0.00    0.00     0  kblockd

#pidstat -u -p ALL 与pidstat命令功能一样
```

输出的信息说明

```
PID     #进程ID
%usr    #进程在用户空间占用cpu的百分比
%system #进程在内核空间占用cpu的百分比
%guest  #进程在虚拟机占用cpu的百分比
%CPU    #进程占用cpu的百分比
CPU     #处理进程的cpu编号
Command #当前进程对应的命令
```

显示各活动进程的内存使用情况

```
[root@centos7 ~]# pidstat -r
Linux 3.10.0-1127.18.2.el7.x86_64 (centos7)  03/29/2021  _x86_64_ (1 CPU)

09:54:32 AM   UID       PID  minflt/s  majflt/s     VSZ    RSS   %MEM  Command
09:54:32 AM     0         1      0.21      0.00  125616   4056   0.41  systemd
09:54:32 AM     0       484      0.06      0.00   37112   3412   0.34  systemd-journal
09:54:32 AM     0       503      0.01      0.00  190376   1336   0.13  lvmetad
09:54:32 AM     0       509      0.02      0.00   44976   1928   0.19  systemd-udevd
09:54:32 AM     0       600      0.00      0.00   55532    848   0.09  auditd
09:54:32 AM   999       623      0.03      0.00  612368  12268   1.23  polkitd
09:54:32 AM    81       626      0.01      0.00   58244   2484   0.25  dbus-daemon
09:54:32 AM     0       634      0.03      0.00  476428   8744   0.88  NetworkManager
09:54:32 AM     0       635      0.02      0.00   26384   1792   0.18  systemd-logind
09:54:32 AM     0       638      0.03      0.00  126420   1624   0.16  crond
09:54:32 AM     0       643      0.01      0.00   99208   2696   0.27  login
09:54:32 AM   998       646      0.01      0.00  120408   2116   0.21  chronyd
09:54:32 AM     0       868      0.02      0.00  112924   4356   0.44  sshd
09:54:32 AM     0       870      0.02      0.00  220796   5196   0.52  rsyslogd
09:54:32 AM     0       872      0.12      0.00  574304  17456   1.75  tuned
```

输出信息详细说明

```
PID        #进程标识符
Minflt/s   #任务每秒发生的次要错误，不需要从磁盘中加载页
Majflt/s   #任务每秒发生的主要错误，需要从磁盘中加载页
VSZ        #虚拟地址大小，虚拟内存的使用KB
RSS        #常驻集合大小，非交换区五里内存使用KB
Command    #task命令名
```

显示各个进程的IO使用情况

```
[root@centos7 ~]# pidstat -d
Linux 3.10.0-1127.18.2.el7.x86_64 (centos7)  03/29/2021  _x86_64_ (1 CPU)

09:56:29 AM   UID       PID   kB_rd/s   kB_wr/s kB_ccwr/s  Command
09:56:29 AM     0         1      1.41      2.11      0.30  systemd
09:56:29 AM     0       404      0.00      0.00      0.00  xfsaild/dm-0
09:56:29 AM     0       484      0.01      0.00      0.00  systemd-journal
09:56:29 AM     0       503      0.00      0.00      0.00  lvmetad
09:56:29 AM     0       509      0.22      0.00      0.00  systemd-udevd
09:56:29 AM     0       578      0.00      0.00      0.00  xfsaild/sda1
09:56:29 AM     0       600      0.00      0.01      0.00  auditd
09:56:29 AM   999       623      0.08      0.00      0.00  polkitd
09:56:29 AM    81       626      0.01      0.00      0.00  dbus-daemon
09:56:29 AM     0       634      0.11      0.00      0.00  NetworkManager
09:56:29 AM     0       635      0.01      0.00      0.00  systemd-logind
09:56:29 AM     0       638      0.00      0.01      0.00  crond
09:56:29 AM     0       643      0.00      0.00      0.00  login
09:56:29 AM   998       646      0.01      0.00      0.00  chronyd
09:56:29 AM     0       868      2.34      0.14      0.05  sshd
09:56:29 AM     0       870      0.01      0.03      0.01  rsyslogd
09:56:29 AM     0       872      0.10      0.00      0.00  tuned
09:56:29 AM     0       972      0.01      0.00      0.00  master
09:56:29 AM    89       974      0.00      0.00      0.00  qmgr
09:56:29 AM     0     18356      0.00      0.00      0.00  bash
09:56:29 AM     0     18378      0.00      0.00      0.00  python3
09:56:29 AM     0     19673      1.83      2.92      0.04  bash
```

输出信息的详细说明

```
PID        #进程id
kB_rd/s    #每秒从磁盘读取的KB
kB_wr/s    #每秒写入磁盘KB
kB_ccwr/s  #任务取消的写入磁盘的KB
COMMAND    #task的命令名
```

显示每个进程的上下文切换情况

```
[root@centos7 ~]# pidstat -w
Linux 3.10.0-1127.18.2.el7.x86_64 (centos7)  03/29/2021  _x86_64_ (1 CPU)

10:02:46 AM   UID       PID   cswch/s nvcswch/s  Command
10:02:46 AM     0         1      0.32      0.04  systemd
10:02:46 AM     0         2      0.00      0.00  kthreadd
10:02:46 AM     0         4      0.00      0.00  kworker/0:0H
10:02:46 AM     0         6      1.55      0.00  ksoftirqd/0
10:02:46 AM     0         7      0.01      0.00  migration/0
10:02:46 AM     0         8      0.00      0.00  rcu_bh
10:02:46 AM     0         9      7.02      0.00  rcu_sched
10:02:46 AM     0        10      0.00      0.00  lru-add-drain
10:02:46 AM     0        11      0.26      0.00  watchdog/0
10:02:46 AM     0        13      0.00      0.00  kdevtmpfs
10:02:46 AM     0        14      0.00      0.00  netns
10:02:46 AM     0        15      0.01      0.00  khungtaskd
10:02:46 AM     0        16      0.00      0.00  writeback
10:02:46 AM     0        17      0.00      0.00  kintegrityd
```

输出信息的详细说明

```
PID        #进程id
Cswch/s    #每秒主动任务上下文切换数量
Nvcswch/s  #每秒被动任务上下文切换数量
Command    #命令名
```

显示线程的统计信息外的其它信息

```
[root@centos7 ~]# pidstat -t
Linux 3.10.0-1127.18.2.el7.x86_64 (centos7)  03/29/2021  _x86_64_ (1 CPU)

10:04:40 AM   UID      TGID       TID    %usr %system  %guest    %CPU   CPU  Command
10:04:40 AM     0         1         -    0.01    0.02    0.00    0.03     0  systemd
10:04:40 AM     0         -         1    0.01    0.02    0.00    0.02     0  |__systemd
10:04:40 AM     0         2         -    0.00    0.00    0.00    0.00     0  kthreadd
10:04:40 AM     0         -         2    0.00    0.00    0.00    0.00     0  |__kthreadd
10:04:40 AM     0         6         -    0.00    0.03    0.00    0.03     0  ksoftirqd/0
10:04:40 AM     0         -         6    0.00    0.03    0.00    0.03     0  |__ksoftirqd/0
10:04:40 AM     0         9         -    0.00    0.02    0.00    0.02     0  rcu_sched
10:04:40 AM     0         -         9    0.00    0.02    0.00    0.02     0  |__rcu_sched
10:04:40 AM     0        11         -    0.00    0.01    0.00    0.01     0  watchdog/0
10:04:40 AM     0         -        11    0.00    0.01    0.00    0.01     0  |__watchdog/0
10:04:40 AM     0        15         -    0.00    0.00    0.00    0.00     0  khungtaskd
10:04:40 AM     0         -        15    0.00    0.00    0.00    0.00     0  |__khungtaskd
10:04:40 AM     0        32         -    0.00    0.00    0.00    0.00     0  khugepaged
```

输出信息的详细说明

```
TGID   #主线程的表示
TID    #线程id
%usr   #进程在用户空间占用cpu的百分比
%system  #进程在内核空间占用cpu的百分比
%guest   #进程在虚拟机占用cpu的百分比
%CPU     #进程占用cpu的百分比
CPU      #处理进程的cpu编号
Command  #当前进程对应的命令
```

查看指定进程的信息

```
[root@centos7 ~]# pidstat -r -w  -d -p 18356
Linux 3.10.0-1127.18.2.el7.x86_64 (centos7)  03/29/2021  _x86_64_ (1 CPU)

10:09:37 AM   UID       PID  minflt/s  majflt/s     VSZ    RSS   %MEM  Command
10:09:37 AM     0     18356      0.01      0.00  115676   2076   0.21  bash

10:09:37 AM   UID       PID   kB_rd/s   kB_wr/s kB_ccwr/s  Command
10:09:37 AM     0     18356      0.00      0.00      0.00  bash

10:09:37 AM   UID       PID   cswch/s nvcswch/s  Command
10:09:37 AM     0     18356      0.00      0.00  bash
[root@centos7 ~]# pidstat  -t -p 18356
Linux 3.10.0-1127.18.2.el7.x86_64 (centos7)  03/29/2021  _x86_64_ (1 CPU)

10:09:51 AM   UID      TGID       TID    %usr %system  %guest    %CPU   CPU  Command
10:09:51 AM     0     18356         -    0.00    0.00    0.00    0.00     0  bash
10:09:51 AM     0         -     18356    0.00    0.00    0.00    0.00     0  |__bash
```

