## 命令简介

paste 命令用于并排显示多个文件的相应行，将多个文件按列合并。

## 语法格式

```
paste [选项] [文件]
paste [OPTION] [FILE]
```

## 选项说明

```
-d  #指定分隔符来取代默认分隔符（TAB分隔符）
-s  #串列进行而非平行处理
--help  #显示帮助信息
--version  #显示版本信息
```

## 应用举例

并排显示两个文件的内容，

```
[root@centos7 testdir]# paste mingongge1.txt mingongge2.txt
1111 11 111111 1 111 1 1 11 head1
22222222222 222 2222 22 2 2 2 head2
33333333333 333333 3333 333 33 head3
444444444444 444 444444444 head4
1 
2 
3 
4 
```

paste 命令其他用法

```
[root@centos7 testdir]# paste mingongge1.txt 
1111 11 111111 1 111 1 1 11
22222222222 222 2222 22 2 2 2
33333333333 333333 3333 333 33
444444444444 444 444444444
1
2
3
4
 
#连接文件中的所有行
[root@centos7 testdir]# paste -s mingongge1.txt 
1111 11 111111 1 111 1 1 11 22222222222 222 2222 22 2 2 2 33333333333 333333 3333 333 33 444444444444 444 444444444 1 2 3 4
 
#使用指定分隔符连接所有行
[root@centos7 testdir]# paste -d, -s mingongge1.txt
1111 11 111111 1 111 1 1 11,22222222222 222 2222 22 2 2 2,33333333333 333333 3333 333 33,444444444444 444 444444444,1,2,3,4
[root@centos7 testdir]# paste -d[] -s mingongge1.txt
1111 11 111111 1 111 1 1 11[22222222222 222 2222 22 2 2 2]33333333333 333333 3333 333 33[444444444444 444 444444444]1[2]3[4
[root@centos7 testdir]# paste -d/ -s mingongge1.txt
1111 11 111111 1 111 1 1 11/22222222222 222 2222 22 2 2 2/33333333333 333333 3333 333 33/444444444444 444 444444444/1/2/3/4
 
#查看 paste 命令版本
[root@centos7 testdir]# paste --version
paste (GNU coreutils) 8.22
Copyright (C) 2013 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Written by David M. Ihnat and David MacKenzie.
```

paste 合并两个文件，或者添加行

```
[root@centos7 testdir]# cat mingongge1.txt
1111 11 111111 1 111 1 1 11
22222222222 222 2222 22 2 2 2
33333333333 333333 3333 333 33
444444444444 444 444444444
1
2
3
4
[root@centos7 testdir]# cat mingongge2.txt 
head1
head2
head3
head4
[root@centos7 testdir]# paste -d '\n' mingongge1.txt mingongge2.txt
1111 11 111111 1 111 1 1 11
head1
22222222222 222 2222 22 2 2 2
head2
33333333333 333333 3333 333 33
head3
444444444444 444 444444444
head4
1

2

3

4

[root@centos7 testdir]# paste -d '\r' mingongge1.txt mingongge2.txt
head111 111111 1 111 1 1 11
head2222222 222 2222 22 2 2 2
head3333333 333333 3333 333 33
head44444444 444 444444444
1
2
3
4
```