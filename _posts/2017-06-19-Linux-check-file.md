---
layout: post
title:  Linux file 
date:   2017-06-19 20:30:52 +0800
categories: linux file 
tag: linux 
---


### linux 查看文件内容 

### cat 
```
$ cat [options] filename

从第一行开始显示文件内容

cat 选项与参数：
-A: 相当於 -vET 的整合选项，可列出一些特殊字符而不是空白而已； 
-b  ：列出行号，仅针对非空白行做行号显示，空白行不标行号！
-E  ：将结尾的断行字节 $ 显示出来；
-n  ：列印出行号，连同空白行也会有行号，与 -b 的选项不同；
-T  ：将 [tab] 按键以 ^I 显示出来；
-v  ：列出一些看不出来的特殊字符
```

### tac  
```
$ tac [options] filename

与cat相反，是从最后一行开始显示文件内容
```
### nl 
```
$ nl [options] filename

添加行号查询

选项与参数：
-b  ：指定行号指定的方式，主要有两种：
      -b a ：表示不论是否为空行，也同样列出行号(类似 cat -n)；
      -b t ：如果有空行，空的那一行不要列出行号(默认值)；
-n  ：列出行号表示的方法，主要有三种：
      -n ln ：行号在萤幕的最左方显示；
      -n rn ：行号在自己栏位的最右方显示，且不加 0 ；
      -n rz ：行号在自己栏位的最右方显示，且加 0 ；
-w  ：行号栏位的占用的位数。

用法有:
$ nl filename
     1	{
     2	    "anonymous_id": "c262df1d-f17c-4317-843c-2f4629f1abdc",
     3	    "message_id": "358d20e0-cc50-49f5-94ce-86fb6dabec72",
     4	    "event": "course.enrollment.activated",
     5	    "timestamp": "2017-03-13T10:10:00.000Z",
     6	    "type": "track",
     7	    "user_id": "test_user22",
     8	    "project_id": 1
     9	}

$ nl -b a filename
     1	{
     2	    "anonymous_id": "c262df1d-f17c-4317-843c-2f4629f1abdc",
     3	    "message_id": "358d20e0-cc50-49f5-94ce-86fb6dabec72",
     4	    "event": "course.enrollment.activated",
     5	    "timestamp": "2017-03-13T10:10:00.000Z",
     6	    "type": "track",
     7	    "user_id": "test_user22",
     8	    "project_id": 1
     9	}

$ nl -b a -n ln filename
1     	{
2     	    "anonymous_id": "c262df1d-f17c-4317-843c-2f4629f1abdc",
3     	    "message_id": "358d20e0-cc50-49f5-94ce-86fb6dabec72",
4     	    "event": "course.enrollment.activated",
5     	    "timestamp": "2017-03-13T10:10:00.000Z",
6     	    "type": "track",
7     	    "user_id": "test_user22",
8     	    "project_id": 1
9     	}

$ nl -b a -n rn filename
     1	{
     2	    "anonymous_id": "c262df1d-f17c-4317-843c-2f4629f1abdc",
     3	    "message_id": "358d20e0-cc50-49f5-94ce-86fb6dabec72",
     4	    "event": "course.enrollment.activated",
     5	    "timestamp": "2017-03-13T10:10:00.000Z",
     6	    "type": "track",
     7	    "user_id": "test_user22",
     8	    "project_id": 1
     9	}

$ nl -b a -n rz -w 3 filename 
001	{
002	    "anonymous_id": "c262df1d-f17c-4317-843c-2f4629f1abdc",
003	    "message_id": "358d20e0-cc50-49f5-94ce-86fb6dabec72",
004	    "event": "course.enrollment.activated",
005	    "timestamp": "2017-03-13T10:10:00.000Z",
006	    "type": "track",
007	    "user_id": "test_user22",
008	    "project_id": 1
009	}
```
### more(一页一页翻动) 
```
$ more /etc/man.config 

1. 空白键 (space)：代表向下翻一页；
2. Enter         ：代表向下翻『一行』；
3. /字串         ：代表在这个显示的内容当中，向下搜寻『字串』这个关键字；
4. :f            ：立刻显示出档名以及目前显示的行数；
5. q             ：代表立刻离开 more ，不再显示该文件内容。
6. b 或 [ctrl]-b ：代表往回翻页，不过这动作只对文件有用，对管线无用。
```
### less(一页一页翻动) 
```
$ less /etc/man.config

1. 空白键 (space)：代表向下翻一页；
2. [pagedown]：向下翻动一页；
3. [pageup]  ：向上翻动一页；
4. /字串     ：向下搜寻『字串』的功能；
5. ?字串     ：向上搜寻『字串』的功能；
6. n         ：重复前一个搜寻 (与 / 或 ? 有关！)
7. N         ：反向的重复前一个搜寻 (与 / 或 ? 有关！)
8. q         ：离开 less 这个程序；
```
### head(取出前面几行) 
```
$ head [-n number] filename

选项与参数：
-n  ：后面接数字，代表显示几行的意思

$ head filename
默认显示前十行

$ head -n 20 /etc/man.config
显示前二十行

上面范例的-n -100时，代表列前的所有行数， 但不包括后面100行。举例来说，
/etc/man.config共有141行，则上述的命令『head -n -100 /etc/man.config』
就会列出前面41行，后面100行不会列印出来了
```
### tail(取出后面几行) 
```
$ tail [-n number] filename

选项与参数：
-n  ：后面接数字，代表显示几行的意思
-f  ：表示持续侦测后面所接的档名，要等到按下[ctrl]-c才会结束tail的侦测
默认显示最后的十行

$ tail -n 20 /etc/man.config
显示后二十行

$ tail -n +100 /etc/man.config
列出100行以后的数据

$ tail -f /var/log/messages
持续侦测/var/log/messages的内容
```
### od(查看非纯文字文件）
```
$ od [-t TYPE] filename

选项或参数：
-t  ：后面可以接各种『类型 (TYPE)』的输出，例如：
      a       ：利用默认的字节来输出；
      c       ：使用 ASCII 字节来输出
      d[size] ：利用十进位(decimal)来输出数据，每个整数占用 size bytes ；
      f[size] ：利用浮点数值(floating)来输出数据，每个数占用 size bytes ；
      o[size] ：利用八进位(octal)来输出数据，每个整数占用 size bytes ；
      x[size] ：利用十六进位(hexadecimal)来输出数据，每个整数占用 size bytes ；

$ od -t c /usr/bin/passwd
将/usr/bin/passwd的内容使用ASCII方式来展现

$ od -t oCc/etc/issue
将/etc/issue这个文件的内容以8进位列出储存值与ASCII的对照表
```
### touch(将某个文件日期修订为目前(mtime 与 atime))
```
三个时间的意义

modification time(mtime)
当该文件的『内容数据』变更时，就会升级这个时间！内容数据指的是文件的内容，
而不是文件的属性或权限喔！

status time(ctime)
当该文件的『状态 (status)』改变时，就会升级这个时间，举例来说，像是权限
与属性被更改了，都会升级这个时间啊。 

access time (atime)：
当『该文件的内容被取用』时，就会升级这个读取时间 (access)。
举例来说，我们使用 cat 去读取 /etc/man.config ， 就会升级该文件的 atime 了。

$ ls -l /etc/man.config
-rw-r--r-- 1 root root 4617 Jan  6  2007 /etc/man.config

$ ls -l --time=atime /etc/man.config
-rw-r--r-- 1 root root 4617 Sep 25 17:54 /etc/man.config

$ ls -l --time=ctime /etc/man.config
-rw-r--r-- 1 root root 4617 Sep  4 18:03 /etc/man.config

touch [-acdmt] filename

选项与参数：
-a  ：仅修订 access time；
-c  ：仅修改文件的时间，若该文件不存在则不创建新文件；
-d  ：后面可以接欲修订的日期而不用目前的日期，也可以使用 --date="日期或时间"
-m  ：仅修改 mtime ；
-t  ：后面可以接欲修订的时间而不用目前的时间，格式为[YYMMDDhhmm]

case1: 
新建一个空的文件并观察时间
$ cd /tmp
$ touch testtouch
$ ls -l testtouch
-rw-r--r-- 1 root root 0 Sep 25 21:09 testtouch

case2:
复制一个文件，并查看时间
$ cp -a ~/.bashrc bashrc
$ ll bashrc; ll --time=atime bashrc; ll --time=ctime bashrc
-rw-r--r-- 1 root root 176 Jan  6  2007 bashrc  <==这是 mtime
-rw-r--r-- 1 root root 176 Sep 25 21:11 bashrc  <==这是 atime
-rw-r--r-- 1 root root 176 Sep 25 21:12 bashrc  <==这是 ctime

case3:
将日期调整为两天前
$ touch -d "2 days ago" bashrc
ll bashrc; ll --time=atime bashrc; ll --time=ctime bashrc
-rw-r--r-- 1 root root 176 Sep 23 21:23 bashrc
-rw-r--r-- 1 root root 176 Sep 23 21:23 bashrc
-rw-r--r-- 1 root root 176 Sep 25 21:23 bashrc

case4:
将bashrc的日期改为2017/6/15/ 2:02
$ touch -t 1706150202 bashrc
$ ll bashrc; ll --time=atime; ll --time=ctime bashrc
-rw-r--r-- 1 root root 176 Sep 15  2007 bashrc
-rw-r--r-- 1 root root 176 Sep 15  2007 bashrc
-rw-r--r-- 1 root root 176 Sep 25 21:25 bashrc
```


[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
