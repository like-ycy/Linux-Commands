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