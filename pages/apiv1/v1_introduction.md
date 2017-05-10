---
title: API v1 Introduction
sidebar: mydoc_sidebar
permalink: v1_introduction.html
---

## General requirements for API requests

- All requests should have "User-Agent" header.
- All requests should be authenticated using HTTP-BASIC (_give example here_)
- All POST requests should use JSON content type for payload (_and not plain text?_). A "Content-Type" header with value "application/json" is also required.
- All requests are subject to rate limits (_explain rules here_)
- Add parameter "pretty" to get pretty printed JSON response. E.g. `https://api.booleanapp.com/v1/stats?start_date=2016-07-16&end_date=2016-07-17&interval=day&pretty`


## Resources

### [Surveys](v1_surveys.html)

### [Score](v1_score.html)

### [Stats](v1_stats.html)

### [Properties](v1_properties.html)

### [Unsubscribes](v1_unsubscribes.html)


## Error codes

|HTTP code|Message|
|---------|-------|
|401|Invalid API Key|
|401|API key not provided|
|400|Badly formed JSON|
|404|Non-existent resource is requested|
|405|Method not allowed|
|422|Unprocessable request. Due to wrong data type or erroneous expression|
|429|Too many requests.|

### Generic JSON response in case of HTTP errors

```json
<HTTP code>
{
  "request": "<request URI>",
  "error": "<error message>"
}
```

#### Example
```json
HTTP1/1.1 401
{
    "request": "/sendsurveys/",
    "error": "Invalid API Key",
    "documentation": "http://api.auscult.com/docs"
}
```

## API Error codes

|Code|Message|Description|
|----|-------|-----------|
|1000|Error|Default error|
|1001|Invalid format|Invalid format of data|
|1002|Already exists|Property already exists with different data type|
|1003|Quota exceeded|Property quota exceeded. Max 50 properties per project|
|1004|Duplicate request|A survey for same transaction_id was already sent|
|1006|Required property missing|One or more required property is missing|
|1007|Email already unsubscribed|Email was unsubscribed in a previous API request.|
|1008|Error while checking email exists|Email validation failed due to internal server error.|
|1009|Invalid Value|Value is incorrect for given field.|
|1010|Invalid survey id|
|1011|__not used__|__not used__|
|1012|Invalid survey type|$transaction_id, $transaction_date, $transaction_currency and $transaction_amount supported only for transactional surveys.|
|1013|Invalid key|Provided key is not supported|

### Notes

- All requests must have the header 'content-type: application/json'. Request will be rejected otherwise with the following error:
  ```json
  {
    "code": "InvalidHeader",
    "message": "Content type application/json expected."
  }
  ```

## CORS test cases

* Support OPTIONS request on /unsubscribes, /stats, /surveys, /score and /properties endpoints with following static response

```html
Access-Control-Allow-Origin: _echo of request origin_
Access-Control-Allow-Headers: Authorization
Access-Control-Allow-Methods: GET, POST
Access-Control-Allow-Credentials: true
```

* Add following header to all GET and POST responses on /unsubscribes, /stats, /surveys, /score and /properties endpoints

```html
Access-Control-Allow-Origin: _echo of request origin_
Access-Control-Allow-Credentials: true
```