# Shell应用技巧

## Shell

查看系统中所有shell，其中bash是许多unix系统都有的。

```bash
cat /etc/shells
```
## 命令补全

命令补齐允许用户输入用户名开始的若干个字母后，按`<Tab>`键补齐用户名。

## 命令历史

按方向键`↑`和`↓`可查找以前执行过的命令，用`history`命令可以显示命令列表。

```bash
$~ yurongchan$ history
    1  ifconfig
    2  history
```

用`!序号`可以执行已经该序号所对应的命令。如我要执行上面的`ifconfig`命令，那么我执行下面的命令即可：

```bash
$ !1
ifconfig
lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384
	options=3<RXCSUM,TXCSUM>
	inet6 ::1 prefixlen 128 
	inet 127.0.0.1 netmask 0xff000000 
	inet6 fe80::1%lo0 prefixlen 64 scopeid 0x1 
	nd6 options=1<PERFORMNUD>
gif0: flags=8010<POINTOPOINT,MULTICAST> mtu 1280
……
```

## 命令别名

定义别名让操作更容易记忆。范例：

```bash
alias copy = cp
alias xrm = "rm -r"
```

如果别名包含的是一组命令组合，那么必须用引号包起来。

**查看别名信息**

```bash
$alias
```

**删除别名**

```bash
$unalias copy
```

## 输入/输出重定向

同标准I/O一样，Shell对于每一个进程预先定义3个文件描述子（0、1、2）。分别对应于：

- 0（STDIN）标准输入
- 1（STDOUT）标准输出
- 2（STDERR）标准错误输出

**输出重定向 > >>**

```bash
$ls -l /tmp > /tmp.msg      //将命令执行结果显示到文件里，会覆盖原来的文件
$date >> /tmp.msg       //>> 表示追加信息到文件中。
```

**输入重定向**

```bash
wall < /etc/motd
```

**错误输出重定向**

```bash
cp -R /usr/backup/usr.bak 2 > /bak.error
```

## 管道

## 命令连接符

## 命令替换符

## 快捷键

```
ctrl + l   清屏
ctrl + u   删除光标前所有内容
```




