Mnemosyne
=========
Mnemosyne has three main objectives:

1. Provide immutable persistence for [hpfeeds](hpfeeds https://redmine.honeynet.org/projects/hpfeeds/wiki).
2. Normalization of data to enable sensor agnostic analysis.
3. Expose the normalized data through a RESTful API.

## Preliminary REST API
*GET /hpfeeds*
```json
{
"hpfeeds": [
    {
        "ident": "2l3if@hp8",
        "timestamp": "2012-12-26T20:01:46.908000",
        "normalized": true,
        "_id": "5deadbeef0e0f7b874e8088d",
        "payload": "<payload>",
        "channel": "glastopf.events"
    },
    {
        "ident": "2l3if@hp8",
        "timestamp": "2012-12-26T20:05:32.773000",
        "normalized": false,
        "_id": "50db57aadfe0f7b8deadbeef",
        "payload": "<payload>",
        "channel": "glastopf.events"
    }]
}
```

*GET /hpfeeds/\<hpfeed_id\>*
```json
{
    "ident": "2l3if@hp8",
    "timestamp": "2012-12-26T19:49:22.212000",
    "normalized": true,
    "_id": "50dbdeadbeeff7b874e806ba",
    "payload": "<payload>",
    "channel": "glastopf.events"
}
```

*GET /session/\<session_id\>*
```json
{
    "_id": "50db96f9dfe0f7aacb57c7af",
    "protocol": "http",
    "hpfeed_id": "50da20b2dfe0f7b0b5fb37d1",
    "timestamp": "2012-12-25T15:52:45",
    "source_ip": "123.123.222.21",
    "source_port": 57462,
    "destination_port": 80,
    "honeypot": "Glastopf",
    "session_http": {
        "request": {
            "body": "",
            "header": "{\"Accept-Language\": \"en-gb,en;q=0.5\", \"Proxy-Connection\": \"Keep-Alive\", \"Accept\": \"text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8\", \"User-Agent\": \"Mozilla/5.0 (Windows; U; Windows NT 6.1; en-US; rv:1.9.2.28) Gecko/20120306 Firefox/3.6.28 (.NET CLR 3.5.30729)\", \"Accept-Charset\": \"ISO-8859-1,utf-8;q=0.7,*;q=0.7\", \"Host\": \"kratlusker.zz\", \"Pragma\": \"no-cache\", \"Cache-Control\": \"no-cache\", \"Accept-Encoding\": \"deflate, gzip\"}",
            "host": "gameframe.net",
            "verb": "GET",
            "url": "http://kratlusker.zz/page.php?id='"
        }
    }
}
```

*GET /sessions/protocols*
```json
{"protocols": [{"count": 680, "protocol": "http"},
               {"count": 125, "protocol": "ssh"},
               {"count": 74,  "protocol": "imap"}]}
```

*GET /urls*
```json
{
"urls": [
    {
        "url": "http://inutterod.ru/count22.php",
        "_id": "50db96fa2c533872c1ba0d26",
        "hpfeed_ids": [
            "50da8260dfe0f7b2c68c2fde"
        ]
    },
    {
        "url": "http://www.jotto-to.xx/images/M_images/t?%0D?",
        "_id": "50db96fa2c533872c1ba0d27",
        "hpfeed_ids": [
            "50dad02bdfe0f7b4f48cd434",
            "50dad0a6dfe0f7b4f48cd435"
        ]
    }
}
```



### Sample console output
```
2012-12-21 23:14:54,804 (connect) connecting to hpfeeds.honeycloud.net:10000
2012-12-21 23:14:54,811 (insert_normalized) Inserting normalized item origination from hpfeeds with id: 1
2012-12-21 23:14:54,876 (connect) info message name: @hp2, rand: '7\x004\xe3'
2012-12-21 23:15:08,187 (on_message) Persisted message from glastopf.events (payload size: 10566)
2012-12-21 23:15:09,816 (insert_normalized) Inserting normalized item origination from hpfeeds with id: 2
2012-12-21 23:15:51,402 (on_message) Persisted message from glastopf.events (payload size: 9885)
2012-12-21 23:15:51,486 (on_message) Persisted message from glastopf.events (payload size: 9863)
2012-12-21 23:15:52,427 (on_message) Persisted message from glastopf.events (payload size: 10343)
2012-12-21 23:15:52,541 (on_message) Persisted message from glastopf.events (payload size: 9102)
2012-12-21 23:15:54,847 (insert_normalized) Inserting normalized item originating from hpfeeds with id: 3
2012-12-21 23:15:54,855 (insert_normalized) Inserting normalized item originating from hpfeeds with id: 4
2012-12-21 23:15:54,861 (insert_normalized) Inserting normalized item originating from hpfeeds with id: 5
2012-12-21 23:15:54,866 (insert_normalized) Inserting normalized item originating from hpfeeds with id: 6
```
