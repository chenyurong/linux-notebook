# Linux帮助命令

## man 命令

语法：man [命令或配置文件]
功能描述：获得帮助信息

**查看命令的帮助**

```bash
$man ls
NAME
       find - search for files in a directory hierarchy

SYNOPSIS
       find [-H] [-L] [-P] [path...] [expression]

DESCRIPTION
       This  manual  page  documents  the GNU version of find.  GNU find searches the directory tree rooted at each
       given file name by evaluating the given expression from left to right, according to the rules of  precedence
       (see  section  OPERATORS),  until the outcome is known (the left hand side is false for and operations, true
       for or), at which point find moves on to the next file name.
……
```

其调用more进行浏览帮助文档，这时候可以用more命令的操作。

**查看配置文件的帮助**

```bash
$man services
NAME
       services - Internet network services list

DESCRIPTION
       services is a plain ASCII file providing a mapping between friendly textual names for internet services, and
       their underlying assigned port numbers and protocol types. Every networking program should  look  into  this
       file  to  get  the  port  number (and protocol) for its service.  The C library routines getservent(3), get-
       servbyname(3), getservbyport(3), setservent(3), and endservent(3) support querying this file from  programs.
……
```

如果同时有一个passwd的命令和一个passwd的配置文件，你想要看的是命令的帮助，而不是passwd配置文件的帮助，这时候，你只需要执行下面的命令就可以。

```bash
$man passwd
NAME
       passwd - change user password
……
```

但如果你要看的是配置文件的帮助呢？这时候你应该执行下面的指令：

```bash 
$man 5 passwd
NAME
       passwd - password file

DESCRIPTION
       Passwd  is  a  text file, that contains a list of the system's accounts, giving for each account some useful
       information
```

因为在Linux中有很多种帮助，命令的帮助类型是1，而配置文件的帮助类型是5，所以上面的指令就可以查看配置文件的帮助。如果不指定，那么默认就显示命令的帮助类型。也就是说下面两条指令的结果是一样的：

```bash
$man passwd
$man 1 passwd
```

## info 命令

- 所在路径：/usr/bin/info
- 语法：info [任何关键字]
- 功能描述：获得帮助信息

**获取ls指令的帮助信息**

```bash
info ls
```

info 命令与 man 命令没有什么区别，只是其信息呈现方式稍有区别。

## whatis 命令

- 所在路径：
- 语法：whatis [关键字]
- 功能描述：显示命令的用途

whatis 命令只显示命令最简单的用法，而不像man和info一样显示得那么全面。

```bash
$whatis ls
cd (1) [bashbuiltins] - bash built-in commands, see bash(1)
cd (n)               - Change working directory
cd (1p)              - change the working directory
```

如果只需要选项内容，则可以用：[命令] --help

```bash
//列出ls命令的选项内容
ls --help
```

如果要查看跟某个配置文件有关的所有信息可以用：apropos [配置文件名]，相当于`man -k`。

```bash
$apropos table
pnm2ppa (1)          - convert portable anymap (PNM) images to HP's PPA printer format.
pax (1p)             - portable archive interchange
crontab (5)          - tables for driving cron (ISC Cron V4.1)
getdtablesize (2)    - get descriptor table size
```

## makewhatis 命令

用于建立whatis和apropos搜索使用的数据库，当使用这两个命令发生错误时，就是whatis database没有建立

## help 命令

查看shell内置命令的帮助。如果一个命令是shell内置命令，那么用man命令是无法查看到其帮助命令的，这时候就要用help命令查看。

**查看cd的帮助命令**

```bash
$help cd
cd: cd [-L|-P] [dir]
     Change the current directory to DIR.  The variable $HOME is the
    default DIR.  The variable CDPATH defines the search path for
    the directory containing DIR.  Alternative directory names in CDPATH
    are separated by a colon (:).
……
```

**查看pwd的帮助命令**

```bash
$help pwd
pwd: pwd [-LP]
     Print the current working directory.  With the -P option, pwd prints
    the physical directory, without any symbolic links; the -L option
    makes pwd follow symbolic links.
```

Linux默认使用的就是BASH，你可以通过`man bash`查看bash的相关信息。

```bash
$man bash
NAME
       bash - GNU Bourne-Again SHell

SYNOPSIS
       bash [options] [file]
……
```









