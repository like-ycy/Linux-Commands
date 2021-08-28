## 命令简介

time 命令用于计算命令执行时间（相当于统计总时间）。

time 命令使用指定参数运行指定的程序命令， 命令完成后，时间将消息写入标准错误，提供有关此程序运行的计时统计信息。这些统计信息包括：

- 调用和终止之间经过的实时时间
- 用户CPU时间
- 系统CPU时间

## 语法格式

```
time [-p] command [arguments...]
```

## 选项说明

```
-f   #使用指定格式输出
-p   #使用兼容 POSIX 的格式输出
-o   #将结果输出到指定文件
-a   #使用追加模式将输出写入指定文件
-v   #输出详细信息
--help   #显示帮助信息
-V       #显示版本信息
```

扩展参数说明（-f参数后的参数）：

```
%E #real时间，显示格式为[小时:]分钟:秒
%U #user时间
%S #sys时间
%C #进行计时的命令名称和命令行参数
%D #进程非共享数据区域，以KB为单位
%x #命令退出状态
%k #进程接收到的信号数量
%w #进程被交换出主存的次数
%Z #系统的页面大小，这是一个系统常量，不用系统中常量值也不同。
%P #进程所获取的CPU时间百分百，这个值等于 user+system 时间除以总共的运行时间
%K #进程的平均总内存使用量（data+stack+text），单位是 KB
%w #进程主动进行上下文切换的次数，例如等待I/O操作完成
%c #进程被迫进行上下文切换的次数（由于时间片到期）
```

## 应用举例

显示执行ls命令的时间

```
[root@centos7 ~]# time ls
123              goInception-linux-amd64-v1.2.3.tar.gz  mingongge.z02
234              httpd                                  mingongge.zip
456              httpd-2.4.46                           mysql_backup.tar.gz
anaconda-ks.cfg  httpd-2.4.46.tar.gz                    mysql_bakcup
dos_test.txt     httpd-2.4.6-95.el7.centos.x86_64.rpm   testdir
download         mingongge.file                         test.txt
goinception      mingongge.z01

real 0m0.013s
user 0m0.007s
sys 0m0.003s
```

输出的信息real 时间、user 时间和 sys 时间详解：

- real 时间是指挂钟时间，也就是命令开始执行到结束的时间。这个短时间包括其他进程所占用的时间片，和进程被阻塞时所花费的时间。
- user 时间是指进程花费在用户模式中的 CPU 时间，这是唯一真正用于执行进程所花费的时间，其他进程和花费阻塞状态中的时间没有计算在内。
- sys 时间是指花费在内核模式中的 CPU 时间，代表在内核中执系统调用所花费的时间，这也是真正由进程使用的 CPU 时间。

一般常用time比较两个命令执行的效率。