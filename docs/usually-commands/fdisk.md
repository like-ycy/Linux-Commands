## 命令简介

fdisk 命令用于查看磁盘使用情况和磁盘分区，它可用于创建，删除和修改磁盘分区。

## 语法格式

```
disk [-uc] [-b sectorsize] [-C cyls] [-H heads] [-S sects] device
```

## 选项说明

```
-b <大小>      #扇区大小(512、1024、2048或4096)
-c[=<模式>]    #兼容模式：“dos”或“nondos”(默认)
-h            #打印此帮助文本
-u[=<单位>]    #显示单位：“cylinders”(柱面)或“sectors”(扇区，默认)
-v            #打印程序版本
-C <数字>      #指定柱面数
-H <数字>      #指定磁头数
-S <数字>      #指定每个磁道的扇区数
```

## 应用举例

选择要进行操作的磁盘

```
[root@localhost ~]$ fdisk /dev/sdb
```

输入 m 查看可执行的命令

```
command (m for help): m
Command action
   a   toggle a bootable flag
   b   edit bsd disklabel
   c   toggle the dos compatibility flag
   d   delete a partition
   l   list known partition types
   m   print this menu
   n   add a new partition
   o   create a new empty DOS partition table
   p   print the partition table
   q   quit without saving changes
   s   create a new empty Sun disklabel
   t   change a partition's system id
   u   change display/entry units
   v   verify the partition table
   w   write table to disk and exit
   x   extra functionality (experts only)
```

输入 p 列出磁盘目前的分区情况

```
Command (m for help): p
 
Disk /dev/sdb: 3221 MB, 3221225472 bytes
255 heads, 63 sectors/track, 391 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
 
   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1           1        8001   8e  Linux LVM
/dev/sdb2               2          26      200812+  83  Linux
```

输入 d 然后选择分区，删除现有分区

```
Command (m for help): d
Partition number (1-4): 1
 
Command (m for help): d
Selected partition 2
```

查看分区情况，确认分区已经删除

```
Command (m for help): print
 
Disk /dev/sdb: 3221 MB, 3221225472 bytes
255 heads, 63 sectors/track, 391 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
 
   Device Boot      Start         End      Blocks   Id  System
 
Command (m for help):
```

输入 n 建立新的磁盘分区，首先建立两个主磁盘分区

```
Command (m for help): n
Command action
   e   extended
   p   primary partition (1-4)
p    #建立主分区
Partition number (1-4): 1  #分区号
First cylinder (1-391, default 1):  #分区起始位置
Using default value 1
last cylinder or +size or +sizeM or +sizeK (1-391, default 391): 100  #分区结束位置，单位为扇区
 
Command (m for help): n  #再建立一个分区
Command action
   e   extended
   p   primary partition (1-4)
p 
Partition number (1-4): 2  #分区号为2
First cylinder (101-391, default 101):
Using default value 101
Last cylinder or +size or +sizeM or +sizeK (101-391, default 391): +200M  #分区结束位置，单位为M
```

确认分区建立成功

```
Command (m for help): p
 
Disk /dev/sdb: 3221 MB, 3221225472 bytes
255 heads, 63 sectors/track, 391 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
 
   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1         100      803218+  83  Linux
/dev/sdb2             101         125      200812+  83  Linux
```

再建立一个逻辑分区

```
Command (m for help): n
Command action
   e   extended
   p   primary partition (1-4)
e  #选择扩展分区
Partition number (1-4): 3
First cylinder (126-391, default 126):
Using default value 126
Last cylinder or +size or +sizeM or +sizeK (126-391, default 391):
Using default value 391
```

确认扩展分区建立成功

```
Command (m for help): p
 
Disk /dev/sdb: 3221 MB, 3221225472 bytes
255 heads, 63 sectors/track, 391 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
 
   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1         100      803218+  83  Linux
/dev/sdb2             101         125      200812+  83  Linux
/dev/sdb3             126         391     2136645    5  Extended
```

在扩展分区上建立两个逻辑分区

```
Command (m for help): n
Command action
   l   logical (5 or over)
   p   primary partition (1-4)
l  #选择逻辑分区
First cylinder (126-391, default 126):
Using default value 126
Last cylinder or +size or +sizeM or +sizeK (126-391, default 391): +400M    
 
Command (m for help): n
Command action
   l   logical (5 or over)
   p   primary partition (1-4)
l
First cylinder (176-391, default 176):
Using default value 176
Last cylinder or +size or +sizeM or +sizeK (176-391, default 391):
Using default value 391
```

确认逻辑分区建立成功

```
Command (m for help): p
 
Disk /dev/sdb: 3221 MB, 3221225472 bytes
255 heads, 63 sectors/track, 391 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
 
   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1         100      803218+  83  Linux
/dev/sdb2             101         125      200812+  83  Linux
/dev/sdb3             126         391     2136645    5  Extended
/dev/sdb5             126         175      401593+  83  Linux
/dev/sdb6             176         391     1734988+  83  Linux
 
Command (m for help):
```

保存操作信息

```
Command (m for help): w
The partition table has been altered!
 
Calling ioctl() to re-read partition table.
Syncing disks.
```

建立好分区之后我们还需要对分区进行格式化才能在系统中使用磁盘。

