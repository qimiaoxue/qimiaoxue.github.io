---
layout: post
title:  Git common CMD 
date:   2017-05-14 00:15:52 +0800
categories: git  
tag: git 
---

* content
{:toc}


### cancel local changes 
```
$ git checkout -- filename 
```
### creat new branch (from current branch) 
```
$ git checkout -b branchname 
```
### creat new branch (from specific branch)  
```
$ git checkout -b branchname master 
```
### change branch  
```
$ git checkout branchname 
```

### merge
```
$ git merge branchname 
$ git merge --no-ff branchname (merge commit)
```

### rebase 
```
$ git rebase branchname 
$ git rebase --continue (need git add)
$ git rebase --abort 
```
### pull (same branch)
```
$ git pull --rebase
```
### push (same branch)
```
$ git push 
$ git push -u origin develop (set up stream of local develop to remote develop)
```


[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/


[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
