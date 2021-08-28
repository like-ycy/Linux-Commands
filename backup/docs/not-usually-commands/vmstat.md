## 命令简介

vmstat 命令用于虚拟内存统计。vmstat 报告有关进程，内存，分页，块IO，陷阱，磁盘和CPU活动的信息。

## 语法格式

```
vmstat [options] [delay [count]]
```

## 选项说明

```
-a  #显示活动内页
-f  #显示启动后创建的进程总数
-m  #显示slab信息
-h  #显示帮助并退出
-n  #头信息仅显示一次
-s  #以表格方式显示事件计数器和内存状态
-d  #报告磁盘状态
-p  #显示指定的硬盘分区状态
-S  #输出信息的单位
-V  #显示版本信息并退出
```

## 应用举例

显示所有信息

```
[root@centos7 ~]# vmstat
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 2  0      0 568632   2108 311348    0    0     7     1   50   38  2  1 98  0  0
#1秒刷新一次
[root@centos7 ~]# vmstat 1
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 2  0      0 568780   2108 311380    0    0     7     1   50   38  2  1 98  0  0
 0  0      0 568756   2108 311380    0    0     0     0   20   20  0  0 100  0  0
 0  0      0 568756   2108 311380    0    0     0     0   25   25  0  1 99  0  0
 0  0      0 568756   2108 311380    0    0     0     0   17   14  0  0 100  0  0
 0  0      0 568756   2108 311380    0    0     0     0   20   18  0  0 100  0  0
 0  0      0 568756   2108 311380    0    0     0     0   16   12  0  0 100  0  0
 0  0      0 568756   2108 311380    0    0     0     0   25   25  0  1 99  0  0
```

结果的字段说明

```
#Procs（进程）
r: 运行队列中进程数量
b: 等待IO的进程数量

#Memory（内存）
swpd: 使用虚拟内存大小
free: 空闲物理内存大小
buff: 用作缓冲的内存大小
cache: 用作缓存的内存大小

#Swap
si: 每秒从交换区写到内存的大小，由磁盘调入内存
so: 每秒写入交换区的内存大小，由内存调入磁盘
 
#IO（现在的Linux版本块的大小为1kb）
bi: 每秒读取的块数
bo: 每秒写入的块数
 
#system（系统）
in: 每秒中断数，包括时钟中断
cs: 每秒上下文切换数
 
#CPU（以百分比表示）
 
us: 用户进程执行时间百分比(user time),us的值比较高时，说明用户进程消耗的CPU时间多。
sy: 内核系统进程执行时间百分比(system time),sy的值高时，说明系统内核消耗的CPU资源多。
wa: IO等待时间百分比,wa的值高时，说明IO等待比较严重。
 
#id: 空闲时间百分比
```

显示系统启动后创建的进程数

```
[root@centos7 ~]# vmstat -f
         5303 forks
```

查看磁盘状态

```
[root@centos7 ~]# vmstat -d
disk- ------------reads------------ ------------writes----------- -----IO------
       total merged sectors      ms  total merged sectors      ms    cur    sec
fd0        0      0       0       0      0      0       0       0      0      0
sda     8001     12  603239   68687   1841    278   64871  192251      0     91
sdb       92      0    5184     563      0      0       0       0      0      0
sr0       18      0    2056     245      0      0       0       0      0      0
dm-0    5949      0  579134   67305   2115      0   60775  227833      0     91
dm-1      88      0    4408     154      0      0       0       0      0      0
```

显示指定磁盘分区的状态

```
[root@centos7 ~]# vmstat -p /dev/sda1
sda1          reads   read sectors  writes    requested writes
                1864      12369          4       4096
[root@centos7 ~]# vmstat -p /dev/sda2
sda2          reads   read sectors  writes    requested writes
                6107     587782       1846      60879
[root@centos7 ~]# vmstat -p /dev/sdb
partition was not found
```