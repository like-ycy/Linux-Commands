# sed

## 功能简介

sed是一种流编辑器，也是文本处理中非常好的工具，配合正则使用更强大处理时，把当前处理的行存储在临时缓冲区中，称为“模式空间”，接着用sed命令处理缓冲区的内容，完成后输出到屏幕，接着处理下一行。文件内容并没有改变，除非使用-i选项。sed主要用来编辑一个或多个文件，简化对文件的反复操作或者用来编写转换程序等。

sed功能同awk类似，差别在于，sed简单，对列处理的功能要差一些，awk功能复杂，对列处理的功能比较强大。

## 命令格式

```
 sed [options] 'command' file(s)
 sed [options] -f scriptfile file(s)
```

## 常用参数

```
-e #以指定的指令来处理输入的文本文件
-n #取消默认输出（如果和p命令同时使用只会打印发生改变的行）
-h #帮助
-V #显示版本信息
```

## 常用动作

```
a #在当前行下面插入文本
i #在当前行上面插入文本
c #把选定的行改为新的文本
d #删除，删除选择的行
D #删除模板块的第一行 
s #替换指定字符
h #拷贝模板块的内容到内存中的缓冲区
H #追加模板块的内容到内存中的缓冲区
g #获得内存缓冲区的内容，并替代当前模板块中的文本 
G #获得内存缓冲区的内容，并追加到当前模板块文本的后面 
l #列表不能打印字符的清单
n #读取下一个输入行，用下一个命令处理新的行而不是用第一个命令
N #追加下一个输入行到模板块后面并在二者间嵌入一个新行，改变当前行号码
p #打印匹配的行
P #(大写)打印模板的第一行
q #退出Sed
b #lable 分支到脚本中带有标记的地方，如果分支不存在则分支到脚本的末尾
r #file 从file中读行
t #label if分支，从最后一行开始，条件一旦满足或者T，t命令，将导致分支到带有标号的命令处，或者到脚本的末尾
T #label 错误分支，从最后一行开始，一旦发生错误或者T，t命令，将导致分支到带有标号的命令处，或者到脚本的末尾
w #file 写并追加模板块到file末尾**
W #file 写并追加模板块的第一行到file末尾**
! #表示后面的命令对所有没有被选定的行发生作用** 
= #打印当前行号码**
# #把注释扩展到下一个换行符以前**
```

## Sed替换命令

```
g #表示行内全面替换（全局替换配合s命令使用）
p #表示打印行 
w  #表示把行写入一个文件 
x #表示互换模板块中的文本和缓冲区中的文本 
y #表示把一个字符翻译为另外的字符（但是不用于正则表达式） 
1  #子串匹配标记 
& #已匹配字符串标记
```

## Sed正则

```
^ #匹配行开始 
$ #匹配行结束
. #匹配一个非换行符的任意字符
* #匹配0个或多个字符
[] #匹配一个指定范围内的字符
[^]  #匹配一个不在指定范围内的字符 
(..) #匹配子串
&  #保存搜索字符用来替换其他字符
< #匹配单词的开始
>  #匹配单词的结束
x{m} #重复字符x，m次
x{m,} #重复字符x，至少m次 
x{m,n} #重复字符x，至少m次，不多于n次
```

## Sed常用实例

1、替换操作

```
echo "hello world" |sed 's/ /-/1g'
hello-world 
#从第一个空格开始全局替换成-，只不过文本中只有一个空格
```

2、删除操作

```
sed '/^$/d' filename #删除空白行

sed '2d' filename #删除第二行

sed '2，$d' filename #删除第二直到未尾所有行

sed '$d' filename #删除最后一行

sed '/^test/'d filename #删除以test开头行
```

3、匹配替换

```
echo "hello world" |sed 's/w+/[&]/g'
[hello] [world]
echo "hello world" |sed 's/w+/"&"/g'
"hello" "world"
#w+匹配每一个单词，&表示匹配到的字符串

echo AAA bbb |sed 's/([A-Z]+) ([a-z]+)/[2] [1]/'
[bbb] [AAA]
#子串匹配替换
```

