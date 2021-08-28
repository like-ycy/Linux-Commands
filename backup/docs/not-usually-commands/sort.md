## 命令简介

sort 对文件的文本内容排序。

系统默认情况下，排序规则如下：

- 以数字开头的行，将排在以字母开头的行前面
- 以小写字母开头的行，将排在以大写字母开头的行前面
- 按字母表的顺序排列以字母开头的行

## 语法格式

```
sort [选项] [文件]
sort [OPTION] [FILE]
```

## 选项说明

```
-b    #排除开头的空白
-d    #只考虑空白、字母、数字
-f    #将小写字母视为大写字母考虑
-g    #根据数字排序
-i    #排除不可打印字符
-M    #按非月份的顺序排序
-h    #根据存储容量排序
-n    #根据数字排序。
-R    #随机排序
-r    #倒序
--sort=WORD    #根据指定的WORD排序
-V   #按文本中(版本)数字的自然排序
-o   #将排序结果写入一个文件
--help     #显示帮助信息并退出
--version  #显示版本信息并退出
```

## 应用举例

```
[root@centos7 testdir]# cat cuttest.txt 
1 2 3 4 5 6 8
9 8 7 6 5 4 3
2 1 9 8 7 6 5
[root@centos7 testdir]# sort cuttest.txt
1 2 3 4 5 6 8
2 1 9 8 7 6 5
9 8 7 6 5 4 3

#将结果输出到文件
[root@centos7 testdir]# sort -o sort.cut.txt cuttest.txt
[root@centos7 testdir]# cat sort.cut.txt
1 2 3 4 5 6 8
2 1 9 8 7 6 5
9 8 7 6 5 4 3

#倒序排列
[root@centos7 testdir]# sort -r cuttest.txt
9 8 7 6 5 4 3
2 1 9 8 7 6 5
1 2 3 4 5 6 8
```