## 命令简介

ioping 命令是一个用于实时显示磁盘 io 延时的工具，以类似 ping 的输出一样来显示输出结果。

默认没有安装，需要用户在使用前手动安装。

```
[root@centos7 ~]# ioping
-bash: ioping: command not found
[root@centos7 ~]# yum install ioping -y
[root@centos7 ~]# ioping -v
ioping 1.1
```

## 语法格式

```
ioping [-ABCDRLWYykq] [-c count] [-i interval] [-s size] [-S wsize]
       [-o offset] [-w deadline] [-pP period] directory|file|device
```

## 选项说明

```
-c count      #计数请求后停止
-i interval   #将两次请求之间的时间间隔设置为（1s）
-l speed      #将间隔设置为请求大小/速度
-t time       #最小有效请求时间（0us）
-T time       #最大有效请求时间
-s size       #要求大小（4k）
-S wsize      #工作集大小
-o offset     #文件/设备中的起始偏移量（0）
-w deadline   #在截止时间之后停止
-p period     #打印每个期间请求的原始统计信息
-P period     #打印每个时间段的原始统计信息
-A            #使用异步I/O
-B            #批处理模式
-C            #使用缓存的I/O
-D            #使用直接I/O（
-L            #使用顺序操作
-R            #磁盘搜寻率测试
-W            #使用写而不是读
-G            #备用读写请求。
-Y            #使用同步I/O
-y            #使用数据同步I/O
-k            #使用临时工作文件“ ioping.tmp”
-q            #禁用人类可读的定期输出
-H            #显示帮助消息并退出
-v            #显示版本并退出
```

## 应用举例

使用20个数据包，每个1M大小，用来测试/opt上的延时

```
[root@centos7 ~]# ioping -c 20 -s 1M /opt
1 MiB <<< /opt (xfs /dev/dm-0): request=1 time=8.46 ms (warmup)
1 MiB <<< /opt (xfs /dev/dm-0): request=2 time=4.51 ms
1 MiB <<< /opt (xfs /dev/dm-0): request=3 time=3.63 ms
1 MiB <<< /opt (xfs /dev/dm-0): request=4 time=4.33 ms
1 MiB <<< /opt (xfs /dev/dm-0): request=5 time=3.44 ms
1 MiB <<< /opt (xfs /dev/dm-0): request=6 time=5.72 ms
1 MiB <<< /opt (xfs /dev/dm-0): request=7 time=3.46 ms (fast)
1 MiB <<< /opt (xfs /dev/dm-0): request=8 time=4.85 ms
1 MiB <<< /opt (xfs /dev/dm-0): request=9 time=3.71 ms
1 MiB <<< /opt (xfs /dev/dm-0): request=10 time=5.21 ms
1 MiB <<< /opt (xfs /dev/dm-0): request=11 time=3.53 ms (fast)
1 MiB <<< /opt (xfs /dev/dm-0): request=12 time=3.41 ms (fast)
1 MiB <<< /opt (xfs /dev/dm-0): request=13 time=3.44 ms (fast)
1 MiB <<< /opt (xfs /dev/dm-0): request=14 time=4.16 ms
1 MiB <<< /opt (xfs /dev/dm-0): request=15 time=3.86 ms
1 MiB <<< /opt (xfs /dev/dm-0): request=16 time=3.75 ms
1 MiB <<< /opt (xfs /dev/dm-0): request=17 time=220.9 ms (slow)
1 MiB <<< /opt (xfs /dev/dm-0): request=18 time=230.9 ms (slow)
1 MiB <<< /opt (xfs /dev/dm-0): request=19 time=3.65 ms (fast)
1 MiB <<< /opt (xfs /dev/dm-0): request=20 time=3.51 ms (fast)

--- /opt (xfs /dev/dm-0) ioping statistics ---
19 requests completed in 519.9 ms, 19 MiB read, 36 iops, 36.5 MiB/s
generated 20 requests in 19.0 s, 20 MiB, 1 iops, 1.05 MiB/s
min/avg/max/mdev = 3.41 ms / 27.4 ms / 230.9 ms / 68.1 ms
```

测试系统磁盘查找效率

```
[root@centos7 ~]# ioping -R /opt

--- /opt (xfs /dev/dm-0) ioping statistics ---
5.15 k requests completed in 2.97 s, 20.1 MiB read, 1.73 k iops, 6.77 MiB/s
generated 5.15 k requests in 3.00 s, 20.1 MiB, 1.72 k iops, 6.70 MiB/s
min/avg/max/mdev = 284.9 us / 577.4 us / 243.3 ms / 4.50 ms
[root@centos7 ~]# ioping -R download/

--- download/ (xfs /dev/dm-0) ioping statistics ---
2.73 k requests completed in 2.97 s, 10.7 MiB read, 920 iops, 3.60 MiB/s
generated 2.73 k requests in 3.00 s, 10.7 MiB, 911 iops, 3.56 MiB/s
min/avg/max/mdev = 296.3 us / 1.09 ms / 76.3 ms / 2.60 ms
```

raw 统计

```
[root@centos7 ~]# ioping -p 50 -c 10 -i 0  /opt
4 KiB <<< /opt (xfs /dev/dm-0): request=1 time=665.7 us (warmup)
4 KiB <<< /opt (xfs /dev/dm-0): request=2 time=655.7 us
4 KiB <<< /opt (xfs /dev/dm-0): request=3 time=391.7 us
4 KiB <<< /opt (xfs /dev/dm-0): request=4 time=516.1 us
4 KiB <<< /opt (xfs /dev/dm-0): request=5 time=682.5 us
4 KiB <<< /opt (xfs /dev/dm-0): request=6 time=782.4 us
4 KiB <<< /opt (xfs /dev/dm-0): request=7 time=771.7 us (slow)
4 KiB <<< /opt (xfs /dev/dm-0): request=8 time=695.6 us
4 KiB <<< /opt (xfs /dev/dm-0): request=9 time=567.0 us
4 KiB <<< /opt (xfs /dev/dm-0): request=10 time=551.7 us

--- /opt (xfs /dev/dm-0) ioping statistics ---
9 requests completed in 5.61 ms, 36 KiB read, 1.60 k iops, 6.26 MiB/s
generated 10 requests in 6.52 ms, 40 KiB, 1.53 k iops, 5.99 MiB/s
min/avg/max/mdev = 391.7 us / 623.8 us / 782.4 us / 120.4 us
```