## 命令简介

alias 命令用来设置指令的别名。

unalias 命令是一个 shell 命令，可从定义的别名列表中删除每个名称，主要用于删除一个或多个别名 、删除全部已定义的别名。

## 语法格式

```
alias [OPTIONS]
unalias  [OPTIONS] name [name ...]
#指定要删除的一个或多个已定义的别名。
```

## 选项说明

alias 选项

```
-p  #打印已经设置的命令别名
```

unalias 选项

```
-a  #删除全部已定义的别名
```

## 应用举例

查看系统当前设置的别名列表

```
[root@centos7 ~]# alias
alias cp='cp -i'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l.='ls -d .* --color=auto'
alias ll='ls -l --color=auto'
alias ls='ls --color=auto'
alias mv='mv -i'
alias rm='rm -i'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
```

设置与删除别名

```
[root@centos7 ~]# alias df='df -h'
[root@centos7 ~]# df
Filesystem               Size  Used Avail Use% Mounted on
devtmpfs                 475M     0  475M   0% /dev
tmpfs                    487M     0  487M   0% /dev/shm
tmpfs                    487M  7.7M  479M   2% /run
tmpfs                    487M     0  487M   0% /sys/fs/cgroup
/dev/mapper/centos-root   17G  2.0G   16G  12% /
/dev/sda1               1014M  167M  848M  17% /boot
tmpfs                     98M     0   98M   0% /run/user/0
[root@centos7 ~]# unalias df
[root@centos7 ~]# df
Filesystem              1K-blocks    Used Available Use% Mounted on
devtmpfs                   486068       0    486068   0% /dev
tmpfs                      497840       0    497840   0% /dev/shm
tmpfs                      497840    7788    490052   2% /run
tmpfs                      497840       0    497840   0% /sys/fs/cgroup
/dev/mapper/centos-root  17811456 2009976  15801480  12% /
/dev/sda1                 1038336  170064    868272  17% /boot
tmpfs                       99572       0     99572   0% /run/user/0
```

