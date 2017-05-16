---
layout: post
title:  ddt & mock demo testcase 
date:   2017-05-16 11:15:52 +0800
categories: ddt mock testcase  
tag: ddt 
---

* content
{:toc}


### ddt & mock demot testcase
```
import json
from itertools import product
import ddt
from mock import patch
from tornado.testing import AsyncHTTPTestCase
from server import make_server


@ddt.ddt
class ValidatorTest(AsyncHTTPTestCase):
    headers = {
        'X-API-KEY': 'test'
    }

    def setUp(self):
        super(ValidatorTest, self).setUp()
        patcher = patch('server.KAFKA_CLIENT')
        self.addCleanup(patcher.stop)
        self.mock_client = patcher.start()

    def get_app(self):
        return make_server()

    @property
    def data(self):
        return {
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
        }.copy()

    def post(self, url, data):
        body = json.dumps(data)
        return self.fetch(url, method='POST', body=body, headers=self.headers)

    @ddt.data(
        *product(
            ('/api/v1/track', '/api/v1/identify', '/api/v1/model'),
            ('message_id', 'timestamp', 'properties', 'context')
        )
    )
    @ddt.unpack
    def test_success_post(self, url, key):
        data = self.data
        data.pop(key)
        response = self.post(url, data)
        self.assertEqual(response.code, 200)
        self.mock_client.send.assert_called_once()

    @ddt.data(
        ('/api/v1/track', 'event', 'event is required.'),
        ('/api/v1/track', 'user_id', 'user_id or anonymous_id is required.'),
        ('/api/v1/identify', 'user_id', 'user_id or anonymous_id is required.'),
        ('/api/v1/model', 'model', 'model is required.'),
        ('/api/v1/model', 'user_id', 'user_id or anonymous_id is required.'),
    )
    @ddt.unpack
    def test_invalid_post(self, url, key, reason):
        data = self.data
        data.pop(key)
        response = self.post(url, data)
        self.assertEqual(response.reason, reason)
        self.mock_client.send.assert_not_called()

    @ddt.data(
        ('/api/v1/batch', 'type', 'type is required.'),
    )
    @ddt.unpack
    def test_batch_required_args_post(self, url, key, reason):
        data = self.data
        data.pop(key)
        response = self.post(url, data)
        self.assertEqual(response.code, 400)
        self.assertEqual(response.reason, reason)

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

    @ddt.data(
        ('/api/v1/track', 'Authorization failed')
    )
    @ddt.unpack
    def test_invalid_clotho_headers(self, url, reason):
        body = json.dumps(self.data)
        response = self.fetch(url, method="POST", body=body)
        self.assertEqual(response.reason, reason)

    def test_kafka_error(self):
        from kafka.errors import KafkaTimeoutError
        self.mock_client.send.side_effect = KafkaTimeoutError
        url = '/api/v1/track'
        body = json.dumps(self.data)
        response = self.fetch(url, method='POST', body=body, headers=self.headers)
        self.assertEqual(response.code, 503)

    """
    Need covered codes:
    clotho.py: 8 test invalid clotho headers
    server.py: 93-94 raise socket error in MagicMock
    server.py 233-247 test the batch handler
    """
```


[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
