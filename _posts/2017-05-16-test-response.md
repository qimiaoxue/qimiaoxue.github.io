---
layout: post
title:  tornado test 
date:   2017-05-16 15:40:52 +0800
categories: tornado testcase
tag: test 
---

* content
{:toc}


### get test response 
```
$ response = self.fetch(url, method="POST", body=body, headers=self.headers) 
```
### get response attributes
```
$ response.code 
$ response.reason 
```
### get response body 
```
$ resp_data = json.loads(response.body) 
```
### get response body attrubutes (example) 
```
$ error_count = resp_data['error_count']
$ status = resp_data['status']
```
### assert equal  
```
$ self.assertEqual(error_count, 1) 
$ self.assertEqual(status, 'OK') 
```
### response example 
```
    @ddt.data(
        ('/api/v1/batch', 'invalid_type'),
    )
    @ddt.unpack
    def test_batch_error_count_post(self, url, key):
        batch_data = [
            {
                'message_id': '358d20e0-cc50-49f5-94ce-86fb6dabec72',
                'event': 'course.enrollment.activated',
                'model': 'course',
                'timestamp': '2017-03-13T10:10:00.000Z',
                'user_id': 'test_user',
                'properties': {
                    'key': 'value',
                },
                'type': 'model',
                'context': {},
            },
            {
                'message_id': '358d20e0-cc50-49f5-94ce-86fb6dabec72',
                'event': 'course.enrollment.activated',
                'model': 'course',
                'timestamp': '2017-03-13T10:10:00.000Z',
                'user_id': 'test_user',
                'properties': {
                    'key': 'value',
                },
                'type': key,
                'context': {},
            }
        ]
        data = json.dumps(batch_data)
        response = self.fetch(url, method='POST', body=data, headers=self.headers)
        resp_data = json.loads(response.body)
        self.assertEqual(resp_data['status'], 'ok')
        self.assertEqual(resp_data['error_count'], 1)
        self.assertEqual(response.code, 200)
        self.mock_client.send.assert_called_once()
```

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
