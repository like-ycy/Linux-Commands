## 命令简介

df 命令用于显示磁盘的相关信息。df（Disk Free）的首字母组合，用来显示文件系统磁盘空间的使用情况。

默认显示单位为KB。可以使用 df 命令来查看硬盘被占用了多少空间，目前还剩下多少空间。

## 命令语法

```
df [OPTION]... [FILE]...
```

## 选项说明

```
-a  #包括所有的文件系统
--block-size=<区块大小>  #以指定的区块大小来显示区块数目
-h  #以可读的方式显示信息
-i  #查看inode的信息
-k  #指定区块大小为1024字节
-l  #仅显示本地端的文件系统
-m  #指定区块大小为1048576字节
--no-sync  #在获取磁盘使用信息前，不要执行sync指令
-P  #使用POSIX的输出格式
--sync  #在获取磁盘使用信息前，先执行sync指令
-t<文件系统类型>或--type=<文件系统类型>  #仅显示指定文件系统类型的磁盘信息
-T  #查看文件系统的类型
--help  #打印帮助信息
--version  #打印版本信息
```

## 应用举例

查看整个文件系统磁盘空间使用情况

```
[root@centos7 ~]# df
Filesystem              1K-blocks    Used Available Use% Mounted on
devtmpfs                   486068       0    486068   0% /dev
tmpfs                      497840       0    497840   0% /dev/shm
tmpfs                      497840    7784    490056   2% /run
tmpfs                      497840       0    497840   0% /sys/fs/cgroup
/dev/mapper/centos-root  17811456 1875036  15936420  11% /
/dev/sda1                 1038336  170064    868272  17% /boot
tmpfs                       99572       0     99572   0% /run/user/0

Filesystem  #Linux 系统中的文件系统
1K-blocks   #文件系统的大小，用 1K 大小的块来表示
Used        #以1K大小的块所表示的已使用数量
Available   #以1K大小的块所表示的可用空间的数量
Use%        #文件系统中已使用的百分比
Mounted on  #文件系统的挂载点
```

以更可读的方式查看文件系统磁盘空间使用情况

```
[root@centos7 ~]# df -h
Filesystem               Size  Used Avail Use% Mounted on
devtmpfs                 475M     0  475M   0% /dev
tmpfs                    487M     0  487M   0% /dev/shm
tmpfs                    487M  7.7M  479M   2% /run
tmpfs                    487M     0  487M   0% /sys/fs/cgroup
/dev/mapper/centos-root   17G  1.8G   16G  11% /
/dev/sda1               1014M  167M  848M  17% /boot
tmpfs                     98M     0   98M   0% /run/user/0
```

以MB为单位显示

```
[root@centos7 ~]# df -m
Filesystem              1M-blocks  Used Available Use% Mounted on
devtmpfs                      475     0       475   0% /dev
tmpfs                         487     0       487   0% /dev/shm
tmpfs                         487     8       479   2% /run
tmpfs                         487     0       487   0% /sys/fs/cgroup
/dev/mapper/centos-root     17394  1832     15563  11% /
/dev/sda1                    1014   167       848  17% /boot
tmpfs                          98     0        98   0% /run/user/0
```

显示inode的信息

```
[root@centos7 ~]# df -i
Filesystem               Inodes IUsed   IFree IUse% Mounted on
devtmpfs                 121517   385  121132    1% /dev
tmpfs                    124460     1  124459    1% /dev/shm
tmpfs                    124460   726  123734    1% /run
tmpfs                    124460    16  124444    1% /sys/fs/cgroup
/dev/mapper/centos-root 8910848 50320 8860528    1% /
/dev/sda1                524288   332  523956    1% /boot
tmpfs                    124460     1  124459    1% /run/user/0
```

显示文件系统类型

```
[root@centos7 ~]# df -T
Filesystem              Type     1K-blocks    Used Available Use% Mounted on
devtmpfs                devtmpfs    486068       0    486068   0% /dev
tmpfs                   tmpfs       497840       0    497840   0% /dev/shm
tmpfs                   tmpfs       497840    7784    490056   2% /run
tmpfs                   tmpfs       497840       0    497840   0% /sys/fs/cgroup
/dev/mapper/centos-root xfs       17811456 1875036  15936420  11% /
/dev/sda1               xfs        1038336  170064    868272  17% /boot
tmpfs                   tmpfs        99572       0     99572   0% /run/user/0
```

显示指定文件系统类型的信息

```
[root@centos7 ~]# df -t xfs
Filesystem              1K-blocks    Used Available Use% Mounted on
/dev/mapper/centos-root  17811456 1875036  15936420  11% /
/dev/sda1                 1038336  170064    868272  17% /boot
```

排除指定文件系统，再显示其它文件系统的信息

```
[root@centos7 ~]# df -x xfs
Filesystem     1K-blocks  Used Available Use% Mounted on
devtmpfs          486068     0    486068   0% /dev
tmpfs             497840     0    497840   0% /dev/shm
tmpfs             497840  7784    490056   2% /run
tmpfs             497840     0    497840   0% /sys/fs/cgroup
tmpfs              99572     0     99572   0% /run/user/0
```