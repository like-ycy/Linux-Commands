## 命令简介

tail 显示文件内容的尾部，默认也是显示指定文件的末尾10行。

tail 命令还可以查看文件实时写入的数据，例如，我们常用它来查看应用运行的日志文件，可以动态实时显示应用运行所产生的日志，便于排错或查看应用运行是否正常。

## 命令格式

```
tail [选项] [链接文件名]
tail [OPTION] [LINKNAME]
```

## 选项说明

```
-f #显示文件最新追加的内容，实时动态展示一个文件的写入数据
-n<N> #输出文件的尾部N（N位数字）行内容。
--pid=<进程号>  #与“-f”选项配合，如果指定进程号的进程终止后，自动退出
-v  #显示文件名信息
-q  #不显示文件名信息
--help     #打印帮助信息
--version  #打印版本信息
```

## 应用举例

```
#显示文件mingongge从第200行至文件末尾的内容
tail -n +200 mingongge
 
#显示文件mingongge的最后100个字符
[root@centos7 ~]# tail -c 100 mingongge
 
#显示mingongge.log最后的250行
[root@centos7 ~]# tail -250 mingongge.log 
 
#实时展示mingongge.log文件的写入数据
[root@centos7 ~]# tail -f mingongge.log 

#带文件名与不带文件名举例
[root@centos7 ~]# tail -v -n 10 /etc/passwd /etc/shadow
==> /etc/passwd <==
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody:/:/sbin/nologin
systemd-network:x:192:192:systemd Network Management:/:/sbin/nologin
dbus:x:81:81:System message bus:/:/sbin/nologin
polkitd:x:999:998:User for polkitd:/:/sbin/nologin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
chrony:x:998:996::/var/lib/chrony:/sbin/nologin

==> /etc/shadow <==
operator:*:17834:0:99999:7:::
games:*:17834:0:99999:7:::
ftp:*:17834:0:99999:7:::
nobody:*:17834:0:99999:7:::
systemd-network:!!:18494::::::
dbus:!!:18494::::::
polkitd:!!:18494::::::
sshd:!!:18494::::::
postfix:!!:18494::::::
chrony:!!:18494::::::
[root@centos7 ~]# tail -q -n 10 /etc/passwd /etc/shadow
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody:/:/sbin/nologin
systemd-network:x:192:192:systemd Network Management:/:/sbin/nologin
dbus:x:81:81:System message bus:/:/sbin/nologin
polkitd:x:999:998:User for polkitd:/:/sbin/nologin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
chrony:x:998:996::/var/lib/chrony:/sbin/nologin
operator:*:17834:0:99999:7:::
games:*:17834:0:99999:7:::
ftp:*:17834:0:99999:7:::
nobody:*:17834:0:99999:7:::
systemd-network:!!:18494::::::
dbus:!!:18494::::::
polkitd:!!:18494::::::
sshd:!!:18494::::::
postfix:!!:18494::::::
chrony:!!:18494::::::
```