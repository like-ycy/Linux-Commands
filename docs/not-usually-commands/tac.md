## 命令简介

tac 命令用于按相反顺序逐行连接和打印文件内容。

和 cat 命令一样，将每个文件连接到标准输出，但顺序相反，逐行打印，首先打印最后一行。这对于检查按时间顺序排列的日志文件很有用（例如），其中文件的最后一行包含最新的信息。

## 语法格式

```
tac [OPTION] ... [FILE] ... 
```

## 选项说明

```
-b          #在之前而不是之后连接分隔符
-r          #将分隔符作为基础正则表达式（BRE）处理
-s          #使用STRING作为分隔符代替默认的换行符
--help      #显示帮助信息并退出
--version   #显示版本信息并退出
```

## 应用举例

反向输出一个文件，从最后一行开始到第一行（与cat对比显示）

```
[root@centos7 ~]# tac test.txt 
This is also also a test line
This is also a test line
This is also a test line
This is a test line
This is a test line
This is a test line
[root@centos7 ~]# cat test.txt 
This is a test line
This is a test line
This is a test line
This is also a test line
This is also a test line
This is also also a test line
```