4、选定范围

```
sed -n '/= 0/,/max/p' svnserve.conf
#min-encryption = 0
#max-encryption = 256

#所有在=0到max范围内的行都会被打印出来
```

5、sed多点编辑功能（-e）

```
[root@centos001 ~]#cat -n test 
1  this is a test file
2  welcome
3  to
4  here
5  hello WORLD
6
7  linux centos6.8
8  redhat

sed -e '2,6d' -e 's/linux centos6.8/Linux Centos6.8/' test
this is a test file
Linux Centos6.8
redhat
#如果两条命令功能一样，那么就需要用到下面的参数

sed --expression='s/linux centos6.8/Linux Centos6.8/' --expression='s/to/TO/' test**
this is a test file
welcome
TO
here
hello WORLD
Linux CenTOs6.8
redhat
```

6、读入与写入

```
[root@centos001 ~]#cat test1
welcom 
to 
here

[root@centos001 ~]#sed '/here/r test1' test
this is a test file
welcome
to
here
#welcom
to
here#
hello WORLD
linux centos6.8
redhat

#将test1的文件内容读取显示所有匹配here行的后面
sed -n '/centos6.8/w test2' test

[root@centos001 ~]#cat test2
linux centos6.8

#将test文件匹配到centos6.8的所有行都写入到test2文件中，文件可以不存在.
#如果文件存在，就会被重定向不是追加
```

7、追加与插入

```
[root@centos001 ~]#sed '/^l/a2017-08-08' test2
linux centos6.8
2017-08-08
#在匹配以l开头的行的后面追加2017-08-08

[root@centos001 ~]#sed '1a2017-08-08' test2
linux centos6.8
2017-08-08
#在第一行的后面追加2017-08-08

[root@centos001 ~]#sed '/^l/i2017-08-08' test2
2017-08-08
linux centos6.8
#在匹配以l开头的行的前面插入2017-08-08
#######以上操作是不会改变文件内容################

[root@centos001 ~]#sed -i '/^l/i2017-08-08' test2
[root@centos001 ~]#cat test2
2017-08-08
linux centos6.8
```

8、其它命令实例

```
[root@centos001 ~]#cat -n test2
 1 2017-08-08
 2 linux centos6.8
 3 08
 4
 5 test

[root@centos001 ~]#**sed '/08/{ n; s/l/L/; }' test2
2017-08-08
Linux centos6.8
08
test
#如果08匹配到就跳到下一行，将小写l替换成大写，注意到第三行也是被匹配到
#但是后面的条件不满足，所有没有被替换

[root@centos001 ~]#sed '1,4y/8/9/' test2
2017-09-09
linux centos6.9
09
test
#将1至4行所有的数字8替换成9

[root@centos001 ~]#**sed '1q' test2**
2017-08-08
#打印第一行内容后退出
```

9、打印奇数或公偶数行

```
[root@centos001 ~]#sed -n 'p;n' test2
20170808
08

[root@centos001 ~]#sed -n 'n;p' test2
linux centos6.8
test

[root@centos001 ~]#sed -n '1~2p' test2
20170808
08

[root@centos001 ~]#sed -n '2~2p' test2
linux centos6.8
test
```

10、打印匹配字符串行的下一行

```
[root@centos001 ~]#sed -n '/linux/{n;p}' test2
08
[root@centos001 ~]#awk '/linux/{getline; print}' test2
08
```



# awk

## 命令简介

Awk  pattern scanning and processing language，对文本和数据进行处理。

awk 是一种编程语言，用于在linux/unix下对文本和数据进行处理。数据可以来自标准输(stdin)、一个或多个文件，或其它命令的输出。它在命令行中使用，但更多是作为脚本来使用。awk有很多内建的功能，比如数组、函数等，这是它和C语言的相同之处，灵活性是awk最大的优势。

