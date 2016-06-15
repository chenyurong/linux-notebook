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
$ls -l /tmp 0> /tmp.msg      //将命令执行结果显示到文件里，会覆盖原来的文件
$date 0>> /tmp.msg       //>> 表示追加信息到文件中。
```

其中上面的0可以省略，即相当于下面的命令：

```bash
$ls -l /tmp > /tmp.msg      
$date >> /tmp.msg 
```

**输入重定向**

```bash
wall 1< /etc/motd
```

其中上面的1可以省略，即：

```bash
wall < /etc/motd
```

**错误输出重定向**

```bash
cp -R /usr /backup/usr.bak 2> /bak.error
```

`2>`表示把出错信息保存到`/bak.error`中。这里的2就无法省略了。

## 管道

将一个命令的输出传送给另一个命令，作为另一个命令的输入。

使用方法：`命令1 | 命令2 | 命令3 ..... | 命令n`

范例：

```bash
ls -l /etc | more
ls -l /etc | grep init 
ls -l /etc | grep init | wc -l
```

`wc`命令用来是一个计数器，而`-l`表示行数，所以`wc -l`用来计算行数。

## 命令连接符

**顺序执行符号 ;**

用`;`间隔的各命令按顺序依次执行

**逻辑与执行符号 &&**

用`&&`间隔的命令表示前后命令的执行存在逻辑与关系，只有`&&`前面的命令执行成功后，它后面的命令才被执行。

**逻辑或执行符号 ||**

用`||`间隔的命令表示前后命令的执行存在逻辑或关系，只有`||`前面的命令执行失败后，它后面的命令才被执行。

## 命令替换符

将一个命令的输出作为另一个命令的参数，其格式为：命令1 `命令2`，其执行效果与管道是颠倒的。

```bash
ls -l `which touch`
```

## 快捷键

```
ctrl + l   清屏
ctrl + u   删除光标前所有内容
```




