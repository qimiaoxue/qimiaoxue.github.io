---
layout: post
title:  Redis string
date:   2017-06-18 10:30:52 +0800
categories: redis  string
tag: python 
---


### Redis 

### value类型为strings 
```
key 是字符串类型的键值对
string类型是二进制安全的
redis的string可以包含任何数据
jpg图片或者序列化的数据

```

### 命令行常见工作 
```
从网络的角度看, 哪个程序打开了这个端口
netstat -tunpl | grep 6379

对比ps aux | grep 6379
后者是从进程的角度来查看哪个进程打开的网络端口
```
### set 
```
redis 127.0.0.1:6379>set name lijie
OK
redis 127.0.0.1:6379>get name 
'lijie'
redis 127.0.0.1:6379>set name li 
OK
redis 127.0.0.1:6379>get name 
'li'
同一个键下面只能存一个value，如果用了同一个键的话，后者的值将会覆盖前面的值
```
### setnx 
```
设置string类型的value时， 如果key已经存在，返回0，nx代表not exit
redis 127.0.0.1:6379>setnx name lijie
(integer) 0
redis 127.0.0.1:6379>get name 
'li'
```
### setex 
```
设置这个键值对的有效时间
redis 127.0.0.1:6379>setex haircolor 10 red 
OK
redis 127.0.0.1:6379>get haircolor 
'red'
如果10秒到了以后
redis 127.0.0.1:6379>get haircolor 
(nil)
nil代表null
```
### setrange 
```
设置key的value值的子字符串
将lijie的126邮箱替换为gmail邮箱
redis 127.0.0.1:6379>get email 
'lijie@163.com'
redis 127.0.0.1:6379>setrange email 6 gmail.com 
(integer) 15
redis 127.0.0.1:6379>get email 
'lijie@gmail.com'
```
### mset 
```
批量给多个key设置多个值
成功返回OK, 失败返回0, 代表没有任何值被设置
redis 127.0.0.1:6379>mset key1 xy key2 xj 
OK
redis 127.0.0.1:6379>get key1 
'xy'
redis 127.0.0.1:6379>get key2 
'xj'
```

### msetnx 
```
批量给多个key设置多个值
成功返回OK, 失败返回0, 代表没有任何值被设置, 而且不会覆盖已经存在的key
redis 127.0.0.1:6379>msetnx key1 xy key2 xj 
(integer) 0
redis 127.0.0.1:6379>get key1 
(nil)
redis 127.0.0.1:6379>get key2 
(nil)
```
### get 
```
返回key对应的值
```
### getset
```
设置key值, 并返回key的旧值
redis 127.0.0.1:6379>getset key1 xl 
'xy'
redis 127.0.0.1:6379>get key1 
'xl'
设置key的新值，返回key的就值
```
### getrange
```
返回key对应的值的子字符串
redis 127.0.0.1:6379>getrange emil 0 4 
'lijie'
```
### mget
```
一次获取多个key的值，如果key不存在，则返回nil
redis 127.0.0.1:6379>mget key1 key2 key3 key4 key5
1) 'xy'
2) 'xj'
3) 'xx'
4) 'xm'
5) (nil)
```
### incr incrby 
```
incr, incrby均代表自增, incrby可设置自增值
如果key不存在的话，认为value为0
redis 127.0.0.1:6379>set key5 20 
'20'
redis 127.0.0.1:6379>incr key5 
(integer) 21
redis 127.0.0.1:6379>incr key5 
(integer) 22
redis 127.0.0.1:6379>incrby key5 4
(integer) 26
```
### decr decrby 
```
decr, decrby均代表自增, decrby可设置自增值
redis 127.0.0.1:6379>decr key5 
(integer) 23
redis 127.0.0.1:6379>decrby key5 3
(integer) 20
```  
### append 
```
给key对应的值增加字符串
返回字符串的长度
redis 127.0.0.1:6379>append key1 .net 
(integer) 6 
redis 127.0.0.1:6379>get append
'xy.net'
```  
### strlen 
```
返回key对应的值的长度
redis 127.0.0.1:6379>strlen key1 
(integer) 6 
redis 127.0.0.1:6379>get key1
'xy.net'
```  



[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
