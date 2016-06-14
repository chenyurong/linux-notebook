# Linux文件搜索命令

## which/whereis 命令

**列出ls命令所在目录以及缩写**

```bash
[chanshuyi@localhost ~]$ which ls
alias ls='ls --color=auto' 
        /bin/ls
```

**列出命令所在目录**

```bash
[chanshuyi@localhost ~]$ whereis ls
ls: /bin/ls /usr/share/man/man1/ls.1.gz /usr/share/man/man1p/ls.1p.gz
```

NOTE：which 和 whereis 的不同之处：Which提供命令的别名信息，Whereis提供命令的帮助信息。上面中的 `alias ls ='ls --color=auto'` 就是ls命令的别名信息，它表示我们按下 `ls` 命令就相当于执行 `ls --color=auto` 命令。`whereis` 中输出部分的文件 `ls.1.gz` 和 `ls.1p.gz` 是指 ls 这个命令的帮助文件。

## find 文件搜索命令

语法：find [搜索路径] [选项] [搜索关键字]

### 按文件名查找

**-name 按文件名查找（`*` 匹配任意字符，包括0个字符，`?` 匹配单个字符）**

```bash
find /etc -name init 
在/etc目录下查找名字为init的文件

find /etc -name init\*     <!-- 这里的星号要加右斜杠转移，否则会出错 -->
在/etc目录下查找所有以init开头的文件

find /etc -name init???
在/etc目录下查找所有以init开头的，并且init后还有3个字符的文字
 
[chanshuyi@localhost Desktop]$ ls
hello.txt  linuxqq-v1.0.2-beta1.i386.rpm  Screenshot.png  test13  test.txt
[chanshuyi@localhost Desktop]$ find . -name test\*    <!-- 这里的星号要加右斜杠转移，否则会出错 -->
./test13
./test13/testfile
./test.txt
```

### 按文件大小查找

**-size 按文件大小查找（+ 表示大于指定大小，- 表示小于指定大小， = 表示刚好等于指定大小）**

单位是block，1个block512Byte，即1KB=2Block，1KB等于两个数据块。

```bash
find / -size +2048
在根目录下查找大小大于100MB的文件
 
find / -size -2048
在根目录下查找大小小于100MB的文件
 
find / -size +2048
在根目录下查找大小刚好等于100MB的文件（一般不用，因为不可能刚好等于100MB）
```

### 根据文件所有者查找

**-user 按所有者查找**

```bash
find /home -user chan
在/home下查找所有者为chan的文件
```

### 根据时间查找

一共有两组共6个选项，分别是：

- ctime/atime/mtime  以天为单位

- cmin/amin/mmin  以分钟为单位 

开头字母的含义：

- c 表示change，指文件的属性（所有者、所属组、权限等）被修改过

- a 表示accesss，表示被访问过

- m 表示modify，表示文件内容被修改过

其中还有：- 表示之内，+ 表示超过。

```bash
find . -mmin -120
在当前目录下查找120分钟内内容被修改过的文件
 
find . -mmin +60
在当前目录下超过60分钟之前内容被修改过的文件（即60分钟内被修改过的文件除外）
 
find . -mtime -2
查找两天之内内容被修改过的文件
 
find . -atime -2
查找两天之内内容被访问过的文件
```

### 按照文件类型查找

type 按文件类型查找（f 表示二进制文件，L 表示软链接文件，D 表示目录）

```bash
find . -type f
查找目录下的所有二进制文件
```

### 根据i节点找

-inum 根据i节点找（i节点是linux中文件的唯一标识）

```bash
//查找到hello.txt文件的i节点是781951
[chanshuyi@localhost Desktop]$ ls -i
781951 hello.txt                      782880 Screenshot.png  782291 test.txt
782823 linuxqq-v1.0.2-beta1.i386.rpm  782587 test13
 
//根据i节点查找
[chanshuyi@localhost Desktop]$ find . -inum 781951
./hello.txt
```

一般情况下用来查找一些文件名为特殊字符的文件，因为这些特殊文件名对于linux来说无法识别（比如“a b” 空间有空格）

## find 连接符

当我们既想以文件名又想用文件大小作为查询条件时，就需要用到find连接符了。

- -a  	逻辑与连接符
- -o 	逻辑或连接符
- -exec 连接执行符
- -ok 	连接执行符

`-ok` 与 `-exec` 的区别就是，ok 在寻找到目标之后会询问你是否进行之前命令中设定的操作，而-exec则不会进行询问。

```bash
--【-exec连接符】找到hello.txt并直接显示它
[chanshuyi@localhost Desktop]$ find . -name hello.txt -exec cat {} \;
Hello, I'm in centos system to write a introduce file to you.
 
--找到hello.txt后，询问用户是否进行对应操作，输入Y/N
[chanshuyi@localhost Desktop]$ find . -name hello.txt -ok cat {} \;
< cat ... ./hello.txt > ? y
Hello, I'm in centos system to write a introduce file to you.
```

## locate 文件搜索命令

```bash
[chanshuyi@localhost Desktop]$ locate hello.txt
/home/chanshuyi/Desktop/hello.txt
```

Locate命令与find命令不同，locate查找是根据系统的文件目录数据库进行查找的，而find是直接去硬盘查找的。因此locate对于刚刚创建的文件或目录会找不到。（因为系统文件目录数据库还未更新）。

你也可以用`updatedb`命令去手动更新系统的文件目录数据库。但locate命令一般只有在linux系统中存在，在其他类型的Unix系统中是不存在的。但是 `updatedb` 指令只有root用户才有权限操作。

## grep 搜索匹配的行

语法：grep [指定字符串] [源文件]

```bash
grep ftp /etc/services
在services文件中搜寻ftp字段，并输出所在的行
```