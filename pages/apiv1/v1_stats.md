---
title: GET /stats
sidebar: mydoc_sidebar
permalink: v1_stats.html
---

## GET /stats

Used to get statistics on sent surveys.

### URL parameters

|Parameter|Required|Requirements|Description|
|---------|--------|------------|-----------|
|start_date|Yes|YYYY:MM:DD (time assumed midnight) or YYYY:MM:DDTHH:MM:SS. Timezone inferred from project setting.|The start date of the statistics to retrieve|
|end_date|Yes|YYYY:MM:DD (time assumed midnight) or YYYY:MM:DDTHH:MM:SS. Timezone inferred from project setting.|The end date of the statistics to retrieve|
|interval|No|Day or Week or Month|Method to group statistics. Default is day.|

#### Example

GET `https://api.booleanapp.com/v1/stats?start_date=2016-08-16&end_date=2016-08-17&interval=day`

##### Response

```json
HTTP/1.1 200
{
  "request_id": "85879157-09f4-41a4-a882-048ec28c1c50",
  "errors": [],
  "response": {
    "surveys_requested": [
      {
        "interval_date": "2016-08-15T00:00:00Z",
        "epoch": 1471219200,
        "count": 0
      },
      {
        "interval_date": "2016-08-16T00:00:00Z",
        "epoch": 1471305600,
        "count": 100
      }
    ],
    "surveys_throttled": [
      {
        "interval_date": "2016-08-15T00:00:00Z",
        "epoch": 1471219200,
        "count": 0
      },
      {
        "interval_date": "2016-08-16T00:00:00Z",
        "epoch": 1471305600,
        "count": 0
      }
    ],
    "surveys_send_failed": [
      {
        "interval_date": "2016-08-15T00:00:00Z",
        "epoch": 1471219200,
        "count": 0
      },
      {
        "interval_date": "2016-08-16T00:00:00Z",
        "epoch": 1471305600,
        "count": 0
      }
    ],
    "surveys_sent": [
      {
        "interval_date": "2016-08-15T00:00:00Z",
        "epoch": 1471219200,
        "count": 0
      },
      {
        "interval_date": "2016-08-16T00:00:00Z",
        "epoch": 1471305600,
        "count": 100
      }
    ],
    "bounced": [
      {
        "interval_date": "2016-08-15T00:00:00Z",
        "epoch": 1471219200,
        "count": 0
      },
      {
        "interval_date": "2016-08-16T00:00:00Z",
        "epoch": 1471305600,
        "count": 0
      }
    ],
    "responses": [
      {
        "interval_date": "2016-08-15T00:00:00Z",
        "epoch": 1471219200,
        "count": 0
      },
      {
        "interval_date": "2016-08-16T00:00:00Z",
        "epoch": 1471305600,
        "count": 92
      }
    ],
    "positive_responses": [
      {
        "interval_date": "2016-08-16T00:00:00Z",
        "epoch": 1471305600,
        "count": 60
      }
    ],
    "negative_responses": [
      {
        "interval_date": "2016-08-16T00:00:00Z",
        "epoch": 1471305600,
        "count": 32
      }
    ]
  }
}
```

#### Response glossary

|Attribute|Description|
|---------|-----------|
|surveys_requested|Surveys requested within the time frame|
|surveys_throttled|Surveys not sent due to throttling of surveys sent per unique email. (<i>write details about logic for throttling and setting in dashboard</i>)|
|surveys_send_failed|Surveys not sent (<i>write list of possible reasons here.</i>)|
|surveys_sent|Surveys sent within the time frame|
|bounced|Surveys which bounced within the time frame|
|responses|Responses within the time frame. Please note that this will include responses received for surveys sent before the time frame|
|positive_responses|Positive responses received within the time frame. Please note that this will include responses received for surveys sent before the time frame.|
|negative_responses|Negative responses received within the time frame. Please note that this will include responses received for surveys sent before the time frame.|


#### Error codes

|Code|Message|Description|
|----|-------|-----------|
|1001|Invalid format|Invalid format of data|
|1006|Required property missing|One or more required property is missing|
|1009|Invalid Value|Value is incorrect for given field.|