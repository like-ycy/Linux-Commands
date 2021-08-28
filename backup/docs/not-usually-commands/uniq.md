## 命令简介

uniq 命令用于去除文件中重复行，一般与 sort 命令结合使用。

## 语法格式

```
uniq [选项] [标准输入 [输出]]
uniq [OPTION] [INPUT [OUTPUT]]
输入文件 #指定要去除的重复行文件。如果不指定该项，则从标准读入
输出文件 #指定要去除重复行后的内容要写入的输出文件。如果不指定此项，则将内容显示到标准输出设备（显示终端）。
```

## 选项说明

```
-c  #在每列旁边显示该行重复出现的次数
-d  #只显示重复出现的行与列
-f  #忽略比较指定的字段
-s  #忽略比较指定的字符
-i  #不区分大小写的比较
-u  #只显示出现过一次的行与列
-w  #指定要比较的字符
-z  #用0字节（NULL）代替换行符
--help    #显示帮助信息并退出
--version #显示版本信息并退出
```

## 应用举例

```
#删除重复行
[root@centos7 ~]# cat test.txt 
This is a test line
This is a test line
This is a test line
This is also a test line
This is also a test line
This is also also a test line
[root@centos7 ~]# uniq test.txt 
This is a test line
This is also a test line
This is also also a test line
[root@centos7 ~]# sort test.txt | uniq
This is also also a test line
This is also a test line
This is a test line

#只显示单一行
[root@centos7 ~]# uniq -u test.txt
This is also also a test line
[root@centos7 ~]# sort test.txt |uniq -u
This is also also a test line

#统计各行在文件中出现的次数
[root@centos7 ~]# sort test.txt |uniq -c
      1 This is also also a test line
      2 This is also a test line
      3 This is a test line

#在文件中找出重复的行
[root@centos7 ~]# sort test.txt |uniq -d
This is also a test line
This is a test line
```