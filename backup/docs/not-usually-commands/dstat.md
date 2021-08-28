## 命令简介

dstat 命令是一个用来替换 vmstat、iostat、netstat、nfsstat 和 ifstat 这些命令的工具，通用的系统资源统计工具，是一个全能系统信息统计工具。

```
[root@centos7 ~]# dstat
-bash: dstat: command not found
[root@centos7 ~]# yum install dstat -y
```

dstat特点

- 结合了vmstat，iostat，ifstat，netstat以及更多的信息
- 实时显示统计情况
- 在分析和排障时可以通过启用监控项并排序
- 模块化设计
- 使用python编写的，更方便扩展现有的工作任务
- 容易扩展和添加你的计数器（请为此做出贡献）
- 包含的许多扩展插件充分说明了增加新的监控项目是很方便的
- 可以分组统计块设备/网络设备，并给出总数
- 可以显示每台设备的当前状态
- 极准确的时间精度，即便是系统负荷较高也不会延迟显示
- 显示准确地单位和和限制转换误差范围
- 用不同的颜色显示不同的单位
- 显示中间结果延时小于1秒
- 支持输出CSV格式报表，并能导入到Gnumeric和Excel以生成图形

## 语法格式

```
dstat [-afv] [options..] [delay [count]]
```

## 选项说明

```
-c  #显示CPU系统占用，用户占用，空闲，等待，中断，软件中断等信息
-C  #可按需分别显示cpu状态
-d  #显示磁盘读写数据大小
-n  #显示网络状态
-N  #指定要显示的网卡
-l  #显示系统负载情况
-m  #显示内存使用情况
-g  #显示页面使用情况
-p  #显示进程状态
-s  #显示交换分区使用情况
-S  #类似D/N
-r  #I/O请求情况
-y  #系统状态
--ipc     #显示ipc消息队列，信号等信息
--socket  #用来显示tcp udp端口状态
--output 文件  #把状态信息以csv的格式重定向到指定的文件中
```

## 应用举例

```
[root@centos7 ~]# dstat
You did not select any stats, using -cdngy by default.
----total-cpu-usage---- -dsk/total- -net/total- ---paging-- ---system--
usr sys idl wai hiq siq| read  writ| recv  send|  in   out | int   csw 
  1   0  98   0   0   0|6268B 1784B|   0     0 |   0     0 |  44    39 
  0   0 100   0   0   0|   0     0 | 120B  842B|   0     0 |  50    68 
  0   0  99   1   0   0|   0     0 | 244B  362B|   0     0 |  53    61 
  1   1  98   0   0   0|   0    20k| 152B  362B|   0     0 |  54    55 
  1   0  99   0   0   0|   0     0 |  60B  362B|   0     0 |  42    54 
```

输出显示的信息，默认情况下分五个区域：

```
--total-cpu-usage--CPU使用率
usr  #用户空间的程序所占百分比
sys  #系统空间程序所占百分比
ide  #空闲百分比
wai  #等待磁盘I/O所消耗的百分比
hiq  #硬中断次数
siq  #软中断次数

--dsk/total--磁盘统计
read  #读总数
writ  #写总数

--net/total-- 网络统计
recv  #网络收包总数
send  #网络发包总数

--paging-内存分页统计
in  #pagein（换入）
out #page out（换出）

--system--系统信息
int  #中断次数
csw  #上下文切换
```

![图片](https://mmbiz.qpic.cn/mmbiz_gif/tuSaKc6SfPpfMiaEuTENjpKAwJicFV73zAqbb3tzriabMIXYCUtIHZkqhGU8OiblMjHqfPbZKkn2aoOwDxXicDVB53g/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

监控 swap，process，sockets，filesystem 并显示监控的时间

```
[root@centos7 ~]# dstat -tsp --socket --fs
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpfMiaEuTENjpKAwJicFV73zAQPZqwFIRxRxrBiaWwUg2kiaIStFpIEf40SSQGbItIhDt4AnJUQ1Pgoog/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)查看全部内存占用情况

```
[root@centos7 ~]# dstat -g -l -m -s --top-mem
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpfMiaEuTENjpKAwJicFV73zATiaJ6t8qDLqBphqRLRvIUdEtAOPfBXleXyl3jDpIYXtic5JDGJln2HAg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)查看 dstat 能使用的所有参数

```
[root@centos7 ~]# dstat --list
internal:
 aio, cpu, cpu24, disk, disk24, disk24old, epoch, fs, int, int24, io, ipc, load, lock, mem, 
 net, page, page24, proc, raw, socket, swap, swapold, sys, tcp, time, udp, unix, vm
/usr/share/dstat:
 battery, battery-remain, cpufreq, dbus, disk-tps, disk-util, dstat, dstat-cpu, dstat-ctxt, 
 dstat-mem, fan, freespace, gpfs, gpfs-ops, helloworld, innodb-buffer, innodb-io, innodb-ops, 
 lustre, memcache-hits, mysql-io, mysql-keys, mysql5-cmds, mysql5-conn, mysql5-io, 
 mysql5-keys, net-packets, nfs3, nfs3-ops, nfsd3, nfsd3-ops, ntp, postfix, power, proc-count, 
 qmail, rpc, rpcd, sendmail, snooze, squid, test, thermal, top-bio, top-bio-adv, 
 top-childwait, top-cpu, top-cpu-adv, top-cputime, top-cputime-avg, top-int, top-io, 
 top-io-adv, top-latency, top-latency-avg, top-mem, top-oom, utmp, vm-memctl, vmk-hba, 
 vmk-int, vmk-nic, vz-cpu, vz-io, vz-ubc, wifi
```

## dstat插件功能

```
-–disk-util    #显示某一时间磁盘的忙碌状况
-–freespace    #显示当前磁盘空间使用率
-–proc-count   #显示正在运行的程序数量
-–top-bio      #指出块I/O最大的进程
-–top-cpu      #图形化显示CPU占用最大的进程
-–top-io       #显示正常I/O最大的进程
-–top-mem      #显示占用最多内存的进程
```



![图片](https://mmbiz.qpic.cn/mmbiz_gif/tuSaKc6SfPpfMiaEuTENjpKAwJicFV73zA0VNKqqQSXGoKlhMd3icKsAbSNNqrVUUBFy01Kpg3zt7moZz8ZLusa1Q/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)