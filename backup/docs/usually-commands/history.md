## 命令简介

history 命令用于查看系统中用户执行命令的历史纪录。读取历史命令文件中的目录到历史命令缓冲区和将历史命令缓冲区中的目录写入命令文件。

历史命令是被保存在内存中的，当退出或者登录 shell 时，会自动保存或读取。在内存中，历史命令仅能够存储 1000 条历史命令，该数量是由环境变量 HISTSIZE 进行控制。

## 语法格式

```
history [OPTIONS ]
```

## 选项说明

```
-c  #清空当前历史命令
-d offset #删除偏移量 OFFSET 处的历史记录条目
-a  #将历史命令缓冲区中命令写入历史命令文件中
-r  #将历史命令文件中的命令读入当前历史命令缓冲区
-w  #将当前历史命令缓冲区命令写入历史命令文件中
```

## 应用举例

打印20条历史命令（最近使用，从最后一条往前数）

```
[root@centos7 ~]# history 20
  876  /usr/sbin/time
  877  which time
  878  find / -type f -name "time"
  879  find /  -name "time"
  880  /sys/module/printk/parameters/time
  881  find /  -name "time*"
  882  time --help
  883  time -V
  884  man time
  885  yum install time -y
  886  time -V
  887  time --help
  888  /usr/bin/time 
  889  /usr/bin/time -f "time: %U" ls
  890  /usr/bin/time -f "time: %U" cat download/mingongge
  891  /usr/bin/time -f "time: %S" cat download/mingongge
  892  /usr/bin/time -f "time: %E" cat download/mingongge
  893  /usr/bin/time  cat download/mingongge
  894  time  cat download/mingongge
  895  history 20
```