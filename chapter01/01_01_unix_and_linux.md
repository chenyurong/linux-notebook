# Unix & Linux

## Unix

UNIX操作系统是一个强大的多用户、多任务操作系统，支持多种处理器架构，按照操作系统的分类，属于分时操作系统。

最早于1969年由AT&T的贝尔实验室开发，现在其商标权由国际开放标准组织所拥有，只有符合单一UNIX规范的UNIX系统才能使用UNIX这个名称，否则只能称为类UNIX（UNIX-like）。 

现在市面上的类Unix系统（Unix发型版本）用得最多的系统有：

- **Linux**：Linux是林纳斯·托瓦兹根据BSD进行不断补充而得出的。
- **Solaris**：隶属SUN公司，在互联网领域用得最多，现已并入Oracle。
- **AIX**：隶属IBM公司，一般用于中高端领域，比如：银行、金融领域。
- HP-UX：隶属HP公司，是惠普9000系列服务器的操作系统。
- IRX：隶属硅谷图形公司SGI。
- BSD：是Unix的衍生系统，在1977至1995年间由加州大学伯克利分校开发和发布的。

一般来说现在用得最多的系统是：**Linux、Solaris、AIX**。

## Linux

Linux是一套免费使用和自由传播的类Unix操作系统，Linux继承了Unix以网络为核心的设计思想，是一个性能稳定的多用户网络操作系统。

Linux操作系统由林纳斯·托瓦兹于 1991 年 10 月 5 日对外发布。Linux存在着许多不同的Linux版本，但它们都使用了Linux内核。

### Linux发型版本

Linux的主要发行版本有两个系列：**Redhat系列和Debian系列**。

**Readhat系列**

redhat系列主要包括以下几个发型版本：redhat、fedora、centos、linux红旗、gentoo linux等。

**Debian系列**

debian系列主要包括以下几个发型版本：debian，ubuntu、knoppix等。

**如何查看系统对应版本？**

- 显示操作系统相关信息

```bash
[nobody@bj10 log]$ uname -a
Linux bj10.190 2.6.32-431.el6.x86_64 #1 SMP Fri Nov 22 03:15:09 UTC 2013 x86_64 x86_64 x86_64 GNU/Linux
```

- 显示内核版本

```bash
[nobody@bj10 log]$ cat /proc/version
Linux version 2.6.32-431.el6.x86_64 (mockbuild@c6b8.bsys.dev.centos.org) (gcc version 4.4.7 20120313 (Red Hat 4.4.7-4) (GCC) ) #1 SMP Fri Nov 22 03:15:09 UTC 2013
```

- 显示发型版本

```bash
[nobody@bj10 log]$ cat /etc/issue
CentOS release 6.5 (Final)
Kernel \r on an \m
```

<!-- 

**AT&T公司**

AT&T公司（American Telephone & Telegraph），是一家美国电信公司，美国第二大移动运营商，创建于1877年，主要提供通信相关服务，其前身是由电话发明人贝尔于1877年创建的美国贝尔电话公司。AT&T公司旗下的**贝尔实验室**，其致力于研究晶体管、激光器等基础研究，一共获得8项诺贝尔奖。贝尔实验室于1996年脱离AT&T而并入新成立的公司——朗讯科技。

-->