## 命令简介

mount 命令用于挂载设备或文件系统。

## 语法格式

```
mount [option] device|dir 
```

## 选项说明

```
-V   #显示版本信息
-h   #显示帮助信息
-v   #通常和 -f 用来除错
-a   #将 /etc/fstab 中定义的所有档案系统挂上
-F   #这个命令通常和 -a 一起使用，它会为每一个 mount 的动作产生一个行程负责执行在系统需要挂上大量 NFS 档案系统时可以加快挂上的动作
-f  #用于日常排错
-s -r #功能与 -o ro相同
-w  #功能与 -o rw相同
-L  #将含有特定标签的硬盘分割挂上
-t  #指定档案系统的型态
-oasync  #打开非同步模式
-o sync  #在同步模式下执行
-o auto、-o noauto  #打开/关闭自动模式
-o ro  #使用只读模式挂载
-o rw  #使用可读写模式挂载
```

## 应用举例

将 /dev/hda1 挂载到 /mnt 目录下

```
[root@centos7 ~]# mount /dev/hda1 /mnt
```

将 /dev/hda1 用只读模式挂载到 /mnt 目录下

```
[root@centos7 ~]# mount -o ro /dev/hda1 /mnt
```

列出当前所有挂载的文件系统

```
[root@centos7 ~]# mount
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
devtmpfs on /dev type devtmpfs (rw,nosuid,size=486068k,nr_inodes=121517,mode=755)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,mode=755)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,mode=755)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/usr/lib/systemd/systemd-cgroups-agent,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,hugetlb)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,net_prio,net_cls)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpuacct,cpu)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,pids)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
configfs on /sys/kernel/config type configfs (rw,relatime)
/dev/mapper/centos-root on / type xfs (rw,relatime,attr2,inode64,noquota)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=32,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=13688)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime)
mqueue on /dev/mqueue type mqueue (rw,relatime)
/dev/sda1 on /boot type xfs (rw,relatime,attr2,inode64,noquota)
tmpfs on /run/user/0 type tmpfs (rw,nosuid,nodev,relatime,size=99572k,mode=700)
```

查找指定文件类型的挂载信息

```
[root@centos7 ~]# mount -l -t tmpfs
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)
tmpfs on /run type tmpfs (rw,nosuid,nodev,mode=755)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,mode=755)
tmpfs on /run/user/0 type tmpfs (rw,nosuid,nodev,relatime,size=99572k,mode=700)
[root@centos7 ~]# mount -l -t xfs
/dev/mapper/centos-root on / type xfs (rw,relatime,attr2,inode64,noquota)
/dev/sda1 on /boot type xfs (rw,relatime,attr2,inode64,noquota)
[root@centos7 ~]# mount -l -t devpts
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
```

## 命令简介

umount 命令用于卸载已经挂载的文件系统。请注意，文件系统在繁忙时无法卸载，例如，当文件系统上有打开的文件，某个进程的工作目录位于其中或正在使用交换文件时。

## 语法格式

```
umount -a [-dflnrv] [-t vfstype] [-O options]
```

## 选项说明

```
-a  #卸载/etc/mtab中记录的所有文件系统
-h  #显示帮助
-n  #卸载时不要将信息存入/etc/mtab文件中
-r  #若无法成功卸载，则尝试以只读的方式重新挂入文件系统
-t<文件系统类型>  #卸载指定的文件系统
-v  #显示执行时的详细信息
-V  #显示版本信息
```

## 应用举例

```
#通过设备名卸载
[root@centos7 ~]# umount -v /dev/sda1
/dev/sda1 umounted
 
#通过挂载点卸载
[root@centos7 ~]# umount -v /opt/dev_mount/
/iso/system-1.0.0.iso umounted
```

卸载文件系统（正在运行中的文件系统）

```
[root@centos7 ~]# umount -v /opt/dev_mount/
umount: /opt/dev_mount/: device is busy

[root@centos7 ~]# lsof | grep dev_mount    #查找打开的文件
bash   4147  francois  cwd   DIR   5,1   1024   3  /opt/dev_mount/
```