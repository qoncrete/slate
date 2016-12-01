---
title: API Reference

language_tabs:
  - shell

search: true
---

# Introduction

Welcome to [Qoncrete.com api](https://qoncrete.com).

We will introduce you with some examples how to work with our api. Anything you
can achieve with the UI can be done directly from our API.

All the action are performed via `http[s]://api.qoncrete.com/v2/`

# Authentication

For any Authentication method, we strongly encourage your to do it via HTTPS.

## JWT (Json Web Token)

Qoncrete UI is only a graphic representation of the API. You can authenticate
your client by generating a JWT. However, the new generated token will only be
available for 48 hours.

```shell
curl -i -X POST -H 'Content-type: application/json' \
    -d '{ "email": "test@email.com", "password": "123456" }' \
    'https://api.qoncrete.com/v2/user/login'

HTTP/1.1 200 OK
Server: nginx
Date: Thu, 10 Nov 2016 04:27:17 GMT
Content-Type: application/json; charset=utf-8
Content-Length: 261
Connection: keep-alive
Vary: Accept-Encoding
Vary: Origin
X-UA-Compatible: IE=Edge

{
    "token": "<jwt token>"
}
```

# Authorization

## JWT (Json Web Token)

```shell
curl -X GET \
    -H 'Content-type: application/json' \
    -H 'Authorization:Bearer <jwt token>'\
    'https://api.qoncrete.com/v2/source'

```

## Token


```shell
curl -X GET \
    -H 'Content-type: application/json' \
    'https://api.qoncrete.com/v2/source?token=<TOKEN>'

```

# Registration

```shell
curl -X POST \
    -H 'Content-type: application/json' \
    -d '{ "email": "", "password": "", "passwordConfirm": "" }'
    'https://api.qoncrete.com/v2/user/register'

```


# Source

As source is an element that can store reports.

## List

```shell
curl -X GET \
    -H 'Content-type: application/json' \
    'https://api.qoncrete.com/v2/source?token=<TOKEN>'

{
    [source objects]
}
```

## One

```shell
curl -X GET \
    -H 'Content-type: application/json' \
    'https://api.qoncrete.com/v2/source/<SOURCE_ID>?token=<TOKEN>'

{
    "_id":"8b5229f1-ee8f-4b23-9b4c-6149288cfb51",
    "db":"",
    "userId":"22c4f102-7f64-460c-8d37-0862638cbc58",
    "name":"DATATEST",
    "created":"2016-10-12T10:57:11.324+08:00",
    "modified":"2016-10-12T10:57:11.324+08:00",
    "active":true,
    "ready":1,
    "reports":[ "<REPORT_ID>" ],
    "reportList":[ {report object} ],
    "sourceVersion":0,
    "maxQuery":-1,
    "_extra": {
        "count":2,
        "size":29
    },
    "rawttl":"",
    "writeMinStat":0,
    "writeAccess": true,
    "readAccess": true
}
```

## Create

```shell
curl -X POST \
    -H 'Content-type: application/json' \
    -d '{ "name": "", "rawttl": "" }'
    'https://api.qoncrete.com/v2/source?token=<TOKEN>'
```

## Modify

```shell
curl -X PUT \
    -H 'Content-type: application/json' \
    -d '{ "name": "", "rawttl": "" }'
    'https://api.qoncrete.com/v2/source/<SOURCE_ID>?token=<TOKEN>'
```

## Delete

```shell
curl -X DELETE \
    -H 'Content-type: application/json' \
    'https://api.qoncrete.com/v2/source/<SOURCE_ID>?token=<TOKEN>'
```

## Share List

```shell
curl -X GET \
    -H 'Content-type: application/json' \
    'https://api.qoncrete.com/v2/source/<SOURCE_ID>/share?token=<TOKEN>'

{
    [source share objects]
}
```

## Share One

```shell
curl -X GET \
    -H 'Content-type: application/json' \
    'https://api.qoncrete.com/v2/source/<SOURCE_ID>/share/<SHARE_ID>?token=<TOKEN>'

{
    "_id": "",
	"ownerId": "",
	"userId": "",
	"userEmail": "",
	"sourceId": "",
	"readAccess": true,
	"writeAccess": false
}
```

## Share Create

```shell
curl -X POST \
    -H 'Content-type: application/json' \
    -d '{ "email": "" }'
    'https://api.qoncrete.com/v2/source/<SOURCE_ID>/share?token=<TOKEN>'
```

## Share Delete

```shell
curl -X DELETE \
    -H 'Content-type: application/json' \
    'https://api.qoncrete.com/v2/source/<SOURCE_ID>/share/<SHARE_ID>?token=<TOKEN>'
```

## Daily statistics

```shell
curl -X GET \
    -H 'Content-type: application/json' \
    'https://api.qoncrete.com/v2/source/<SOURCE_ID>/stat/daily?token=<TOKEN>'
```

# Report

## List

```shell
curl -X GET \
    -H 'Content-type: application/json' \
    'https://api.qoncrete.com/v2/source/<SOURCE_ID>/report?token=<TOKEN>'

{
    [report object]
}
```

## One

```shell
curl -X GET \
    -H 'Content-type: application/json' \
    'https://api.qoncrete.com/v2/source/<SOURCE_ID>/report/<REPORT_ID>?token=<TOKEN>'

{
    "_id":"433e40f7-5d44-4363-96ad-517670fead31",
    "sourceId":"8b5229f1-ee8f-4b23-9b4c-6149288cfb51",
    "name":"my report",
    "period":"1M",
    "created":"2016-10-14T14:44:44.983+08:00",
    "modified":"2016-10-19T16:06:38.27+08:00",
    "reportVersion":4,
    "active":true,
    "preprocess":[ preprocess object ],
    "filter":[ filter object ],
    "groupBy":[ groupBy object ],
    "values":[ value object ],
    "_extra":null,
    "storageVersion":0,
    "dataSize":32768,
    "startingPoint":"",
    "writeAccess": true,
    "readAccess": true
}
```

## Create

```shell

# REPORT_JSON
# {
#     "name": "",
#     "period": "",
#     "preprocess":[ preprocess object ],
#     "filter":[ filter object ],
#     "groupBy":[ groupBy object ],
#     "values":[ value object ]
# }

curl -X POST \
    -H 'Content-type: application/json' \
    -d '<REPORT_JSON>' \
    'https://api.qoncrete.com/v2/source/<SOURCE_ID>/report?token=<TOKEN>'
```

## Modify

```shell

# REPORT_JSON
# {
#     "name": "",
#     "period": "",
#     "preprocess":[ preprocess object ],
#     "filter":[ filter object ],
#     "groupBy":[ groupBy object ],
#     "values":[ value object ]
# }

curl -X PUT \
    -H 'Content-type: application/json' \
    -d '<REPORT_JSON>' \
    'https://api.qoncrete.com/v2/source/<SOURCE_ID>/report/<REPORT_ID>?token=<TOKEN>'
```

## Delete

```shell
curl -X DELETE \
    -H 'Content-type: application/json' \
    'https://api.qoncrete.com/v2/source/<SOURCE_ID>/report/<REPORT_ID>?token=<TOKEN>'
```

## Share List

```shell
curl -X GET \
    -H 'Content-type: application/json' \
    'https://api.qoncrete.com/v2/source/<SOURCE_ID>/report/<REPORT_ID>/share?token=<TOKEN>'

{
    [report share objects]
}
```

## Share One

```shell
curl -X GET \
    -H 'Content-type: application/json' \
    'https://api.qoncrete.com/v2/source/<SOURCE_ID>/report/<REPORT_ID>/<SHARE_ID>?token=<TOKEN>'

{
    "_id": "",
	"ownerId": "",
	"userId": "",
	"userEmail": "",
	"sourceId": "",
	"reportId": "",
	"readAccess": true,
	"writeAccess": false
}
```

## Share Create

```shell
curl -X POST \
    -H 'Content-type: application/json' \
    -d '{ "email": "" }'
    'https://api.qoncrete.com/v2/source/<SOURCE_ID>/report/<REPORT_ID>/share?token=<TOKEN>'
```

## Share Delete

```shell
curl -X DELETE \
    -H 'Content-type: application/json' \
    'https://api.qoncrete.com/v2/source/<SOURCE_ID>/report/<REPORT_ID>/share/<SHARE_ID>?token=<TOKEN>'
```

# Report Preprocess

```json
{
	"key": "",
	"injectKey": "",
	"func": "",
	"param1": "",
	"param2": ""
}
```

# Report Filter

```json
{
    "key": "",
    "condition": "",
    "type": "",
    "comparator": {}
}
```

# Report GroupBy

```json
{
	"name": "",
	"keys": [""]
}
```

# Report Value

```json
{
    "name": "",
    "key": "",
    "type": "",
	"mustExists": true
}
```

# MergeReports

```shell

# MERGE_REPORTS_JSON
# {
#   "mainReport":
#   {
#       "sid": "bc3528df-ac20-4278-b31f-0b719e6251eb",
#       "rid": "bfc8bf58-277b-44bf-8364-e1f3913aed2c",
#       "at": "2016-11-26T16:00:00Z",
#       "search": "sth",
#       "klen": 1,
#       "limit": 10,
#       "cursor": 10,
#       "sort": -1,
#       "order": "asc",
#       "filters": [{"value": 0, "comp": ">=", "to": 10}]
#   },
#   "subReports":
#   [
#       {
#           "sid": "bc3528df-ac20-4278-b31f-0b719e6251eb",
#           "rid": "395b9554-a9b0-47a9-88a4-8b74e3c5e533",
#           "search": "",
#           "timeDiff": "-2d"
#       }
#   ]
# }

curl -X POST \
    -H 'Content-type: application/json' \
	-d '<MERGE_REPORTS_JSON>' \
	'https://api.qoncrete.com/v2/query/mergereports'
```


# Scan

## ScanDates

```shell

# SCAN_DATES_JSON
# {
#     "from":"2016-06-30T00:14:00.000Z",
#     "to":"2016-06-30T00:14:00.000Z",
#     "keys": []
#	  "sort": "asc",
#	  "count": 20,
#     "filters": [{"value": 0, "comp": ">=", "to": 10}]
# }

curl -X POST \
    -H 'Content-type: application/json' \
	-d '<SCAN_DATES_JSON>' \
	'https://api.qoncrete.com/v2/source/<SOURCE_ID>/report/<REPORT_ID>/scandates'
```

## ScanDatesExport

```shell

curl -X GET \
	'https://api.qoncrete.com/v2/source/<SOURCE_ID>/report/<REPORT_ID>/scandates/export?query=<SCAN_DATES_JSON>'
```

## ScanKeys

```shell

# SCAN_KEYS_JSON
# {
#     "at":"2016-06-30T00:14:00.000Z",
#     "klen": 1,
#     "keySearch": "",
#     "count": 20,
#     "cursor": 20,
#	  "sortType": "asc",
#     "sortPos": 1
#     "filters": [{"value": 0, "comp": ">=", "to": 10}]
# }

curl -X POST \
    -H 'Content-type: application/json' \
	-d '<SCAN_KEYS_JSON>' \
	'https://api.qoncrete.com/v2/source/<SOURCE_ID>/report/<REPORT_ID>/scankeys'
```         

## ScanKeysExport

```shell

curl -X GET \
	'https://api.qoncrete.com/v2/source/<SOURCE_ID>/report/<REPORT_ID>/scankeys/export?query=<SCAN_KEYS_JSON>'
```

# Store

## List

```shell

curl -X GET \
	'https://api.qoncrete.com/v2/store/:kind'

 {
	[ stored items]	 
 }

```

## One

```shell

curl -X GET \
    'https://api.qoncrete.com/v2/store/:kind/:id'

	{
		"id": "xxxxxx",
		"name": "test",
		"value": "{\"f1\": \"field one\", \"f2\": 10}"
	}
```         

## Create

```shell

# ITEM_JSON 
# {
#     "name":"test",
#     "value": "{\"f1\": \"field one\", \"f2\": 10}"
# }

curl -X POST \
	-H 'Content-type: application/json' \
    -d '<ITEM_JSON>' \
    'https://api.qoncrete.com/v2/store/:kind'
```

## Modify

```shell

# UPDATE_ITEM_JSON
# {
#	  "id": "abdcde-dedfa-dfad-sfds",
#     "name":"test",
#     "value": "{\"f1\": \"field one\", \"f2\": 10}"
# }

curl -X PUT \
    -H 'Content-type: application/json' \
	-d '<UPDATE_ITEM_JSON>' \
	'https://api.qoncrete.com/v2/store/:kind'
```

## Delete

```shell

curl -X DELETE \
    'https://api.qoncrete.com/v2/store/:kind/:id'
```

# Token

## List

```shell
curl -X GET \
    -H 'Content-type: application/json' \
	'https://api.qoncrete.com/v2/token?token=<TOKEN>'

	{
		[token objects]
	}
```

## One

```shell
curl -X GET \
    -H 'Content-type: application/json' \
	'https://api.qoncrete.com/v2/token/<TOKEN_ID>?token=<TOKEN>'

		{
			    "_id":"97b8a203-f4ca-4832-8469-d2188e4c487g1",
				"userId":"22c4f102-7f64-460c-8d37-0862638cbc51",
				"name":"Manage",
				"access":7,
				"created":"2016-08-05T14:32:44.463+08:00",
				"modified":"2016-09-08T12:54:19.587+08:00"
		}
```

## Create

```shell
curl -X POST \
    -H 'Content-type: application/json' \
	-d '{ "name": "", "access": "" }'
	'https://api.qoncrete.com/v2/token?token=<TOKEN>'
```

## Modify

```shell
curl -X PUT \
    -H 'Content-type: application/json' \
	-d '{ "name": "", "access": "" }'
	'https://api.qoncrete.com/v2/source/<SOURCE_ID>?token=<TOKEN>'
```

## Delete

```shell
curl -X DELETE \
    -H 'Content-type: application/json' \
	'https://api.qoncrete.com/v2/source/<SOURCE_ID>?token=<TOKEN>'
```

