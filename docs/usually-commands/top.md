## 命令简介

top 命令用于实时显示系统资源使用情况。它可以显示系统摘要信息，以及内核当前正在管理的进程或线程的列表。

top 命令可以实时动态地查看系统的整体运行情况，是一个非常实用的系统性能和运行信息的监测工具。通过 top 命令所提供的互动式界面，用热键可以管理。

## 语法格式

```
top [options]
```

## 选项说明

```
-b  #以批处理模式操作
-c  #显示完整的治命令
-d  #屏幕刷新间隔时间
-I  #忽略失效过程
-s  #保密模式
-S  #累积模式
-i<时间>  #设置间隔时间
-u<用户名>  #指定用户名
-p<进程号>  #指定进程
-n<次数>  #循环显示的次数
```

## top交互命令

在 top 命令执行过程中会使用到一些交互命令，这些命令都是单字母，如下。

```
h  #显示帮助信息界面
k  #终止一个进程
i  #忽略闲置和僵死进程，这是一个开关式命令
q  #退出程序
r  #重新安排一个进程的优先级别
S  #切换到累计模式
s  #改变两次刷新之间的延迟时间（单位为s），默认值是5s
f或者F  #从当前显示中添加或者删除项目
o或者O  #改变显示项目的顺序
l  #切换显示平均负载和启动时间信息
m  #切换显示内存信息
t  #切换显示进程和CPU状态信息
c  #切换显示命令名称和完整命令行
M  #根据驻留内存大小进行排序
P  #根据CPU使用百分比大小进行排序
T  #根据时间/累计时间进行排序
w  #将当前设置写入~/.toprc文件中
```

## 应用举例

查看系统整体运行信息

```
[root@centos7 ~]# top
top - 05:59:56 up 1 day,  7:13,  1 user,  load average: 0.06, 0.03, 0.05
Tasks:  92 total,   2 running,  90 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.3 sy,  0.0 ni, 99.7 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :   995684 total,   473120 free,   124960 used,   397604 buff/cache
KiB Swap:  2097148 total,  2097148 free,        0 used.   698120 avail Mem 

   PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND                                                                                               
   860 root      20   0  574304  17416   6112 S  0.3  1.7   1:01.09 tuned                                                                                                 
  2250 root      20   0  161536   6112   4720 S  0.3  0.6   0:02.82 sshd                                                                                                  
 18762 root      20   0       0      0      0 S  0.3  0.0   0:02.76 kworker/0:2                                                                                           
 21244 root      20   0  161996   2188   1552 R  0.3  0.2   0:00.19 top                                                                                                   
     1 root      20   0  125372   3840   2564 S  0.0  0.4   0:23.04 systemd                                                                                               
     2 root      20   0       0      0      0 S  0.0  0.0   0:00.03 kthreadd                                                                                              
     4 root       0 -20       0      0      0 S  0.0  0.0   0:00.00 kworker/0:0H                                                                                          
     6 root      20   0       0      0      0 S  0.0  0.0   0:17.53 ksoftirqd/0                                                                                           
     7 root      rt   0       0      0      0 S  0.0  0.0   0:00.00 migration/0                                                                                           
     8 root      20   0       0      0      0 S  0.0  0.0   0:00.00 rcu_bh                                                                                                
     9 root      20   0       0      0      0 S  0.0  0.0   0:12.19 rcu_sched                                                                                             
    10 root       0 -20       0      0      0 S  0.0  0.0   0:00.00 lru-add-drain                                                                                         
    11 root      rt   0       0      0      0 S  0.0  0.0   0:07.75 watchdog/0                                                                                            
    13 root      20   0       0      0      0 S  0.0  0.0   0:00.00 kdevtmpfs                                                                                             
    14 root       0 -20       0      0      0 S  0.0  0.0   0:00.00 netns                                                                                                 
    15 root      20   0       0      0      0 S  0.0  0.0   0:00.19 khungtaskd                                                                                            
    16 root       0 -20       0      0      0 S  0.0  0.0   0:00.00 writeback                                                                                             
    17 root       0 -20       0      0      0 S  0.0  0.0   0:00.00 kintegrityd
```

上述结果信息详细说明

```
top - 05:59:56  #当前系统时间
up 1 day    #系统已经运行了1天
1 user    #当前登录用户个数 
load average: 0.06, 0.03, 0.05   #系统负载信息

Tasks:  
92 total  #总进程数 
2 running #正在运行的进程数
90 sleeping   #休眠的进程数
0 stopped     #停止的进程数
0 zombie      #冻结的进程数

%Cpu(s):  
0.0 us  #用户空间占用CPU的百分比 
0.3 sy  #内核空间占用CPU的百分比
0.0 ni  #用户进程空间内改变过优先级的进程占用CPU百分比
99.7 id #空闲CPU百分比
0.0 wa  #等待输入输出的CPU时间百分比
0.0 hi  #硬中断占用CPU的百分比 
0.0 si  #软中断占用CPU的百分比
0.0 st  #虚拟机占用百分比 

KiB Mem :   
995684 total  #物理内存的总量
473120 free   #剩余内存的总量
124960 used   #已使用内存的总量
397604 buff/cache  #内核缓存所使用内存的量

KiB Swap:  
2097148 total   #交换分区的总量
2097148 free    #交换分区剩余的总量    
0 used          #交换分区已使用的总量
698120 avail Mem  #可用内存总量

PID  #进程id
USER #进程所有者
PR  #任务的调度优先级，范围0-31，数值越低，优先级越高
NI  #nice值，范围-20到+19，用于调整进程优先级
VIRT #进程所使用的虚拟内存总量（单位 KB）
RES  #任务已使用的未交换物理内存（单位 KB）
SHR  #共享内存大小（单位 KB）
S    #进程状态
      ' D '=不间断的睡眠
      ' R '=运行
      ' S '=睡眠
      ' T '=被跟踪或停止的
      ' Z '=僵尸
%CPU #CPU的使用率
%MEM #内存使用率
TIME+ #CPU时间
COMMAND #进程名称（命令名/命令行），显示用于启动任务的命令行或关联程序的名称。
```

显示帮助信息界面![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpE6EBryOnicNNZg6y5P5hXuqztnJAgWIK4ovxbC6yhvxRicAKBh2lichW2sD7kNnKj7eOicDI275aySg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)切换内存显示信息

![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpE6EBryOnicNNZg6y5P5hXu8AZ2ZqclXlUGBfKZ85UZDpnkYhkuNUp6r2ofgjn8jg0bic0vtAnpGMg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

再按一次m再切换一次![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpE6EBryOnicNNZg6y5P5hXubczWkZVLxOKG1BEkwz72yjVHGUp1VhYhEKAShM5VEKbMndbRKhyiapw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)切换显示命令的完整命令

![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpE6EBryOnicNNZg6y5P5hXupDFuOseddTVYia5ZcSTBKhFib8Nf8gb9VfVWI7fHl3IjF7mkeuNiblQTw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)