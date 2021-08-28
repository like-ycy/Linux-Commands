## 命令简介

fping 命令是 ping 命令的加强版，它可以同时 ping 多台主机（网段）。

系统默认是没有安装，需要用户在使用前手动安装。

```
[root@centos7 ~]# fping
-bash: fping: command not found
[root@centos7 ~]# yum install fping -y
```

## 语法格式

```
 fping [options] [targets...]
```

## 选项说明

```
-a  #显示存活的主机
-b  #ping 数据包的大小（默认为56）
-c  #ping每个目标的次数 (默认为1)
-f  #从文件获取目标列表(不能与-g同时使用)
-l  #循环向指定目标发送 ping
-g  #通过指定开始和结束地址来生成目标列表
-u  #打印不可达的目标主机
```

## 应用举例

同时fping多个指定的地址

```
[root@centos7 ~]# fping 192.168.1.1 192.168.1.79 192.168.1.199
192.168.1.1 is alive
192.168.1.79 is alive
192.168.1.199 is alive
[root@centos7 ~]# fping 192.168.1.1 192.168.1.79 192.168.1.199 192.168.1.100
192.168.1.1 is alive
192.168.1.79 is alive
192.168.1.199 is alive
192.168.1.100 is unreachable
```

fping整个网段地址

```
[root@centos7 ~]# fping -g 192.168.1.0/24 2>/dev/null
192.168.1.1 is alive
192.168.1.10 is alive
192.168.1.79 is alive
192.168.1.81 is alive
192.168.1.93 is alive
192.168.1.199 is alive
192.168.1.2 is unreachable
192.168.1.3 is unreachable
.........
192.168.1.249 is unreachable
192.168.1.250 is unreachable
192.168.1.251 is unreachable
192.168.1.252 is unreachable
192.168.1.253 is unreachable
192.168.1.254 is unreachable

2>/dev/null #减少信息输出，直接显示结果
```

fping网段，但只显示活动主机

```
[root@centos7 ~]# fping -ag 192.168.1.0/24 2>/dev/null
192.168.1.1
192.168.1.10
192.168.1.79
192.168.1.81
192.168.1.93
192.168.1.199
```

fping指定的区间段

```
[root@centos7 ~]# fping -ag 192.168.1.90  192.168.1.100 2>/dev/null
192.168.1.93
```

fping 整体类似于 ping 命令，但比它强大，不需要等待对方主机返回相关的信息，只需将数据包完整的发送给某个主机后，就可以直接将数据发送给下一个主机，从而实时多主机同时ping的功能，使用也非常简单，功能确实强大不少。