---
title: API Documentation
description: 
---

## General requirements for API requests

- All requests should have "User-Agent" header.
- All requests should be authenticated using HTTP-BASIC
- All POST requests should use JSON content type for payload. A "Content-Type" header with value "application/json" is also required.
- All requests are subject to rate limits.
- Add parameter "pretty" to get pretty printed JSON response. E.g. `https://api.booleanapp.com/v1/stats?start_date=2016-07-16&end_date=2016-07-17&interval=day&pretty`

## Root endpoint

https://api.booleanapp.com/v1

- Only HTTPS is supported. Please do not use HTTP.

## Resources

### 1. [Unsubscribes](/api-unsubscribes/)

### 2. [Responses](/api-responses/)

### 3. [Stats](/api-stats/)

### 4. [Sendsurveys](/api-sendsurveys/)

### 5. [Score](/api-score/)




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

### Notes

- All requests must have the header 'content-type: application/json'. Request will be rejected otherwise with the following error:
  ```json
  {
    "code": "InvalidHeader",
    "message": "Content type application/json expected."
  }
  ```

- Note that the response for Stats endpoint is incorrect(aggregated over hour for testing). Update document when we have correct data.
