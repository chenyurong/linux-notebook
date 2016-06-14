# Linux 解压缩命令

## gzip 压缩命令

- 命令路径：/bin/gzip
- 语法：gzip 选项 [文件]
- 功能：压缩文件
- 压缩后文件格式：.gz

gzip 的两个特点：

- 只能压缩文件，不能压缩目录
- 不保留原文件

```bash
gzip file
```

## gunzip 解压缩命令

- 命令路径：/bin/gunzip
- 语法：gunzip 选项 [文件]
- 功能：解压缩.gz的压缩包

```bash
gunzip file.gz
```

或者你也可以用`gzip -d`来解压缩，它和`gunzip`命令的作用是一样的。

## tar 压缩命令

- 命令路径：/bin/tar
- 语法：tar 选项[cvf] [目录]
	- -c 产生.tar打包文件（必选）
	- -v 显示详细信息（可选）
	- -f 指定压缩后的文件名（必选）
	- -z 打包同时压缩（可选，如果选中则生成.tar.gz的文件）
- 功能描述：打包目录
- 压缩后文件格式：.tar

```bash
$tar -zcvf folder.tar.gz folder
```

NOTE：
- `file [文件]` 命令可以判断文件的类型。
- 有些Unix系统可能并不支持`-z`参数，也就是不能在打包的时候直接压缩。这时候只能先打包，再压缩。

## tar 解压命令

- 语法：tar 选项[zxvf] [文件]
	- -x 解压.tar文件
	- -v 显示详细信息
	- -f 指定压缩文件
	- -z 解压缩

```bash
$tar -zxvf folder.tar.gz
```

## zip 压缩命令

- 所在路径：/usr/bin/zip
- 语法：zip 选项[-r] [压缩后的文件名] [压缩文件或目录]
	- -r 压缩目录
- 功能：压缩文件或目录
- 压缩后文件格式：.zip

```bash
$zip file.txt
$zip -r folder
```

## unzip 解压缩命令

- 所在路径：/usr/bin/unzip
- 语法：gnzip [需要解压缩的文件]
- 功能：解压.zip的压缩文件

```bash
$unzip test.zip
```

## bzip2 压缩命令

- 所在路径：/usr/bin/bzip2
- 语法：bzip2 选项[-k] [需要压缩的文件]
	- -k 产生压缩文件后保留原文件
- 功能描述：压缩文件
- 压缩后文件格式：.bz2

```bash
$bzip2 -k file
```

NOTE：bzip2其实是gzip的升级版，其余gzip的区别是有了-k选项，其他的都一样。bzip2的特点是其压缩比很惊人，适合用来压缩大文件。

## bunzip2 解压缩命令

- 所在路径：/usr/bin/bunzip2
- 语法：bzip2 选项[-k] [需要解压缩的文件]
	- -k 解压缩后保留原文件
- 功能描述：解压缩

```bash
$bunzip2 -k file.bz2
```






 

   