## 语法格式

```
awk [options] 'scripts' var=value filename
```

## 常用参数

```
-F 指定分隔符（可以是字符串或正则表达式）
-f 从脚本文件中读取awk命令
-v var=value 赋值变量，将外部变量传递给awk
```

## 脚本基本结构

```
awk 'BEGIN{ print "start" } pattern{ commands } END{ print "end" }' filename
```

一个awk脚本通常由BEGIN语句+模式匹配+END语句三部分组成,这三部分都是可选项.

工作原理:

- 第一步执行BEGIN 语句
- 第二步从文件或标准输入读取一行，然后再执行pattern语句，逐行扫描文件到文件全部被读取
- 第三步执行END语句

实例展示:

```
echo "hello " | awk 'BEGIN{ print "welcome" } END{ print "2017-08-08" }'
welcome
2017-08-08

echo -e "hello" | awk 'BEGIN{ print "welcome" } {print} END{ print "2017-08-08" }'
welcome
hello
2017-08-08
#不加print参数时默认只打印当前的行

echo|awk '{ a="hello"; b="nihao"; c="mingongge"; print a,b,c; }'
hello nihao mingongge
#使用print以逗号分隔时，打印则是以空格分界

echo|awk '{ a="mgg"; b="mingg"; c="mingongge"; print a" is "b" or "c; }'
mgg is mingg or mingongge
#awk的print语句中双引号其实就是个拼接作用
```

## Awk的变量

内置变量

```
$0   #当前记录
$1~$n #当前记录的第N个字段
FS   #输入字段分隔符（-F相同作用）默认空格
RS   #输入记录分割符，默认换行符
NF   #字段个数就是列 
NR   #记录数，就是行号，默认从1开始
OFS  #输出字段分隔符，默认空格
ORS  #输出记录分割符，默认换行符 
```

外部变量

```
[mingongge@ ~]#a=100
[mingongge@ ~]#b=100
[mingongge@ ~]#echo |awk '{print v1*v2 }' v1=$a v2=$b
10000
```

## Awk运算与判断

算术运算符

```
+ - 加减
* / & 乘 除 求余
^ *  求幂
++ -- 增加或减少，作为前缀或后缀
[mingongge@ ~]#awk 'BEGIN{a="b";print a,a++,a--,++a;}'
b 0 1 1

[mingongge@ ~]#awk 'BEGIN{a="0";print a,a++,a--,++a;}'
0 0 1 1

[mingongge@ ~]#awk 'BEGIN{a="0";print a,a++,--a,++a;}'
0 0 0 1

#和其它编程语言一样，所有用作算术运算符进行操作，操作数自动转为数值，所有非数值都变为0
```

赋值运算符

```
= += -= *= /= %= ^= **=
```

正则运算符

```
~ !~  匹配正则表达式/不匹配正则表达式
```

逻辑运算符

```
||  &&  逻辑或  逻辑与
```

关系运算符

```
< <= > >= != = 
```

其它运算符

```
$   字段引用 
空格 字符串链接符
?:   三目运算符
ln   数组中是否存在某键值
```

## Awk正则

```
^    行首定位符
$    行尾定位符
.    匹配任意单个字符
*    匹配0个或多个前导字符（包括回车）
+    匹配1个或多个前导字符
?    匹配0个或1个前导字符 
[]   匹配指定字符组内的任意一个字符/^[ab]
[^]  匹配不在指定字符组内的任意一个字符
()   子表达式
|    或者
\    转义符
~,!~ 匹配或不匹配的条件语句
x{m} x字符重复m次
x{m,} x字符至少重复m次
X{m,n} x字符至少重复m次但不起过n次（需指定参数-posix或--re-interval）
```

## Awk实例介绍

