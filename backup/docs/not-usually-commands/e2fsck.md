## 命令简介

e2fsck 命令用于检查 ext2/ext3/ext4 类型文件系统。

## 语法格式

```
e2fsck [-panyrcdfvtDFV] [-b superblock] [-B blocksize]
  [-I inode_buffer_blocks] [-P process_inode_size]
  [-l|-L bad_blocks_file] [-C fd] [-j external_journal]
  [-E extended-options] device
```

## 选项说明

```
-d     #显示debug排错信息
-t     #显示时间信息
-p      #不提示，自动修复文件系统
-n      #以只读模式开启文件系统
-y      #采取非互动方式执行，所有提示都以"yes"确认
-c      #执行badblocks，把损坏的区块标记出来
-f      #强制检查
-v      #显示详细信息
-b superblock        #设定 superblock 位置
-B blocksize         #指定区块的大小，单位为字节
-j external_journal  #设置在哪里可以找到这个文件系统的外部日志的路径名
-l bad_blocks_file   #将文件中指定的区块加到损坏区块列表
-L bad_blocks_file   #先清除损坏区块列表，再将文件中指定的区块加到损坏区块列表
-C<文件描述符>        #将检查过程的信息完整记录在 file descriptor 中，使得整个检查过程都能完整监控。
```

e2fsck 命令执行后返回值及意义如下

```
0   #没有任何错误发生
1   #文件系统发生错误，并且已经修正
2   #文件系统发生错误，并且已经修正
4   #文件系统发生错误，但没有修正
8   #运作时发生错误
16  #使用的语法发生错误
128 #共享的函数库发生错误
```

## 应用举例

检查磁盘分区/dev/sdb 的文件系统

```
[root@centos7 ~]# e2fsck /dev/sdb
e2fsck 1.42.9 (28-Dec-2013)
/dev/sdb: clean, 11/655360 files, 83137/2621440 blocks
```

检查磁盘分区/dev/sdb 的文件系统，自动修复文件系统

```
[root@centos7 ~]# e2fsck -p /dev/sdb
```