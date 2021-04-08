## 命令简介

cat命令用来连接文件内容并打印输出到标准设备上，所以，它常常被用来查看显示文件的内容，或者将几个文件连接起来显示，或者从标准输入读取内容并显示，它常与重定向符号配合使用。

## cat命令三大功能

- 1、显示一个文件的全部内容，cat file_name
- 2、创建一个文件，cat > file_name
- 3、合并文件，将几个文件合并到一个文件，cat file1 file2 > file

## 语法格式

```
cat [选项] [文件]
cat [OPTION]  FILE
```

## 选项说明

```
-A, --show-all           #等价于 -vET
-b, --number-nonblank     #对非空输出行编号
-e                       #等价于 -vE
-E, --show-ends           #在每行结束处显示 $
-n, --number              #对输出的所有行编号,由1开始对所有输出的行数编号
-s, --squeeze-blank       #有连续两行以上的空白行，就代换为一行的空白行 
-t                      #与 -vT 等价
-T, --show-tabs          #将跳格字符显示为 ^I
-u                       #(被忽略)
-v, --show-nonprinting   #使用 ^ 和 M- 引用，除了LFD和TAB之外
```

## 应用实例

普通内容输出举例

```
[root@localhost ~]# cat mingongge.txt        #输出文件全部内容
1111111111


2222222222

3333333333
[root@localhost ~]# cat -n mingongge.txt     #输出全部内容，并显示行号
1  1111111111
2
3
4  2222222222
5
6  3333333333
[root@localhost ~]# cat -E mingongge.txt     #以$结束
1111111111$
$
$
2222222222$
$
3333333333$
[root@localhost ~]# cat -s mingongge.txt     #超过二个空行，合并成一个
1111111111

2222222222

3333333333
[root@localhost ~]# cat -ns mingongge.txt   #合并空行，加行号
1  1111111111
2
3  2222222222
4
5  3333333333
```

从键盘录入内容到文件，回车是保存，退出Ctrl+z

```
[root@localhost ~]# cat > mingongge.tx  
111111111111111
2233445566778899
0126459fdfdfdkffffkfkfkfkfdkfdkdfkk
^Z
[4]+  Stopped                 cat > mingongge.tx
```

合并文件

```
[root@localhost ~]# cat mingongge.tar.gz_?? > mingongge.tar.gz   
#可以用cat命令将多个压缩包合并成一个
```

追加文件内容

```
[root@localhost ~]# cat mingongge.txt
aa
aabb
bbcc
[root@localhost ~]# cat mingongge.doc
111111111111
222222222222
[root@localhost ~]# cat mingongge.txt >> mingongge.doc  #将mingongge.txt内容添加到mingongge.doc内容后
[root@localhost ~]# cat mingongge.doc
111111111111
222222222222
aa
aabb
bbcc
```

插入多行内容

```
[root@localhost ~]# cat >> mingongge.doc <<EOF
> 111111111111
> 222222222222
> aa+aabb-bbcc
> EOF
#将你所要输入的内容插入到文件中，输入EOF即为结束插入，EOF也可以使用其它字符替代。
[root@localhost ~]# cat mingongge.doc
111111111111
222222222222
aa+aabb-bbcc
```

清空文件内容

```
[root@localhost ~]# cat mingongge.doc
111111111111
222222222222
aa+aabb-bbcc
[root@localhost ~]# cat /dev/null > mingongge.doc
[root@localhost ~]# cat mingongge.doc
```