```
awk –F : ‘{print $2}’ datafile
#以:分隔打印第二列

awk –F : ‘/^Dan/{print $2}’ datafile
#以:分隔打印以Dan开头行的第二列内容

awk –F : ‘/^[CE]/{print $1}’ datafile 
#打印以C或E开头行的第一列

awk –F : ‘{if(length($1) == 4) print $1}’ datafile 
#打印以:分隔且长度为4字符的第一列内容

awk –F : ‘/[916]/{print $1}’ datafile
#匹配916的行以:分隔打印第一列

awk -F : '/^Vinh/{print "a"$5}' 2.txt
#显示以Dan开头行并在第五列前加上a

awk –F : ‘{print $2”,”$1}’  datafile
#打印第二列第一列并以,分隔

awk -F : '($5 == 68900) {print $1}' 2.txt
#以:分隔打印第五列是68900的行第一列  

awk -F : '{if(length($1) == 11) print $1}' 2.txt
#打印以:分隔且长度为4字符的第一列内容

awk -F : '$1~/Tommy Savage/ {print $5}' 2.txt
awk -F : '($1 == "Tommy Savage") {print $5}' 2.txt
#打印以:分隔且第一列为Tommy Savage的第五列内容

ll |awk 'BEGIN {size=0;} {size=size+$5;} END{print "[end]size is ",size}'
#统计目录个的文件所有的字节数

awk 'BEGIN{size=0;} {size=size+$5;} END{print "[end]size is ",size/1024/1024,"M"}' 
#以M为单位显示目录下的所有字节数

awk 'BEGIN{a=10;a+=10;print a}'
20 
#a+10等价于 a=a+10

echo|awk 'BEGIN{a="100testaaa"}a~/test/{print "ok"}' 
#正则匹配a 是否有test字符，成立打印ok

awk 'BEGIN{a="b";print a=="b"?"ok":"err"}'
ok
awk 'BEGIN{a="b";print a=="c"?"ok":"err"}'
err
#三目运算符?:

awk '/root/{print $0}' passwd 
#匹配所有包含root的行

awk -F: '$5~/root/{print $0}' passwd 
# 以分号作为分隔符，匹配第5个字段是root的行

ifconfig eth0|awk 'BEGIN{FS="[[:space:]:]+"} NR==2{print $4}'
#打印IP地址

awk '{print toupper($0)}' test.txt
#toupper是awk内置函数，将所小写字母转换成大写
```



# grep

## 命令简介

文本查找或搜索工具。用于查找内容包含指定的范本样式的文件，如果发现某文件的内容符合所指定的范本样式，预设grep会把含有范本样式的那一列显示出来。若不指定任何文件名称，或是所给予的文件名为 -，则grep会从标准输入设备读取数据。

同样可以配合正则表达式来搜索文本，并将匹配的行打印输出,也可用于过滤与搜索特定字符串，使用十分灵活

## 常用参数

```
-a  #不要忽略二进制数据
-A  #除了显示符合范本样式的那一行之外，并显示该行之后的内容
-b  #在显示符合范本样式的那一行之外，并显示该行之前的内容
-B  #除了显示符合样式的那一行之外，并显示该行之前的内容
-c  #计算符合范本样式的列数
-C  #除了显示符合范本样式的那一列之外，并显示该列之前后的内容
-d  #当指定要查找的是目录而非文件时，必须使用这项参数，否则grep命令将回报信息并停止动作
-e  #指定字符串作为查找文件内容的范本样式
-E  #将范本样式为延伸的普通表示法来使用，意味着使用能使用扩展正则表达式
-f  #指定范本文件，其内容有一个或多个范本样式，让grep查找符合范本条件的文件内容，格式为每一列的范本样式
-F  #将范本样式视为固定字符串的列表
-G  #将范本样式视为普通的表示法来使用
-h  #在显示符合范本样式的那一列之前，不标示该列所属的文件名称
-H  #在显示符合范本样式的那一列之前，标示该列的文件名称
-i  #忽略字符大小写的差别
-l  #列出文件内容符合指定的范本样式的文件名称
-L  #列出文件内容不符合指定的范本样式的文件名称
-n  #在显示符合范本样式的那一列之前，标示出该列的编号
-q  #不显示任何信息
-R/-r #此参数的效果和指定“-d recurse”参数相同
-s  #不显示错误信息
-v  #反转查找
-V  #显示版本信息 
-w  #只显示全字符合的列
-x  #只显示全列符合的列
-y  #此参数效果跟“-i”相同
-o  #只输出文件中匹配到的部分
```

