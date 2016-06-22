# 源代码包管理

下面以proftd源代码包的安装为例，说明源代码包的安装步骤：

```bash
#tar -xzvf proftpd-1.3.3d.tar.gz  //解压缩包
#cd proftpd-1.3.3d
#.configure --prefix=/usr/local/proftd //配置信息，prefix参数指定源代码包安装位置
#make        //编译
#make install  //安装
```

其中配置环节是让软件去收集系统的信息，以便后面进行编译操作。