## 命令简介

nohup 命令用于将进程放后台运行（不挂断）。

## 命令语法

```
nohup Command [ Arg … ] [ & ]
```

## 选项说明

```
--help    #打印帮助信息并退出
--version  #打印版本信息并退出
```

## 应用举例

后台运行

```
[root@centos7 ~]# nohup java -server -Xms128M -Xmx512M -XX:MetaspaceSize=128M -jar test.jar $1 $2 $3 &
```

执行test.sh 脚本，并重定向输入到 test.log 文件

```
[root@centos7 ~]# nohup /scripts/test.sh > test.log 2>&1 &

2>&1 解释
#将标准错误 2 重定向到标准输出 &1 ，标准输出 &1 再被重定向输入到 test.log 文件中。
0 – stdin (standard input，标准输入)
1 – stdout (standard output，标准输出)
2 – stderr (standard error，标准错误输出)
```