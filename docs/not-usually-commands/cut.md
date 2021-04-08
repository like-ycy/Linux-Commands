## 命令简介

cut 将文件中行中内容按指定分隔符分割并输出。

cut命令还可以用于删除文件中指定行或段，然后打印输出更改后的内容。还可能用以拼接文件内容到一个新的文件中，功能和cat类似。

## 命令格式

```
cut [选项] [链接文件名]
cut [OPTION] [LINKNAME]
```

## 选项说明

```
-b #只显示行中指定（字节数）的内容
-c #只显示行中指定（字符数）的内容
-d #指定字段的分隔符，默认为“TAB”
-f #打印指定字段（列）的内容
-n #与“-b”选项连用，不分割多字节字符
-s #不打印不包含定界符的行的内容
--help     #打印帮助信息
--version  #打印版本信息
```

cut命令中指定字节或字符范围的说明如下：

```
N    #从1字节、字符或字段开始到第N个字节、字符或字段
N-  #从第N个字节、字符或字段到行的结尾
N-M  #从第N个字节、字符或字段到第M个字节，字符或字段
-M  #从第1个字节、字符或字段到第M个字节、字符或字段
注意：所有的范围取值需为整数，如：10,10-,10-20,-20。
```

## 应用举例

```
#打印指定字节数的内容
[root@centos7 testdir]# cat mingongge1.txt 
1111 11 111111 1 111 1 1 11
22222222222 222 2222 22 2 2 2
33333333333 333333 3333 333 33
444444444444 444 444444444
[root@centos7 testdir]# cut -b 3 mingongge1.txt
1
2
3
4

#截取指定字段内容
[root@centos7 testdir]# cat cuttest.txt 
1 2 3 4 5 6 8
9 8 7 6 5 4 3
2 1 9 8 7 6 5
#以空格为分隔，打印每一行的第一列
[root@centos7 testdir]# cut -f1 -d" " cuttest.txt 
1
9
2
#以空格为分隔，打印每一行的第一列和第三列
[root@centos7 testdir]# cut -f1,3 -d" " cuttest.txt 
1 3
9 7
2 9
#以空格为分隔，打印每一行的第三列到结尾
[root@centos7 testdir]# cut -f3- -d" " cuttest.txt 
3 4 5 6 8
7 6 5 4 3
9 8 7 6 5

#截取每一行第2-5个字符
[root@centos7 testdir]# cut -c 2-5 cuttest.txt 
 2 3
 8 7
 1 9
#截取每一行第一个到第五个字符
[root@centos7 testdir]# cut -c -5 cuttest.txt 
1 2 3
9 8 7
2 1 9
#截取每一行第五个到最后一个字符
[root@centos7 testdir]# cut -c 5- cuttest.txt 
3 4 5 6 8
7 6 5 4 3
9 8 7 6 5
```

指定分隔符截取内容的用法非常实用，工作中也经常使用。