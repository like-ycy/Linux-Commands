## 命令简介

xargs可以将stdin中以空格或换行符进行分隔的数据，形成以空格分隔的参数（arguments），传递给其他[命令](http://mp.weixin.qq.com/s?__biz=MzI0MDQ4MTM5NQ==&mid=2247503585&idx=1&sn=4479870e9509cfea8221b7034f2eb8ac&chksm=e918abfdde6f22eb129d650de68059e16862b98889ba63843e64f710429b56333b045687b81c&scene=21#wechat_redirect)。因为以空格作为分隔符，所以有一些文件名或者其他意义的字符串内含有空格的时候，xargs可能会误判。简单来说，xargs的作用是给其他命令传递参数，是构建单行命令的重要组件之一。

之所以要用到xargs，是因为很多命令不支持使用管道|来传递参数，例如：

```
find /sbin -perm +700 | ls -l         # 这个命令是错误,因为标准输入不能作为ls的参数
find /sbin -perm +700 | xargs ls -l   # 这样才是正确的
```

## 命令格式

```
xargs [OPTIONS] [COMMAND]
```

## 选项说明

注意，长选项的强制性参数对于短选项也是强制的。

```
-0, --null
  #如果输入的stdin含有特殊字符，例如反引号 `、反斜杠 \、空格等字符时，xargs将它还原成一般字符。为默认选项
-a, --arg-file=FILE
  #从指定的文件FILE中读取输入内容而不是从标准输入
-d, --delimiter=DEL
  #指定xargs处理输入内容时的分隔符。xargs处理输入内容默认是按空格和换行符作为分隔符，输出arguments时按空格分隔
-E EOF_STR
  #EOF_STR是end of file string，表示输入的结束
-e, --eof[=EOF_STR]
  #作用等同于 -E 选项，与 -E 选项不同时，该选项不符合POSIX标准且EOF_STR不是强制的。如果没有EOF_STR则表示输入没有结束符
-I REPLACE_STR
  #将xargs输出的每一项参数单独赋值给后面的命令，参数需要用指定的替代字符串REPLACE_STR代替。REPLACE_STR可以使用{} $ @ 等符号，其主要作用是当xargs command后有多个参数时，调整参数位置。
  例如备份以 txt 为后缀的文件：find . -name "*.txt" | xargs -I {}  cp {} /tmp/{}.bak
-i, --replace[=REPLACE_STR]
  #作用同 -I 选项，参数 REPLACE_STR 是可选的，缺省为 {}。建议使用 -I 选项，因为其符合 POSIX
-L MAX_LINES
  #限定最大输入行数。隐含了 -x 选项
-l, --max-lines[=MAX_LINES]
  #作用同 -L 选项，参数 MAX_LINES 是可选的，缺省为 1。建议使用 -L 选项，因为其符合 POSIX 标准
-n, --max-args=MAX_ARGS
  #表示命令在执行的时候一次使用参数的最大个数
-o, --open-tty
  #在执行命令之前，在子进程中重新打开stdin作为/dev/TTY。如果您希望xargs运行交互式应用程序，这是非常有用的
-P, --max-procs=MAX_PROCS
  #每次运行最大进程；缺省值为 1。如果MAX_PROCS为 0，xargs将一次运行尽可能多的进程。一般和-n或-L选项一起使用
-p, --interactive
  #当每次执行一个argument的时候询问一次用户
--process-slot-var=NAME
  #将指定的环境变量设置为每个正在运行的子进程中的唯一值。一旦子进程退出，将重用该值。例如，这可以用于初始负荷分配方案
-r, --no-run-if-empty
  #当 xargs 的输入为空的时候则停止xargs，不用再去执行后面的命令了。为默认选项
-s, --max-chars=MAX_CHARS
  #命令行的最大字符数，指的是xargs后面那个命令的最大命令行字符数，包括命令、空格和换行符。每个参数单独传入xargs后面的命令
--show-limits
  #显示操作系统对命令行长度的限制
-t， --verbose
  #先打印命令到标准错误输出，然后再执行
-x, --exit
  #配合 -s 使用，当命令行字符数大于 -s 指定的数值时，退出 xargs
--help
  #显示帮助信息并退出
--version
  #显示版本信息并退出
```

## 常用示例

1、将 [Shell](http://mp.weixin.qq.com/s?__biz=MzI0MDQ4MTM5NQ==&mid=2247503009&idx=2&sn=6d3caafaae6807fd7b4cc0f330acd713&chksm=e918a9bdde6f20ab93883e315938916387ffa1ba315deda523795373c629ed2dde8811362563&scene=21#wechat_redirect) 的特殊字符反引号还原为一般字符。

```
echo '`0123`4 56789' | xargs -t echo
echo `0123`4 56789 
`0123`4 56789
```

如果直接进行如下操作，会报无法找到命令 01234 的错误，因为反引号在 Shell 中会将 01234 作为一个命令来执行，但是 01234 不是一个命令。-t 表示先打印命令，然后再执行。[值得收藏！Linux系统常用命令速查手册](http://mp.weixin.qq.com/s?__biz=MzI0MDQ4MTM5NQ==&mid=2247500085&idx=2&sn=5455a50a3ec0fc0a69a7cc910a316ebe&chksm=e918a429de6f2d3f4ba700653b387459cb16dd4bf34cd42b4b0ef53c2dd91a53ce40abf0f2a2&scene=21#wechat_redirect)

```
echo `01234` 56789
-bash: 01234: command not found
```

2、设置 xargs 读入参数时的结束标识，以逗号结束。这里要注意结束标志必须要是单独的字段，即以空格或者换行符分隔的字段。

```
echo 01234 , 56789 | xargs -E ","
01234
```

3、使用 rm、mv 等[命令](http://mp.weixin.qq.com/s?__biz=MzI0MDQ4MTM5NQ==&mid=2247503846&idx=2&sn=0237dd02ce72740f5e1293dffe061b08&chksm=e918aafade6f23ec43dc2009bdf1f88396b6e252af86bdfe544209e95afe184fd5c3a0fe761a&scene=21#wechat_redirect)同时操作多个文件时，有时会报 “argument list too long” 参数列表过长的错误，此时可以使用 xargs 来解决。xargs 将标准输入的字符串分隔后，作为参数传递给后面的[命令](http://mp.weixin.qq.com/s?__biz=MzI0MDQ4MTM5NQ==&mid=2247502217&idx=1&sn=f6ee7fef395fc81ae2a451f98a1af566&chksm=e918ac95de6f25835a9be61e09a4f0f0c935b8e7fae19eb4451269d0f3c75bd896aac682ab90&scene=21#wechat_redirect)。例如，给当前目录的所有文件添加后缀名。

```
ls | xargs -t -i mv {} {}.bak

# 选择符合条件的文件
ls | grep -E "201701|201702|201703" | xargs -I {} mv {} {}.bak
```

4、设置命令行的最大字符数。参数默认一个一个单独传入命令中执行。

```
echo "01234 56789" | xargs -t -s 11
echo 01234 
01234
echo 56789 
56789
```

5、设置标准输入中每次多少行作为命令的参数，默认是将标准输入中所有行的归并到一行一次性传给命令执行。

```
echo -e "01234\n56789\n01234" | xargs -t -L 2 echo
echo 01234 56789 
01234 56789
echo 01234 
01234
```

6、将文件内容以空格分隔合并为一行输出。

```
# 列出文件内容
cat test.txt
a b c d e
f g h i j 
k l m n o

# 多行输入合并为一行输出
cat test.txt | xargs
a b c d e f g h i j k l m n o
```

7、与ps、grep、awk和kill结合，强制终止指定进程。

```
ps -ef | grep spp | awk '{printf "%s ",$2}' | xargs kill -9
1
```

ps -ef|grep spp用于查找包含 spp 的进程，awk '{printf "%s ",$2,FNR}将目标进程 ID 打印输出，xargs kill -9则将目标进程 ID 作为参数传递给kill -9用于杀死进程。