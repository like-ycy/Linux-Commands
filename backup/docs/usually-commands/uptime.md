## 命令简介

uptime命令用于显示系统运行时间及负载。

uptime 命令可以打印出系统总共运行了多长时间和系统的平均负载。uptime 命令显示的信息显示依次为：现在时间、系统已经运行了多长时间、目前有多少登陆用户、系统在过去的 1 分钟、5 分钟和 15 分钟内的平均负载。

```
[root@centos7 ~]# uptime
 19:48:14 up 21:02,  1 user,  load average: 0.00, 0.01, 0.05
```

## 命令语法

```
uptime [options]
```

## 选项说明

```
-p #以好看的格式显示正常运行时间
-s #自系统启动来的时间
-h #打印帮助信息
-V #打印版本信息。
```

## 应用举例

```
[root@centos7 ~]# uptime -V
uptime from procps-ng 3.3.10

[root@centos7 ~]# uptime 
 19:50:29 up 21:04,  1 user,  load average: 0.03, 0.03, 0.05
 
[root@centos7 ~]# uptime -p
up 21 hours, 4 minutes

[root@centos7 ~]# uptime -s
2021-01-15 22:46:06

[root@centos7 ~]# uptime -h

Usage:
 uptime [options]

Options:
 -p, --pretty   show uptime in pretty format
 -h, --help     display this help and exit
 -s, --since    system up since
 -V, --version  output version information and exit

For more details see uptime(1).
```

文件存放目录

```
/var/run/utmp #当前登录者的信息
[root@centos7 ~]# cat /var/run/utmp
~~~reboot3.10.0-1127.18.2.el7.x86_64󞞗/vtty1tty1LOGINv `S3~~~runlevel3.10.0-1127.18.2.el7.x86_64 `pts/0ts/0root192.168.1.93󂠻(]
```