## 命令简介

w 命令是一个非常常用的命令，用来查看登录者的信息及他们的行为动作、系统负载等信息。

## 语法格式

```
w [OPTIONS][用户名称]
```

## 选项说明

```
-f  #开启或关闭显示用户从何处登录到系统
-h  #不显示各栏位的标题信息列
-l  #使用详细格式列表（默认）
-s  #使用简洁格式列表
-u  #忽略执行程序的名称，以及该程序耗费CPU时间的信息
-V  #打印版本信息
```

## 应用举例

```
#显示当前用户及系统负载信息
[root@centos7 ~]# w
 08:48:55 up 1 day, 10:02,  2 users,  load average: 0.09, 0.04, 0.05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
root     pts/0    192.168.1.93     08:26   20:15   0.04s  0.04s -bash
root     pts/1    192.168.1.93     08:32    7.00s  0.25s  0.18s w

#不显示用户登录位置信息
[root@centos7 ~]# w -f
 08:48:58 up 1 day, 10:02,  2 users,  load average: 0.08, 0.04, 0.05
USER     TTY        LOGIN@   IDLE   JCPU   PCPU WHAT
root     pts/0     08:26   20:18   0.04s  0.04s -bash
root     pts/1     08:32    2.00s  0.08s  0.01s w -f

#以精简格式显示
[root@centos7 ~]# w -s
 08:49:12 up 1 day, 10:03,  2 users,  load average: 0.06, 0.04, 0.05
USER     TTY      FROM              IDLE WHAT
root     pts/0    192.168.1.93     20:32  -bash
root     pts/1    192.168.1.93      0.00s w -s

#不显示列的标题信息
[root@centos7 ~]# w -h
root     pts/0    192.168.1.93     08:26   20:36   0.04s  0.04s -bash
root     pts/1    192.168.1.93     08:32    4.00s  0.07s  0.00s w -h
```