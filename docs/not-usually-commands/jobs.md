## 命令简介

jobs 使用用于显示 Linux 中的任务列表及任务状态。

## 语法格式

```
jobs [-lnprs] [jobspec ...] or jobs -x command [args]
```

## 选项说明

```
-l  #显示进程号
-p  #仅任务对应的显示进程号
-n  #显示任务状态的变化
-r  #仅输出运行状态（running）的任务
-s  #仅输出停止状态（stoped）的任务
```

## 应用举例

实例

```
[root@centos7 ~]# jobs
[1]+  Stopped                 zcat mysql_backup.tar.gz | more

[root@centos7 ~]# jobs -l
[1]+  5328 Stopped                 zcat mysql_backup.tar.gz
      5329                       | more
[root@centos7 ~]# jobs -s
[1]+  Stopped                 zcat mysql_backup.tar.gz | more
[root@centos7 ~]# jobs -n
[root@centos7 ~]# jobs -p
5328
```