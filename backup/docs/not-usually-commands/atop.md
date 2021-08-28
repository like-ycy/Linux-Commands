## 命令简介

atop 命令是一款监控 Linux 系统资源与进程的工具，非内部命令，需要安装。

```
[root@centos7 ~]# atop
-bash: atop: command not found
[root@centos7 ~]# yum install atop -y

#Debian && Ubuntu
apt-get install atop

#Fedora
dnf install atop
```

atop 是以一定的频率记录系统的运行状态，所采集的数据包含系统资源(CPU、内存、磁盘和网络)使用情况和进程运行情况，并能以日志文件的方式保存在磁盘中，服务器出现问题后，我们可获取相应的atop日志文件进行分析，atop是一款开源软件。

## 语法格式

```
atop -w  file  [-S] [-a] [interval [samples]]
atop -r [file] [-b [YYYYMMDD]hhmm] [-e [YYYYMMDD]hhmm] [-flags]
```

## 选项说明

进程图的快捷键

```
g  #默认输出
m  #内存相关输出
d  #磁盘相关输出
n  #网络相关输出
c  #命令行输出
u  #查看对应的用户资源使用情况
p  #显示所有每个进程的所有信息占用情况（disk、mem、io）
P（大写） #正则匹配，显示所有匹配到的进程
q  #退出
```

## 应用举例

![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpCF2icTSH7m7Y0NQwcdSYFrDd5gverw0UJCng55w2EZ91Iaib3xP2mKLToqpwXCaYvhxPyQXDcXiczw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

```
[root@centos7 ~]# atop
ATOP - centos7              2021/03/29  08:33:28              ----------------              10s elapsed
PRC |  sys    0.18s |  user   0.35s  | #proc     95  |  #tslpu     0 |  #zombie    0  | #exit    0  |
CPU |  sys  1% |  user  3%  | irq  0%  |  idle     96% |  wait   0%  | ipc notavail  |
CPL |  avg1    0.27 |  avg5    0.13  | avg15   0.13  |  csw     1088 |  intr     954  | numcpu     1  |
MEM |  tot   972.3M |  free  203.3M  | cache 563.1M  |  buff    2.1M |  slab   83.8M  | hptot   0.0M  |
SWP |  tot     2.0G |  free    2.0G  | swcac   0.0M  |               |  vmcom 266.0M  | vmlim   2.5G  |
NET |  transport    |  tcpi   1  | tcpo       1  |  udpi       1 |  udpo       1  | tcpao      0  |
NET |  network      |  ipi   17  | ipo    3  |  ipfrw    0 |  deliv     17  | icmpo      1  |
NET |  ens33   ---- |  pcki  20  | pcko       5  |  sp    0 Mbps |  si    6 Kbps  | so    1 Kbps  |

   PID SYSCPU  USRCPU RDELAY   VGROW  RGROW   RDDSK  WRDSK  ST  EXC  THR  S CPUNR   CPU CMD         1/1
 18378  0.08s   0.33s  0.11s      0K     0K      0K     0K  --    -    3  S     0    4% python3
 27620  0.04s   0.02s  0.00s   0K     0K  0K     0K  --    -    1  R     0    1% atop
 27664  0.04s   0.00s  0.02s   0K     0K  0K     0K  --    -    1  S     0    0% kworker/0:1
   404  0.02s   0.00s  0.05s      0K     0K      0K     0K  --    -    1  R     0    0% xfsaild/dm-0
   872  0.00s   0.00s  0.00s      0K     0K      0K     0K  --    -    5  S     0    0% tuned
 19670  0.00s   0.00s  0.00s      0K     0K      0K     0K  --    -    1  S     0    0% sshd
   870  0.00s   0.00s  0.00s      0K     0K      0K     0K  --    -    3  S     0    0% rsyslogd
     1  0.00s   0.00s  0.00s      0K     0K  0K     0K  --    -    1  S     0    0% systemd
     6  0.00s   0.00s  0.09s   0K     0K  0K     0K  --    -    1  S     0    0% ksoftirqd/0
     9  0.00s   0.00s  0.29s   0K     0K  0K     0K  --    -    1  R     0    0% rcu_sched
 26820  0.00s   0.00s  0.00s   0K     0K  0K     0K  --    -    1  S     0    0% kworker/0:2
```

###### 输出信息的详细说明如下

```s
ATOP列：该列显示了主机名、信息采样日期和时间点

PRC列：该列显示进程整体运行情况
sys、usr字段  #进程在内核态和用户态的运行时间
proc字段      #进程总数
zombie字段    #僵死进程的数量
exit字段      #atop采样周期期间退出的进程数量

CPU列：该列显示CPU整体(即多核CPU作为一个整体CPU资源)的使用情况

sys、usr字段   #CPU被用于处理进程时，进程在内核态、用户态所占CPU的时间比例
irq字段   #CPU被用于处理中断的时间比例
idle字段  #CPU处在完全空闲状态的时间比例
wait字段  #CPU处在“进程等待磁盘IO导致CPU空闲”状态的时间比例

cpu列：该列显示某一核cpu的使用情况

CPL列：该列显示CPU负载情况
avg1、avg5和avg15字段  #过去1分钟、5分钟和15分钟内运行队列中的平均进程数量
csw字段   #上下文交换次数
intr字段  #中断发生次数

MEM列：该列显示内存的使用情况
tot字段    #物理内存总量
free字段   #空闲内存的大小
cache字段  #用于页缓存的内存大小
buff字段   #用于文件缓存的内存大小
slab字段   #系统内核占用的内存大小

SWP列：该列显示交换空间的使用情况
tot字段   #交换区总量
free字段  #空闲交换空间大小

PAG列：该列显示虚拟内存分页情况
swin、swout字段  #换入和换出内存页数

DSK列：该列显示磁盘使用情况
sda字段   #磁盘设备标识
busy字段  #磁盘忙时比例
read、write字段  #读、写请求数量


NET列：显示网络状况，包括传输层(TCP和UDP)、IP层以及各活动的网口信息

XXXi 字段  #各层或活动网口收包数目
XXXo 字段  #各层或活动网口发包数目
```