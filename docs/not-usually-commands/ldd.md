## 命令简介

ldd 命令打印程序和库的共享库依赖项。注意：ldd 不是一个可执行程序，而只是一个 Shell 脚本。

## 语法格式

```
ldd [OPTION]... FILE...
```

## 选项说明

```
--version  #打印指令版本号
-v  #打印所有相关信息
-u  #打印未使用的直接依赖
-d  #执行重定位和报告任何丢失的对象
-r  #执行数据对象和函数的重定位，并且报告任何丢失的对象和函数
--help  #显示帮助信息
```

## 应用举例

打印版本信息

```
[root@centos7 ~]# ldd --version
ldd (GNU libc) 2.17
Copyright (C) 2012 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
Written by Roland McGrath and Ulrich Drepper.
```

打印 /bin/bash 的共享库依赖项

```
[root@centos7 ~]# ldd /bin/bash
 linux-vdso.so.1 =>  (0x00007ffd15ca8000)
 libtinfo.so.5 => /lib64/libtinfo.so.5 (0x00007f7343eab000)
 libdl.so.2 => /lib64/libdl.so.2 (0x00007f7343ca7000)
 libc.so.6 => /lib64/libc.so.6 (0x00007f73438d9000)
 /lib64/ld-linux-x86-64.so.2 (0x00007f73440d5000)
```