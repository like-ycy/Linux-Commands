## 命令简介

pstree 命令以树状图的方式展现进程之间的派生关系。

```
[root@centos7 ~]# pstree
-bash: pstree: command not found
[root@centos7 ~]# yum install psmisc -y
```

## 语法格式

```
pstree [OPTIONS] 
```

## 选项说明

```
-a  #显示每个程序的完整指令
-c  #不使用精简标示法
-G  #使用VT100终端机的列绘图字符
-h  #列出树状图时，特别标明现在执行的程序
-H<程序识别码>  #此参数的效果和指定"-h"参数类似
-l  #采用长列格式显示树状图
-n  #用程序识别码排序
-p  #显示程序识别码
-u  #显示用户名称
-U  #使用UTF-8列绘图字符
-V  #显示版本信息
```

## 应用举例

```
[root@centos7 ~]# pstree
systemd─┬─NetworkManager───2*[{NetworkManager}]
        ├─agetty
        ├─auditd───{auditd}
        ├─chronyd
        ├─crond
        ├─dbus-daemon
        ├─lvmetad
        ├─master─┬─pickup
        │        └─qmgr
        ├─polkitd───6*[{polkitd}]
        ├─rsyslogd───2*[{rsyslogd}]
        ├─sshd─┬─sshd───bash─┬─gzip
        │      │             ├─more
        │      │             └─pstree
        │      └─sshd───bash
        ├─systemd-journal
        ├─systemd-logind
        ├─systemd-udevd
        └─tuned───4*[{tuned}]
```

显示系统当前所有进程的进程ID和进程号

```
[root@centos7 ~]# pstree -p
systemd(1)─┬─NetworkManager(634)─┬─{NetworkManager}(656)
           │                     └─{NetworkManager}(658)
           ├─agetty(643)
           ├─auditd(600)───{auditd}(601)
           ├─chronyd(646)
           ├─crond(638)
           ├─dbus-daemon(626)
           ├─lvmetad(503)
           ├─master(972)─┬─pickup(5692)
           │             └─qmgr(974)
           ├─polkitd(623)─┬─{polkitd}(633)
           │              ├─{polkitd}(636)
           │              ├─{polkitd}(637)
           │              ├─{polkitd}(641)
           │              ├─{polkitd}(647)
           │              └─{polkitd}(651)
           ├─rsyslogd(870)─┬─{rsyslogd}(897)
           │               └─{rsyslogd}(898)
           ├─sshd(868)─┬─sshd(5304)───bash(5306)─┬─gzip(5328)
           │           │                         ├─more(5329)
           │           │                         └─pstree(6204)
           │           └─sshd(5546)───bash(5548)
           ├─systemd-journal(484)
           ├─systemd-logind(635)
           ├─systemd-udevd(509)
           └─tuned(872)─┬─{tuned}(1131)
                        ├─{tuned}(1132)
                        ├─{tuned}(1134)
                        └─{tuned}(1138)
```

显示所有进程的详细信息，相同的进程名可以压缩显示

```
[root@centos7 ~]# pstree -a
systemd --switched-root --system --deserialize 22
  ├─NetworkManager --no-daemon
  │   └─2*[{NetworkManager}]
  ├─agetty --noclear tty1 linux
  ├─auditd
  │   └─{auditd}
  ├─chronyd
  ├─crond -n
  ├─dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation
  ├─lvmetad -f
  ├─master -w
  │   ├─pickup -l -t unix -u
  │   └─qmgr -l -t unix -u
  ├─polkitd --no-debug
  │   └─6*[{polkitd}]
  ├─rsyslogd -n
  │   └─2*[{rsyslogd}]
  ├─sshd -D
  │   ├─sshd
  │   │   └─bash
  │   │       ├─gzip -cd mysql_backup.tar.gz
  │   │       ├─more
  │   │       └─pstree -a
  │   └─sshd
  │       └─bash
  ├─systemd-journal
  ├─systemd-logind
  ├─systemd-udevd
  └─tuned -Es /usr/sbin/tuned -l -P
      └─4*[{tuned}]
```

查看指定进程的PID

```
[root@centos7 ~]# pstree -p | grep ssh
           |-sshd(868)-+-sshd(5304)---bash(5306)-+-grep(6325)
           |           `-sshd(5546)---bash(5548)
[root@centos7 ~]# pstree -p | grep system
systemd(1)-+-NetworkManager(634)-+-{NetworkManager}(656)
           |-systemd-journal(484)
           |-systemd-logind(635)
           |-systemd-udevd(509)
```