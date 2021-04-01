## 命令介绍

shutdown 命令可以用执行系统关机或系统重启，shutdown可以关闭系统的所有应用程序，并按用户的指定要求，进行系统关闭或重启的动作执行。此命令需要具备系统管理员权限才能使用。

## 命令格式

```
shutdown [选项] [其它信息]
```

## 参数说明

```
-c：#执行shutdown命令后，只需要按+键就可以中断正在执行的命令
-f：#重启时不执行fsck
-F：#重启时执行fsck
-h：#关机
-k：#发送信息给所有用户，但不会关机
-n：#不调用init程序进行关机
-r：#关机之后再重新启动
-t<秒数>：#发送警告信息和删除信息之间的延迟时间
```

## 示例详解

1、马上关机

```
shutdown -H now
//或
halt
```

2、系统将在今天指定的时间23:59分关机

```
# shutdown -H 23:59
```

3、马上重启系统

```
shutdown -r now
//或
reboot
```

4、向所有用户发送告警信息，系统会在30分钟自动重启

```
shutdown -r +30 'The system will reboot 30mins later' 
```

5、仅向所有用户发出警告信息，系统并不会真正关机

```
shutdown -k now 'This is just a warning message'
```

6、立即执行关机操作并且断电

```
shutdown -P now
//或
poweroff
```

7、仅发出警告，实际上不会执行关机操作，恶搞~~~~

```
shutdown +10 -k '10分钟后关机'
```

8、设置系统在那个时间点关机

```
shutdown -h 12:30
或后台执行 
shutdown -h 12:30 &
```

9、取消shutdown命令的执行

```
如果执行了下面的命令，突然发现时间上有冲突，可以使用ctrl+c取消
shutdown -h 12:3
Shutdown cancelled.
或者，在另一个命令行窗口，使用下面的命令取消。
shutdown -c
```