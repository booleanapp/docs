---
title: GET /stats
sidebar: mydoc_sidebar
permalink: v1_stats.html
---

## GET /stats

Used to get statistics on sent surveys.

### URL parameters

|Parameter|Required|Requirements|
|---------|--------|------------|
|start_date|Yes|YYYY:MM:DD (time assumed midnight) or YYYY:MM:DDTHH:MM:SS. Timezone inferred from survey setting.|
|end_date|Yes|YYYY:MM:DD (time assumed midnight) or YYYY:MM:DDTHH:MM:SS. Timezone inferred from survey setting.|
|interval|No|Day or Week or Month.|

#### Example

```
GET /stats?start_date=2017-05-23&end_date=2017-05-24&pretty
```

##### Response

```json
HTTP/1.1 200
{
  "request_id": "c7ab31ca-a668-44f6-a32d-171f382890dc",
  "success": true,
  "errors": [],
  "response": {
    "surveys_requested": [
      {
        "interval_date": "2017-05-23T00:00:00+05:30",
        "epoch": 1495477800,
        "count": 12
      },
      {
        "interval_date": "2017-05-24T00:00:00+05:30",
        "epoch": 1495564200,
        "count": 0
      },
      {
        "interval_date": "2017-05-25T00:00:00+05:30",
        "epoch": 1495650600,
        "count": 0
      }
    ],
    "surveys_throttled": [
      {
        "interval_date": "2017-05-23T00:00:00+05:30",
        "epoch": 1495477800,
        "count": 8
      },
      {
        "interval_date": "2017-05-24T00:00:00+05:30",
        "epoch": 1495564200,
        "count": 0
      },
      {
        "interval_date": "2017-05-25T00:00:00+05:30",
        "epoch": 1495650600,
        "count": 0
      }
    ],
    "surveys_send_failed": [
      {
        "interval_date": "2017-05-23T00:00:00+05:30",
        "epoch": 1495477800,
        "count": 0
      },
      {
        "interval_date": "2017-05-24T00:00:00+05:30",
        "epoch": 1495564200,
        "count": 0
      },
      {
        "interval_date": "2017-05-25T00:00:00+05:30",
        "epoch": 1495650600,
        "count": 0
      }
    ],
    "surveys_sent": [
      {
        "interval_date": "2017-05-23T00:00:00+05:30",
        "epoch": 1495477800,
        "count": 4
      },
      {
        "interval_date": "2017-05-24T00:00:00+05:30",
        "epoch": 1495564200,
        "count": 0
      },
      {
        "interval_date": "2017-05-25T00:00:00+05:30",
        "epoch": 1495650600,
        "count": 0
      }
    ],
    "bounced": [
      {
        "interval_date": "2017-05-23T00:00:00+05:30",
        "epoch": 1495477800,
        "count": 0
      },
      {
        "interval_date": "2017-05-24T00:00:00+05:30",
        "epoch": 1495564200,
        "count": 0
      },
      {
        "interval_date": "2017-05-25T00:00:00+05:30",
        "epoch": 1495650600,
        "count": 0
      }
    ],
    "responses": [
      {
        "interval_date": "2017-05-23T00:00:00+05:30",
        "epoch": 1495477800,
        "count": 2
      },
      {
        "interval_date": "2017-05-24T00:00:00+05:30",
        "epoch": 1495564200,
        "count": 1
      },
      {
        "interval_date": "2017-05-25T00:00:00+05:30",
        "epoch": 1495650600,
        "count": 0
      }
    ],
    "positive_responses": [
      {
        "interval_date": "2017-05-23T00:00:00+05:30",
        "epoch": 1495477800,
        "count": 2
      },
      {
        "interval_date": "2017-05-24T00:00:00+05:30",
        "epoch": 1495564200,
        "count": 1
      },
      {
        "interval_date": "2017-05-25T00:00:00+05:30",
        "epoch": 1495650600,
        "count": 0
      }
    ],
    "negative_responses": [
      {
        "interval_date": "2017-05-23T00:00:00+05:30",
        "epoch": 1495477800,
        "count": 0
      },
      {
        "interval_date": "2017-05-24T00:00:00+05:30",
        "epoch": 1495564200,
        "count": 0
      },
      {
        "interval_date": "2017-05-25T00:00:00+05:30",
        "epoch": 1495650600,
        "count": 0
      }
    ]
  }
}
```


#### Error codes

|Code|Message|Description|
|----|-------|-----------|
|1001|Invalid format|Invalid format of data.|
|1006|Required property missing|One or more required property is missing.|
|1009|Invalid Value|Value is incorrect for a given field.|