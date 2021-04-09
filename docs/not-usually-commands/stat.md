## 命令简介

stat 命令用于显示文件或文件系统的状态。

## 命令语法

```
stat [OPTION]... FILE...
```

文件：指定要显示信息的普通文件或者文件系统对应的设备文件名

## 选项说明

```
-L  #支持符号连接
-f  #显示文件系统状态而非文件状态
-t  #以简洁方式输出信息
-c  #使用指定的格式而不是默认格式
-Z  #打印 SELinux 安全上下文
--help  #打印帮助信息
--version  #打印的版本信息
```

## 应用举例

查看文件test.txt详细信息

```
[root@centos7 ~]# stat test.txt
  File: ‘test.txt’
  Size: 140        Blocks: 8          IO Block: 4096   regular file
Device: fd00h/64768d Inode: 33575001    Links: 1
Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2021-01-16 11:34:32.000000000 -0500
Modify: 2021-01-16 11:32:55.000000000 -0500
Change: 2021-01-16 11:38:17.157156882 -0500
 Birth: -
 
[root@centos7 ~]# stat -f test.txt
  File: "test.txt"
    ID: fd0000000000 Namelen: 255     Type: xfs
Block size: 4096       Fundamental block size: 4096
Blocks: Total: 4452864    Free: 3984106    Available: 3984106
Inodes: Total: 8910848    Free: 8860529

[root@centos7 ~]# stat -t test.txt
test.txt 140 8 81a4 0 0 fd00 33575001 1 0 0 1610814872 1610814775 1610815097 0 4096
```

获取文件权限的数字

```
[root@centos7 ~]# stat test.txt |awk 'NR==4' |awk -F '[(0/]' '{print $3}'
644
[root@centos7 ~]# stat test.txt |awk 'NR==4' |cut -c 11-13 
644
[root@centos7 ~]# stat test.txt |sed -n '4p' |cut -c 11-13 
644
[root@centos7 ~]# stat -c %a test.txt
644
```

文件有效格式说明

```
The valid format sequences for files (without --file-system):

  %a   #显示8进制访问权限
  %A   #可读格式的访问权限
  %b   #可分配的块数
  %B   #每个块的字节大小
  %C   #SELinux安全上下文字符串
  %d   #设备编号（十进制）
  %D   #设备编号（十六进制）
  %f   #文件类型（十六进制）
  %F   #文件类型
  %g   #所有者的组ID
  %G   #所有者的组名
  %h   #硬链接数
  %i   #inode号
  %m   #挂载点
  %n   #文件名
  %N   #带引号的文件名，如果有软链接则取消引用
  %o   #IO块大小
  %s   #总大小（以字节为单位）
  %t   #十六进制的主要设备类型
  %T   #次设备类型（十六进制）
  %u   #所有者的用户ID
  %U   #所有者的用户
  %x   #最后访问时间
  %X   #最后访问时间（以秒为单位）
  %y   #最后修改时间
  %Y   #最后修改时间（以秒为单位）
  %z   #最后更改时间
  %Z   #最后更改时间（以秒为单位）
```

文件系统有效格式说明：

```
Valid format sequences for file systems:

  %a   #非超级用户可用的空闲块
  %b   #文件系统中的数据块总数
  %c   #文件系统中的文件节点总数
  %d   #文件系统中的空闲文件节点
  %f   #文件系统中的空闲块
  %i   #十六进制文件系统ID
  %l   #文件名的最大长度
  %n   #文件名
  %s   #最佳传输块大小
  %t   #十六进制的形式输入
  %T   #以易读的形式输入
[root@centos7 ~]# stat -f /dev/sda
  File: "/dev/sda"
    ID: 0        Namelen: 255     Type: tmpfs
Block size: 4096       Fundamental block size: 4096
Blocks: Total: 121517     Free: 121517     Available: 121517
Inodes: Total: 121517     Free: 121132
```