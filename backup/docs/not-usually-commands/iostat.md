## 命令简介

iostat 命令用于统计系统IO状态信息。

## 语法格式

```
iostat [options]
```

## 选项说明

```
-c  #仅显示CPU使用情况
-d  #仅显示设备利用率
-k  #显示状态以千字节每秒为单位，而不使用块每秒
-m  #显示状态以兆字节每秒为单位
-p  #仅显示块设备和所有被使用的其他分区的状态
-t  #显示每个报告产生时的时间
-V  #显示版号并退出
-x  #显示扩展状态
```

## 应用举例

查看指定设备的IO状态信息

```
[root@centos7 ~]# iostat -x /dev/sda1
Linux 3.10.0-1127.18.2.el7.x86_64 (centos7)  03/28/2021  _x86_64_ (1 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           1.59    0.00    0.55    0.05    0.00   97.81

Device:         rrqm/s   wrqm/s     r/s     w/s    rkB/s    wkB/s avgrq-sz avgqu-sz   await r_await w_await  svctm  %util
sda1              0.00     0.00    0.04    0.00     0.15     0.05     8.82     0.00    1.07    0.73   63.50   1.02   0.00
```

结果字段说明

```
Device  #监测设备名称
rrqm/s  #每秒需要读取需求的数量
wrqm/s  #每秒需要写入需求的数量
r/s     #每秒实际读取需求的数量
w/s     #每秒实际写入需求的数量
rsec/s  #每秒读取区段的数量
wsec/s  #每秒写入区段的数量
rkB/s   #每秒实际读取的大小，单位为KB
wkB/s   #每秒实际写入的大小，单位为KB
avgrq-sz  #需求的平均大小区段
avgqu-sz  #需求的平均队列长度
await     #等待I/O平均的时间（milliseconds）
svctm     #I/O需求完成的平均时间
%util     #被I/O需求消耗的CPU百分比
```

系统整体IO状态信息

```
[root@centos7 ~]# iostat
Linux 3.10.0-1127.18.2.el7.x86_64 (centos7)  03/28/2021  _x86_64_ (1 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           1.58    0.00    0.55    0.05    0.00   97.82

Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
sda               0.25         7.39         1.84     316339      78930
sdb               0.00         0.06         0.00       2592          0
scd0              0.00         0.02         0.00       1028          0
dm-0              0.21         7.11         1.80     304267      76862
dm-1              0.00         0.05         0.00       2204          0
```

其它实例

```
#只显示CPU的IO状态
[root@centos7 ~]# iostat -c
Linux 3.10.0-1127.18.2.el7.x86_64 (centos7)  03/28/2021  _x86_64_ (1 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           1.58    0.00    0.55    0.05    0.00   97.82

#只显示设备的使用率状态
[root@centos7 ~]# iostat -d
Linux 3.10.0-1127.18.2.el7.x86_64 (centos7)  03/28/2021  _x86_64_ (1 CPU)

Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
sda               0.25         7.38         1.84     316339      78930
sdb               0.00         0.06         0.00       2592          0
scd0              0.00         0.02         0.00       1028          0
dm-0              0.21         7.09         1.79     304267      76862
dm-1              0.00         0.05         0.00       2204          0

#以千字节每秒为单位显示
[root@centos7 ~]# iostat -k
Linux 3.10.0-1127.18.2.el7.x86_64 (centos7)  03/28/2021  _x86_64_ (1 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           1.58    0.00    0.55    0.05    0.00   97.82

Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
sda               0.25         7.37         1.84     316339      78930
sdb               0.00         0.06         0.00       2592          0
scd0              0.00         0.02         0.00       1028          0
dm-0              0.21         7.09         1.79     304267      76862
dm-1              0.00         0.05         0.00       2204          0

#以兆字节每秒为单位
[root@centos7 ~]# iostat -m
Linux 3.10.0-1127.18.2.el7.x86_64 (centos7)  03/28/2021  _x86_64_ (1 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           1.58    0.00    0.55    0.05    0.00   97.82

Device:            tps    MB_read/s    MB_wrtn/s    MB_read    MB_wrtn
sda               0.25         0.01         0.00        308         77
sdb               0.00         0.00         0.00          2          0
scd0              0.00         0.00         0.00          1          0
dm-0              0.21         0.01         0.00        297         75
dm-1              0.00         0.00         0.00          2          0
```