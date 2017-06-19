---
layout: post
title:  Redis hashes 
date:   2017-06-18 22:30:52 +0800
categories: redis hashes 
tag: python 
---


### Redis 

### hashes 
```
hash是一个string类型的field和value的映射表
它的添加，删除操作都是O(1)
hash 特别适合存储对象，比对象的每个字段存成单个string类型，将一个对象存储
在hasb类型中会占用更少的内存，并且更方便的存储整个对象

```

### hset
```
给某个表的某个字段设置某个值
redis 127.0.0.1:6379>hset user:1 name xy 
(integer) 1
redis 127.0.0.1:6379>hget user:1 name 
'xy'
```
### hsetnx 
```
给某个表的某个字段设置某个值
如果key不存在，则先创建
如果key存在，则返回0
redis 127.0.0.1:6379>hsetnx user:2 name xj 
(integer) 1 
redis 127.0.0.1:6379>hsetnx user:2 name xm 
(integer) 0 
redis 127.0.0.1:6379>hget user:2 name 
'xj'
```
### hmset 
```
批量给一个表多个key设置多个值
成功返回OK, 失败返回0, 代表没有任何值被设置
redis 127.0.0.1:6379>hmset user:3 name xx age 25 
OK
redis 127.0.0.1:6379>hget user:3 name
'xx'
redis 127.0.0.1:6379>hget user:3 age 
25
```
### hmget 
```
批量获取给一个表多个field的值
redis 127.0.0.1:6379>hmget user:3 name age 
1) 'xx'
2) 25 
```
### hincrby 
```
incrby对某一个键进行自增, incrby可设置自增值
redis 127.0.0.1:6379>hincrby user:3 age 5 
(integer) 30 
redis 127.0.0.1:6379>hget user:3 age 
"30"
```
### hexists 
```
判断某张表的某个字段是否存在，存在返回1, 不存在返回0
redis 127.0.0.1:6379>hexists user:3 age 
(integer) 1 
redis 127.0.0.1:6379>hexists user:3 sex 
(integer) 0 
```
### hlen 
```
返回hash表里面所有field的数量
redis 127.0.0.1:6379>hlen user:3  
(integer) 3 
```
### hdel 
```
删除hash表里的某个字段
redis 127.0.0.1:6379>hdel user:3 name 
(integer) 1 
```

### hkeys 
```
返回hash的所有的字段
redis 127.0.0.1:6379>hkeys user:3 
1) age 
```
### hvals 
```
返回hash所有的value
redis 127.0.0.1:6379>hvals user:3 
1) "xm"
2) 28
3) 1
```
### hgetall 
```
返回hash所有的value
redis 127.0.0.1:6379>hgetall user:4 
1) "name"
2) "xm"
3) "age" 
4) 28 
5) "sex" 
6) male 
```


[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
