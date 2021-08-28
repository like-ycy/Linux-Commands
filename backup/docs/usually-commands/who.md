## 命令简介

who 命令用于显示目前登录系统的用户信息。

who 命令用于显示当前系统登录的所有用户的信息，可以查看目前有那些用户登录到系统等信息。单独执行 who 命令时可以打印出登录的帐号，用户所使用的终端，登录时间以及从何处登录或正在使用哪些显示器等信息。

## 语法格式

```
who [ OPTION ]... [ FILE ] [ am i ]
```

## 选项说明

```
-a  #与使用选项-b -d --login -p -r -t -T -u相同。
-b  #显示上次系统引导的时间
-d  #显示无效进程
-H  #显示各栏位的标题信息列
-i  #显示闲置时间
-m  #此参数和指定"am i"字符串相同
-q  #只显示登入系统的帐号名称和总人数
-w  #显示用户的信息状态栏
--help  #打印在线帮助
--version  #显示版本信息
```

## 应用举例

```
[root@centos7 ~]# who
root     pts/0        2021-01-17 08:26 (192.168.1.93)
root     pts/1        2021-01-17 08:32 (192.168.1.93)
[root@centos7 ~]# who -b
         system boot  2021-01-14 05:41
[root@centos7 ~]# who -d
[root@centos7 ~]# who -m
root     pts/1        2021-01-17 08:32 (192.168.1.93)
[root@centos7 ~]# who -q
root root
# users=2
[root@centos7 ~]# who -aH
NAME       LINE         TIME             IDLE          PID COMMENT  EXIT
           system boot  2021-01-14 05:41
LOGIN      tty1         2021-01-14 05:42               630 id=tty1
           run-level 3  2021-01-14 05:42
root     + pts/0        2021-01-17 08:26 00:06       28432 (192.168.1.93)
root     + pts/1        2021-01-17 08:32   .         28737 (192.168.1.93)
```