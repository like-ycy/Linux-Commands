## 命令简介

mkfs 命令用于格式化创建Linux文件系统。通常用于在设备（通常是硬盘分区）上构建 Linux 文件系统。

## 语法格式

```
mkfs [options] [-t type fs-options] device [size]
```

## 选项说明

```
fs  #指定建立文件系统时的参数
-t<文件系统类型>  #指定要建立何种文件系统
  fs-options     #使用的文件系统
  <device>       #使用的设备路径
  <size>         #使用的设备块数
  #文件系统：指定要创建的文件系统对应的设备文件名
  #块数：指定文件系统的磁盘块数
  
-V  #输出详细信息（--verbose）
-V  #显示版本信息（--version）
-c  #检查该partition是否有坏道
-h  #显示帮助并退出
```

## 应用举例

格式化磁盘

```
[root@centos7 ~]# mkfs.ext4 /dev/sdb
mke2fs 1.42.9 (28-Dec-2013)
/dev/sdb is entire device, not just one partition!
Proceed anyway? (y,n) y
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
655360 inodes, 2621440 blocks
131072 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=2151677952
80 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks: 
 32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (32768 blocks): 
done
```