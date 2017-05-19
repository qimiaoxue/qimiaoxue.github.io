---
layout: post
title:  apache benchmark workflow 
date:   2017-05-19 15:50:52 +0800
categories: apache benchmark 
tag: apache 
---

* content
{:toc}


### install apache benchmark 
```
$ sudo apt-get update
$ sudo apt-get install apache2-utils
```
### apache benchmark references 
```
https://kuntalchandra.wordpress.com/2015/10/10/install-apache-bench-ubuntu-14-04/
https://www.cyberciti.biz/tips/howto-performance-benchmarks-a-web-server.html
http://httpd.apache.org/docs/2.2/programs/ab.html
```

### common use (get requests) 
```
$ ab -n 100 -c 10 http://www.baidu.com/
```
### post requests (form)

```
$ ab -T 'application/x-www-form-urlencoded' -n 10 -p post.data http://localhost:8080/
ps: post.data: url=my_encoded_url&csrfmiddlewaretoken=my_tokensetting X-API-KEY=test in headers
```
### post requests (json)
```
$ ab -T 'application/json' -H 'X-API-KEY:test' -n 10000 -c 100 -p post.json http://localhost:8888/api/v1/track
ps:
post.json:
{
    "anonymous_id": "c262df1d-f17c-4317-843c-2f4629f1abdc",
    "message_id": "358d20e0-cc50-49f5-94ce-86fb6dabec72",
    "event": "course.enrollment.activated",
    "properties": {
      "course_id": "test_course"
    },
    "timestamp": "2017-03-13T10:10:00.000Z",
    "type": "track",
    "user_id": "test_user",
    "customer_id": 1,
    "project_id": 1
}
```

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
