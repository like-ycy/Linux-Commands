## 命令简介

tee 命令用于从标准输入读取，然后写入文件或标准输出和文件。一般用于需要同时查看数据内容并输出到文件时使用。

## 语法格式

```
tee [OPTION]... [FILE]...
```

## 选项说明

```
-a   #追加到文件中而不是覆盖
-i   #忽略中断信号（Ctrl+c中断操作无效）
-p   #诊断写入非管道的错误
--output-error[=MODE]    #设置写错误时的行为
--help                   #显示帮助信息并退出
--version                #显示版本信息并退出
```

MODE参数

```
'warn'           #当写入到任何输出报错时诊断
'warn-nopipe'    #当写入到任何输出（而不是管道）报错时诊断
'exit'           #当写入到任何输出报错时退出
'exit-nopipe'    #当写入到任何输出（而不是管道）报错时退出
```

## 应用举例

列出当前目录中所有文件扩展名为.tar.gz的文件，每行一个文件， 然后将内容传输给 wc 对行进行计数并输出数字。通过管道传输到 tee 后再将输出写入终端，并将相同的信息写入文件 tee.txt。如果 tee.txt 已经存在，它将被覆盖，如果不存在，将被创建。

```
[root@centos7 ~]# ls -l *.tar.gz
-rw-r--r-- 1 root root 13034487 Aug 30  2020 goInception-linux-amd64-v1.2.3.tar.gz
-rw-r--r-- 1 root root  9363314 Aug  5  2020 httpd-2.4.46.tar.gz
-rw-r--r-- 1 root root 31674465 Mar 10 09:42 mysql_backup.tar.gz
-rw-r--r-- 1 root root   398872 Mar 28 00:11 netcat-0.7.1.tar.gz
[root@centos7 ~]# ls -l *.tar.gz | wc -l
4
[root@centos7 ~]# ls -l *.tar.gz | wc -l | tee tee.txt
4
[root@centos7 ~]# cat tee.txt
4
```

tee.txt 已经存在，它将被覆盖

```
[root@centos7 ~]# cat tee.txt 
4
[root@centos7 ~]# ls -1 *.txt | wc -l 
3
[root@centos7 ~]# ls -l *.txt | wc -l |tee tee.txt
3
[root@centos7 ~]# cat tee.txt 
3
```

追加内容

```
[root@centos7 ~]# cat tee.txt 
3
[root@centos7 ~]# ls -1 *.tar.gz | wc -l
4
[root@centos7 ~]# ls -1 *.tar.gz | wc -l | tee -a tee.txt
4
[root@centos7 ~]# cat tee.txt 
3
4
```