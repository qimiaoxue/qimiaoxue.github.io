---
layout: post
title:  "Welcome to xueyan!"
date:   2017-05-13 22:41:52 +0800
categories: git merge
tag: git 
---

* content
{:toc}

Git Merge
------------------------

# view diffs when having merge conflict

`git log --merge -p file1.txt`

# Strategies
1. Resolve strategy
2. Recursive strategy
    
    * -X Ours
    * -X Theirs
    * -X ignore-space-change
    * -X ignore-all-space
    * -X ignore-space-at-eol

    ```
    git cherry-pick -Xtheirs d9e3b4
    ```
    
3. Octopus strategy
4. Ours strategy

# Set merge conflict to show ancestor

```
git config --global merge.conflictstyle diff3
```

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
