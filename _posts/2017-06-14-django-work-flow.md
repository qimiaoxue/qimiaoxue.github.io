---
layout: post
title:  django workflow_1
date:   2017-06-14 10:30:52 +0800
categories: python django cors 
tag: django 
---

* content
{:toc}


### django-cors-middle 

### reference 
```
https://github.com/zestedesavoir/django-cors-middleware
https://pypi.python.org/pypi/django-cors-middleware/1.3.1
```

### install 
```
$ pip install django-cors-middleware
```
### setting.py
```
INSTALLED_APPS = ('corsheaders',)

MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',
    'django.middleware.common.CommonMiddleware',
]

CORS_ORIGIN_ALLOW_ALL = True
```

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
