## 命令简介

whereis 命令查找二进制程序、代码等相关文件路径。

但是，和 find 相比，whereis 查找的速度非常快，因为，Linux 会将系统里的所有文件统一记录在一个数据库文件中，当用户使用 whereis 命令时，它就会直接从这个数据库文件中去查找。而find命令则是遍历硬盘来进行查找，故而效率比不上 whereis 命令。

## 语法格式

```
whereis [ OPTIONS ] file name...
```

## 选项说明

```
-b  #只查找二进制文件
-B<目录>  #只在指定的目录下查找二进制文件
-f  #不显示文件名前的路径名称
-m  #只查找说明文件
-M<目录>  #只在指定的目录下查找说明文件
-s  #只查找原始代码文件
-S<目录>  #只在指定的目录下查找原始代码文件
-u  #查找不包含指定类型的文件
```

## 应用举例

```
#将相关的所有文件都查找出来
[root@centos7 ~]# whereis ifconfig
ifconfig: /usr/sbin/ifconfig /usr/share/man/man8/ifconfig.8.gz
[root@centos7 ~]# whereis top
top: /usr/bin/top /usr/share/man/man1/top.1.gz

#只将二进制文件查找出来
[root@centos7 ~]# whereis -b ifconfig
ifconfig: /usr/sbin/ifconfig
[root@centos7 ~]# whereis -b top
top: /usr/bin/top
```