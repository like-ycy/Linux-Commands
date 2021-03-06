## 命令简介

vi/vim 命令是功能强大的纯文本编辑器。vim 是 vi 的加强版，比vi更容易使用。vim编辑器是Unix系统和Linux系统中最标准的编辑器，功能非常强大。它可以执行查找、删除、替换、输出多种文本操作方式。因此，学习vim编辑器也是学习Linux系统过程中比较重要的一个基础部分。

vim编辑器有三种模式，分别如下

```
#命令模式
此种模式下，可能通过移动光标，对字符或行进行删除操作。
#插入模式
在命令模式下，按键盘上字母“i”键即可进行插入模式，只有在此模式下才可以进行文字、字符的输入操作，按“ESC”键退出插入模式（返回命令模式）。
#底行模式
对文件保存或退出，以及设置编辑环境。
```

```
语法格式
vi/vim [选项] [文件]
vi/vim [OPTION] [FILE]
```

## 选项说明

```
+<行号>  #从指定行号的行开始显示文本内容
-b  #以二进制模式打开文件，用于编辑二进制文件和可执行文件
-c<指令>  #多个文件时，先完成第一文件操作，然后再执行指定的指令动作
-d  #以diff模式打开文件，当多个文件编辑时，显示文件差异部分
-l  #使用lisp模式
-m  #取消写文件功能
-M  #关闭修改功能
-n  #不使用缓存功能
-o<文件数目>  #指定同时打开文件的数量
-R  #以只读方式打开文件
-s  #安静模式
```

## vi/vim的基本操作

### 命令模式下光标的移动方法

```
Ctrl+f #屏幕向下移动一页，相当于Page Down
Ctrl+b #屏幕向上移动一页，相当于Page Up
0（数字） #移动到行首位置
$    #移动到行尾位置
gg #移动到第一行
G   #移动到最后一行，与Shift+g功能相同
n<Enter> #光标向下移动n行（n为数字）
```

### 命令模式下搜索与查找

```
/word  #向下查找匹配名为word的字符串
?word  #向上查找匹配名为word的字符串
:n1,n2s/word1/word2/g  #n1,n2为数字，在第n1与n2行之间查找匹配word1的字符串，并将word1全部替换成word2
:1,$s/word1/word2/g  #在第一行与最后一行之间查找匹配word1的字符串，并将word1全部替换成word2
:1,$s/word1/word2/gc #在第一行与最后一行之间查找匹配word1的字符串，并将word1全部替换成word2,替换前进行提示确认是否需要替换
:%s/word1/word2/g   #将匹配word1的内容全替换成word2
```

### 命令模式下删除、复制与粘贴方法

```
yy #复制光标当前所在的行
nyy #复制当前光标所在向下n行（n为数字）
dd #删除光标当前所在的行
ndd #删除当前光标所在向下n行（n为数字）
u  #撤销上一次的操作
p   #将复制的内容粘贴在光标所在的下一行
P  #将复制的内容粘贴在光标所在的上一行
x   #删除光标所在后一个字符
X   #删除光标所有前一个字符
```

### 插入模式下保存与退出

```
:wq  #保存并退出
:wq! #保存交强制退出
:q!  #强制退出不保存
```