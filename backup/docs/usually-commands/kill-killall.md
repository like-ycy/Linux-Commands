## 命令简介

kill 命令用于删除执行中的程序或工作。kill 命令向进程发送信号。如果您未指定要发送的信号，则默认情况下会发送 TERM 信号，从而终止该过程。

killall 命令使用进程的名称来杀死一组进程，killall 命令需要安装。

## 语法格式

```
kill pid ... 
kill {-signal | -s signal} pid ...
killall [OPTIONS]
```

## 选项说明

kill 命令选项

```
-a  #当处理当前进程时，不限制命令名和进程号的对应关系
-l <信息编号>  #若不加<信息编号>选项，则-l参数会列出全部的信息名称
-s <信息名称或编号>  #指定要送出的信息
-p  #只打印相关进程的进程号
-u  #指定用户
```

killall 命令选项：

```
-e  #对长名称进行精确匹配
-l  #忽略大小写的不同
-p  #杀死进程所属的进程组
-i  #交互式模式，杀死进程前需要进行确认
-l  #打印所有已知信号列表
-q  #不输出任何信息
-r  #使用正规表达式匹配要杀死的进程名称
-s  #用指定的进程号代替默认信号“SIGTERM”
-u  #杀死指定用户的进程
```

## 应用举例

显示所有信息

```
[root@centos7 ~]# kill -l
 1) SIGHUP  2) SIGINT  3) SIGQUIT  4) SIGILL  5) SIGTRAP
 6) SIGABRT  7) SIGBUS  8) SIGFPE  9) SIGKILL 10) SIGUSR1
11) SIGSEGV 12) SIGUSR2 13) SIGPIPE 14) SIGALRM 15) SIGTERM
16) SIGSTKFLT 17) SIGCHLD 18) SIGCONT 19) SIGSTOP 20) SIGTSTP
21) SIGTTIN 22) SIGTTOU 23) SIGURG 24) SIGXCPU 25) SIGXFSZ
26) SIGVTALRM 27) SIGPROF 28) SIGWINCH 29) SIGIO 30) SIGPWR
31) SIGSYS 34) SIGRTMIN 35) SIGRTMIN+1 36) SIGRTMIN+2 37) SIGRTMIN+3
38) SIGRTMIN+4 39) SIGRTMIN+5 40) SIGRTMIN+6 41) SIGRTMIN+7 42) SIGRTMIN+8
43) SIGRTMIN+9 44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12 47) SIGRTMIN+13
48) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-12
53) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9 56) SIGRTMAX-8 57) SIGRTMAX-7
58) SIGRTMAX-6 59) SIGRTMAX-5 60) SIGRTMAX-4 61) SIGRTMAX-3 62) SIGRTMAX-2
63) SIGRTMAX-1 64) SIGRTMAX 
```

常用的信号(9信号是无条件终止)

```
HUP     1    终端断线
INT     2    中断（同 Ctrl + C）
QUIT    3    退出（同 Ctrl + \）
TERM   15    终止
KILL    9    强制终止
CONT   18    继续（与STOP相反， fg/bg命令）
STOP   19    暂停（同 Ctrl + Z）
```

查找指定的进程后，再通过进程ID杀死进程

```
[root@centos7 ~]# ps -ef|grep ssh
root        868      1  0 Mar27 ?        00:00:00 /usr/sbin/sshd -D
root       4878    868  0 02:10 ?        00:00:00 sshd: root@pts/0
root       4909   4880  0 02:35 pts/0    00:00:00 grep --color=auto ssh
[root@centos7 ~]# kill 4878
```

批量操作

```
[root@centos7 ~]# ps -ef |grep ssh
root        868      1  0 Mar27 ?        00:00:00 /usr/sbin/sshd -D
root       4878    868  0 02:10 ?        00:00:00 sshd: root@pts/0
root       4911   4880  0 02:37 pts/0    00:00:00 grep --color=auto ssh
[root@centos7 ~]# ps -ef |grep ssh |awk '{print $2}'
868
4878
4913
[root@centos7 ~]# ps -ef |grep ssh |awk '{print $2}' -exec kill -9
[root@centos7 ~]# ps -ef |grep ssh |awk '{print $2}' |xargs kill -9
```

杀死所有同名的进程

```
[root@centos7 ~]#killall vim
```