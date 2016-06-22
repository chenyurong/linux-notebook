# 脚本安装

脚本安装就是软件编写者写好一个shell脚本或者java脚本，你只需要输入一些简单的信息便可直接安装。这种安装方式方便简单，类似于Wins下的安装方式。

下面以webmin的安装为例讲解脚本安装的步骤：

```bash
#tar -xzvf webmin-1.530.tar.gz  //解压缩
#cd webmin-1.530
#vi README //通过查看说明文件，可以查看安装的脚本是哪个（或者是INSTALL帮助文件）
#./setup.sh  //执行安装脚本（通过README帮助文件查找得知）
```