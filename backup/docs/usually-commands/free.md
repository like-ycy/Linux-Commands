## 命令简介

free 命令用于显示内存的使用情况，显示可用和已用物理内存和交换内存的总数，以及内核使用的缓冲区。

## 语法格式

```
free [options]
```

## 选项说明

```
-b #以Byte为单位显示内存使用情况
-k #以KB为单位显示内存使用情况
-m #以MB为单位显示内存使用情况
-g #以GB为单位显示内存使用情况
-o #不显示缓冲区调节列
-s<间隔秒数> #持续观察内存使用状况
-t #显示内存总和列
-V #显示版本信息
```

## 应用举例

查看内存使用的总和

```
[root@centos7 ~]# free -t
              total        used        free      shared  buff/cache   available
Mem:         995684      124784      473344        7784      397556      698328
Swap:       2097148           0     2097148
Total:      3092832      124784     2570492
```

周期性打印出内存使用信息

```
[root@centos7 ~]# free -s 10
              total        used        free      shared  buff/cache   available
Mem:         995684      124780      473344        7784      397560      698332
Swap:       2097148           0     2097148

              total        used        free      shared  buff/cache   available
Mem:         995684      124780      473344        7784      397560      698332
Swap:       2097148           0     2097148

              total        used        free      shared  buff/cache   available
Mem:         995684      124780      473344        7784      397560      698332
Swap:       2097148           0     2097148

              total        used        free      shared  buff/cache   available
Mem:         995684      124780      473344        7784      397560      698332
Swap:       2097148           0     2097148
```

显示内存使用情况

```
[root@centos7 ~]# free -m
              total        used        free      shared  buff/cache   available
Mem:            972         121         462           7         388         682
Swap:          2047           0        2047

结果信息详细说明如下：
total #内存总和
used  #已经使用的内存
free  #空闲的内存
shared  #当前已经废弃不用
Buffer/cache  #缓存内存数
available     #实际可用内存数
```

Linux 在内存管理方面做的非常的好，系统在运行一段时间后，会将暂时用不到的内存转为 buff/cache，这样在程序使用到这一部分数据时，能够很快的取出，从而提高系统的运行效率。如果你看到服务器内存剩余的非常少，不必担心，真正剩余的内存是 free+buff/cache的和才是实际可用的内存。如果应用程序需要内存空间时，Linux 会将缓存让出给程序使用，从而使内存达到最大化的利用率。

当大量的缓存占用内存空间时，应用程序就会使用到sawp交换分区，这样会使得系统的运行变慢，从而影响整体运行效率。

所以，这个时候我们需要手动去释放内存，释放内存的时候，首先执行命令 sync 将所有正在内存中的缓冲区写到磁盘中，其中包括已经修改的文件 inode、已延迟的块 I/O 以及读写映射文件，从而确保文件系统的完整性。

```
sync
 
echo 1 > /proc/sys/vm/drop_caches
 
echo 0 > /proc/sys/vm/drop_caches
```

Swap 是指交换分区，当可用内存少于额定值的时候，就会开会进行交换。额定值信息如下

```
[root@centos7 ~]# cat /proc/meminfo
MemTotal:         995684 kB
MemFree:          473460 kB
MemAvailable:     698452 kB
Buffers:            2108 kB
Cached:           321280 kB
SwapCached:            0 kB
Active:           229996 kB
Inactive:         132264 kB
Active(anon):      39304 kB
Inactive(anon):     7352 kB
Active(file):     190692 kB
Inactive(file):   124912 kB
Unevictable:           0 kB
Mlocked:               0 kB
SwapTotal:       2097148 kB
SwapFree:        2097148 kB
Dirty:                 0 kB
Writeback:             0 kB
AnonPages:         38904 kB
Mapped:            20988 kB
Shmem:              7784 kB
Slab:              99432 kB
SReclaimable:      74176 kB
SUnreclaim:        25256 kB
KernelStack:        3728 kB
PageTables:         3280 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:     2594988 kB
Committed_AS:     230116 kB
VmallocTotal:   34359738367 kB
VmallocUsed:      177420 kB
VmallocChunk:   34359310332 kB
Percpu:            22528 kB
HardwareCorrupted:     0 kB
AnonHugePages:      8192 kB
CmaTotal:              0 kB
CmaFree:               0 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
DirectMap4k:       69504 kB
DirectMap2M:      978944 kB
DirectMap1G:           0 kB
```