## 正则表达式

```
^  #匹配以XX开头的行
$  #匹配以XX结尾的行
```

## 常用实例

1、在多个文件中查找：

```
grep "file" file_1 file_2 file_3
```

2、输出除之外的所有行 -v 选项：

```
grep -v "file" file_name
```

3、标记匹配颜色 --color=auto 选项：

```
grep "file" file_name --color=auto
```

4、使用正则表达式 -E 选项：

```
grep -E "[1-9]+"

egrep "[1-9]+"
```

5、只输出文件中匹配到的部分 -o 选项：

```
echo this is a test line. | grep -o -E "[a-z]+."
line.

echo this is a test line. | egrep -o "[a-z]+."
line.
```

6、统计文件或者文本中包含匹配字符串的行数-c 选项：

```
grep -c "text" file_name
2
```

7、输出包含匹配字符串的行数 -n 选项：

```
grep "text" -n file_name
或
cat file_name | grep "text" -n
```

8、多个文件

```
grep "text" -n file_1 file_2
```

9、搜索多个文件并查找匹配文本在哪些文件中：

```
grep -l "text" file1 file2 file3...
```

10、grep递归搜索文件

在多级目录中对文本进行递归搜索：

```
grep "text" . -r -n
```

11、忽略匹配样式中的字符大小写：

```
echo "hello world" | grep -i "HELLO"
hello
```

12、选项 -e 指定多个匹配样式：

```
echo this is a text line | grep -e "is" -e "line" -o
is
line
```

13、也可以使用 -f 选项来匹配多个样式，在样式文件中逐行写出需要匹配的字符。

```
cat patfile
aaa
bbb

echo aaa bbb ccc ddd eee | grep -f patfile -o
```

14、在grep搜索结果中包括或者排除指定文件：

只在目录中所有的.php和.html文件中递归搜索字符"main()"

```
grep "main()" . -r --include *.{php,html}
```

15、在搜索结果中排除所有README文件

```
grep "main()" . -r --exclude "README"
```

16、在搜索结果中排除filelist文件列表里的文件

```
grep "main()" . -r --exclude-from filelist
```

更多Linux命令请参考>>>值得收藏！[Linux系统常用命令速查手册](http://mp.weixin.qq.com/s?__biz=MzI0MDQ4MTM5NQ==&mid=2247500085&idx=2&sn=5455a50a3ec0fc0a69a7cc910a316ebe&chksm=e918a429de6f2d3f4ba700653b387459cb16dd4bf34cd42b4b0ef53c2dd91a53ce40abf0f2a2&scene=21#wechat_redirect)

```
grep "San" testfile 
#过滤有San的行

grep '^J' testfile 
#显示以J开头的行

grep '70$' testfile 
#显示以70结尾的行

grep -v "834" testfile 
#显示所有不包括834的行

grep ':12/' testfile 
#显示:12/的行 

grep ':498-' testfile 
#显示:498-的行

grep '[A-Z][a-z]{4}:[[:space:]][A-Z]' testfile 
#显示这样的行，一个大写字母+四个小写字母+空格+一个大写字母

grep '[a-z]{1,}[[:space:]][Kk]' testfile 
#显示包括K k的行

grep -n '[0-9]{6,}$' testfile 
#显示6位数字的行，并打印行号

grep -i "lincoln" testfile 
#显示有lincoln的行，不区分大小写
```