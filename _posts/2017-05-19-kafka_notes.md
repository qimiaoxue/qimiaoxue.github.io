---
layout: post
title:  Kafka producer workflow 
date:   2017-05-19 15:30:52 +0800
categories: kafka producer server 
tag: kafka 
---

* content
{:toc}


### launch kafka server 
```
$ sudo  /opt/Kafka/kafka_2.10-0.10.0.1/bin/kafka-server-start.sh /opt/Kafka/kafka_2.10-0.10.0.1/config/server.properties
```

### launch local tornado server 
```
$ python server.py 
```
### use postman to tornado server sending post request

```
setting X-API-KEY=test in headers
data
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
### check kafka server topic 
```
$ sudo /opt/Kafka/kafka_2.10-0.10.0.1/bin/kafka-topics.sh --list --zookeeper localhost:2181
```
### check kafka receive data 
```
sudo /opt/Kafka/kafka_2.10-0.10.0.1/bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic event --from-beginning
```
### check kafka receive data count 
```
$ sudo /opt/Kafka/kafka_2.10-0.10.0.1/bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic event -b
```

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
