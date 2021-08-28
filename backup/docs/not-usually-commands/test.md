## 命令简介

test 命令执行条件表达式，用于检查文件类型并比较值，评估条件。如果为 true，则返回 0 退出状态，否则返回 1。

## 语法格式

```
test EXPRESSION
```

## 选项说明

文件操作符

```
-a FILE    如果文件存在，则为true。
-b FILE    如果文件是块特殊的，则为true。
-c FILE    如果文件是特殊字符，则为true。
-d FILE    如果文件是目录，则为true。
-e FILE    如果文件存在，则为true。
-f FILE    如果文件存在并且是常规文件，则为true。
-g FILE    如果文件是set-group-id，则为true。
-h FILE    如果文件是符号链接，则为true。
-L FILE    如果文件是符号链接，则为true。
-k FILE    如果文件的粘滞位（sticky）设置了，则为true。
-p FILE    如果文件是命名管道，则为true。
-r FILE    如果您可以读取文件，则为true。
-s FILE    如果文件存在且不为空，则为true。
-S FILE    如果文件是套接字，则为true。
-t FD      如果在终端上打开FD，则为True。
-u FILE    如果文件是set-user-id，则为true。
-w FILE    如果文件可写，则为true。
-x FILE    如果您可以执行文件，则为true。
-O FILE    如果文件有效地归您所有，则为true。
-G FILE    如果文件有效地归您的组所有，则为true。
-N FILE    如果文件自上次读取以来已被修改，则为true。
 
FILE1 -nt FILE2   根据修改日期，如果 file1 比 file2 新，则为true。
FILE1 -ot FILE2   根据修改日期，如果 file1 比 file2 旧，则为true。
FILE1 -ef FILE2   如果 file1 为 file2 的硬链接，则为true。
```

字符串运算符

```
-z STRING              如果字符串为空，则为true。
-n STRING              如果字符串不为空，则为true。
STRING                 如果字符串不为空，则为true。
STRING1 = STRING2      如果字符串相等，则为true。
STRING1 ！= STRING2    如果字符串不相等，则为true。
STRING1 < STRING2      如果 STRING1 的字典排序在 STRING2 之前，则为true。
STRING1 > STRING2      如果 STRING1 在字典排序在 STRING2 之后，则为true。
```

其他运算符

```
-o OPTION        如果启用了shell选项OPTION，则为true。
-v VAR           如果设置了shell变量VAR，则为true。
-R VAR           如果设置了shell变量VAR并且是变量引用，则为true。
！EXPR           如果expr为假，则为true。
EXPR1 -a EXPR2    如果expr1和expr2都为true，则为true。
EXPR1 -o EXPR2    如果expr1或expr2为true，则为true。
arg1 OP arg2      算术表达式测试；OP是 -eq，-ne，-lt，-le，-gt，-ge 中的一个；算术表达式为真时返回true。
```

参考：https://www.computerhope.com/unix/test.htm

## 应用举例

比较大小

```
[root@centos7 ~]# test 100 -gt 99 && echo "Yes, that's true." || echo "No, that's false."
Yes, that's true.
[root@centos7 ~]# test 100 -lt 99 && echo "Yes." || echo "No."
No.
```

判断字符串

```
[root@centos7 ~]# [ "mingongge" = "mgg" ]; echo $?
1
[root@centos7 ~]# [ "mingongge" = "mingongge" ]; echo $?
0
```

测试目录是否存在

```
[root@centos7 ~]# test ! -d /usr/local/mingongge && echo "yes." ||echo "No."
yes.
[root@centos7 ~]# test -d /usr/local/mingongge && echo "yes." ||echo "No."
No.
```