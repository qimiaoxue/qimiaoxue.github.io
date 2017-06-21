---
layout: post
title:  linux command permission
date:   2017-06-21 23:41:52 +0800
categories: linx command
tag: command
---

command permission

###  

```
一、让使用者能进入某目录成为『可工作目录』的基本权限为何：

可使用的命令：例如 cd 等变换工作目录的命令；
目录所需权限：使用者对这个目录至少需要具有 x 的权限
额外需求：如果使用者想要在这个目录内利用 ls 查阅档名，则使用者对此目录还需要 r 的权限。

二、使用者在某个目录内读取一个文件的基本权限为何？

可使用的命令：例如本章谈到的 cat, more, less等等
目录所需权限：使用者对这个目录至少需要具有 x 权限；
文件所需权限：使用者对文件至少需要具有 r 的权限才行！

三、让使用者可以修改一个文件的基本权限为何？

可使用的命令：例如 nano 或未来要介绍的 vi 编辑器等；
目录所需权限：使用者在该文件所在的目录至少要有 x 权限；
文件所需权限：使用者对该文件至少要有 r, w 权限

四、让一个使用者可以创建一个文件的基本权限为何？

目录所需权限：使用者在该目录要具有 w,x 的权限，重点在 w 啦！

五、让使用者进入某目录并运行该目录下的某个命令之基本权限为何？

目录所需权限：使用者在该目录至少要有 x 的权限；
文件所需权限：使用者在该文件至少需要有 x 的权限

```

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
