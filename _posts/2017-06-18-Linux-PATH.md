---
layout: post
title:  Linux $ PATH 
date:   2017-06-17 10:30:52 +0800
categories: python Linux PATH 
tag: python 
---


### Linux PATH 

### bin 
```
所有二进制应用程序可放的位置
```

### PATH  
```
在命令行输入一个命令的时候，系统通过path里面存的目录来寻找此命令的二进制文件
再通过此二进制文件来操作
```
### 得到root身份搜寻的路径 
```
$ echo $PATH

结果为由分号（：）隔开的目录组成
/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/sbin:/usr/local/bin:/sbin
:/bin:/usr/sbin:/usr/bin:/root/bin
```
### 把一个目录增加到PATH路径的方法
```
$ PATH="$PATH":/root
```
### 相同的命令在不同的目录中，哪个目录中的命令先被执行
```
PATH里面哪个目录先被查询，则哪个目录下的命令先执行
```
### 总结
```
1. 不同身份使用者默认的PATH不同, 能够随意运行的命令业不同
2. PATH是可以修改的，所以一般使用者还是可以通过修改某些位于/sbin
或者/usr/bin下的命令来查询
3. 使用绝对或者相对路径指定某个命令的档名来运行，比搜寻PATH来的正确
4. 命令应该要放置在正确的目录下，运行才会比较方便
5. 本目录(.)最好不要放在PATH当中
```

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
