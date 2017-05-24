---
title: API v1 Introduction
sidebar: mydoc_sidebar
permalink: v1_introduction.html
---

## Root endpoint

```
https://api.booleanapp.com/v1
```

- HTTP is not supported. Only HTTPS.
- The context for all resources in this endpoint is the project indentified by authentication key.

## General requirements

- All API access is over JSON.
- "User-Agent" header is mandatory in all requests.
- "Content-Type : application/json" header is mandatory in all requests.

## Authentication

- Use HTTP BASIC authentication. Use project's API key for username. Leave password empty.

```
curl https://api.booleanapp.com/v1/surveys?pretty -u sk_800089b0657fa1c9dje14af1:
```

## Rate limits

- Max 5000 requests per hour.
- "X-RateLimit-Limit" response header will communicate max requests allowed in current time interval.
- "X-RateLimit-Remaining" response header will communicate available requests remaining in current time interval.
- "X-RateLimit-Reset" response header will communicate time of next limit reset.
- There is also a limit of 60 requests with failed authentication per hour.

```
HTTP/1.1 200 OK
Date: Tue, 23 May 2017 07:45:51 GMT
Content-Type: application/json
Content-Length: 2675
Connection: keep-alive
Vary: Accept-Encoding
X-RateLimit-Limit: 5000
X-RateLimit-Remaining: 4992
X-RateLimit-Reset: 1495526400000
```

## Request size limit

- Max request size allowed is 50 MB.

## Pretty print

- Add parameter "pretty" to get pretty printed response.

```
https://api.booleanapp.com/v1/stats?start_date=2016-07-16&end_date=2016-07-17&interval=day&pretty
```


## Error codes

|HTTP code|Message|
|---------|-------|
|401|Invalid API Key.|
|401|API key not provided.|
|400|Badly formed JSON.|
|404|Non-existent resource is requested.|
|405|Method not allowed.|
|422|Unprocessable request. Due to wrong data type or erroneous expression.|
|429|Too many requests.|


## API Error codes

|Code|Message|Description|
|----|-------|-----------|
|1000|Error|Default error.|
|1001|Invalid format|Invalid format of data.|
|1002|Already exists|Property already exists with different data type.|
|1003|Quota exceeded|Property quota exceeded. Max 50 properties per project.|
|1004|Duplicate request|A survey for same transaction_id was already sent.|
|1006|Required property missing|One or more required property is missing.|
|1007|Email already unsubscribed|Email was unsubscribed in a previous API request.|
|1008|Error while checking email exists|Email validation failed due to internal server error.|
|1009|Invalid Value|Value is incorrect for a given field.|
|1010|Invalid survey id.|
|1012|Invalid survey type|$transaction_id, $transaction_date, $transaction_currency and $transaction_amount supported only for transactional surveys.|
|1013|Invalid key|Provided key is not supported.|
