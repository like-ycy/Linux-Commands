## 命令简介

mpstat（Multi-Processor Statistics） 命令用于显示各个可用CPU的状态统计。是一个实时监控工具，与vmstat类似，但只能监控CPU的整体性能状态。

```
[root@centos7 ~]# mpstat
-bash: mpstat: command not found
[root@centos7 ~]# yum install sysstat -y
```

## 语法格式

```
mpstat [ options ]
```

## 选项说明

```
-P  #指定CPU编号
```

## 应用举例

列出端口

```
[root@centos7 ~]# mpstat
Linux 3.10.0-1127.18.2.el7.x86_64 (centos7)  03/28/2021  _x86_64_ (1 CPU)

11:14:29 AM  CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle
11:14:29 AM  all    1.61    0.00    0.48    0.05    0.00    0.07    0.00    0.00    0.00   97.79
```

字段说明

```
%user      
#在internal时间段里，用户态的CPU时间(%)，不包含nice值为负进程  (usr/total)*100
%nice      
#在internal时间段里，nice值为负进程的CPU时间(%)(nice/total)*100
%sys       
#在internal时间段里，内核时间(%)(system/total)*100
%iowait    
#在internal时间段里，硬盘IO等待时间(%) (iowait/total)*100
%irq         
#在internal时间段里，硬中断时间(%)(irq/total)*100
%soft       
#在internal时间段里，软中断时间(%)(softirq/total)*100
%idle       
#在internal时间段里，CPU除去等待磁盘IO操作外的因为任何原因而空闲的时间闲置时间(%) (idle/total)*100
```