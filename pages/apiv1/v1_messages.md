---
title: POST,GET /messages
sidebar: mydoc_sidebar
permalink: v1_messages.html
---

## POST /messages

Used to send survey emails.

### Query parameters

|Parameter|Required|Requirements|Description|
|---------|--------|------------|-----------|
|transactional|No|"true" or "false"|"Transactional" emails will prominently feature 4 variables in body - $transaction_id, $transaction_date, $transaction_amount, and $transaction_currency. Use "transactional=false" for sending regular emails.|


### JSON parameters

|Parameter|Required|Requirements|Description|
|---------|--------|------------|-----------|
|$email|Yes|email address. Max 75 characters.|Email address of recipient.|
|properties|No|Dictionary/map|Used to send properties for segmentation. Property name and data type should be specified in every request. Property name and data type once set cannot be changed. Property name should follow these [rules](#property-naming-requirements).|
|$transaction_id|No|String, max 50 characters|Mandatory for transactional emails.|
|$transaction_date|No|YYYY-MM-DDTHH:MM:SSZ (UTC time) or YYYY-MM-DDTHH:MM:SS±00:00 (local time with offset) or 1474698657 (epoch) |Mandatory for transactional emails.|
|$transaction_amount|No|Number (double). Max 9999999999|Mandatory for transactional emails.|
|$transaction_currency|No|INR, USD, EUR, JPY, GBP or CNY|Mandatory for transactional emails.|
|$send_at|No|YYYY-MM-DDTHH:MM:SSZ (UTC time) or YYYY-MM-DDTHH:MM:SS±00:00 (local time with offset) or 1474698657 (epoch) |Use for scheduling emails.|

### Property naming requirements

  - Should start with an alphanumeric character.
  - Length `2` to `75` characters.
  - Only 2 special characters allowed `_` or `$` (after first character).

Valid property name examples - `addressLine1`, `customer_name`, `a1`.

Invalid property name examples - `$cust_prop`, `_cust_prop`, `#address`, `a`, `cust&prop`, `cust(prop)`, `cust prop`.

### Property data types

|Property type|Notation|Data limits|
|-------------|--------|-----------|
|String|S|Max 255 characters.|
|Number|N|Max 9999999999.|
|Date|D|YYYY-MM-DDTHH:MM:SSZ (UTC time) or YYYY-MM-DDTHH:MM:SS±00:00 (local time with offset) or 1474698657 (epoch).|
|Boolean|B|true or false.|
|String set|SS|Max 20 items in array, each string max 255 characters.|
|Number set|NS|Max 20 items in array, each number max 9999999999.|


#### Example - regular email

```
POST /messages?transactional=false
```

##### JSON Parameters

```json
[
    {
        "$email": "someone@somedomain.com",
    }
]
```

##### Response

```json
HTTP 1/1.1 200
{
  "request_id": "fcdabbc2-eb34-48f4-a9c3-b364df5f6a2d",
  "success": true,
  "errors": [],
  "response": [
    {
      "$email": "someone@somedomain.com",
      "message": "accepted",
      "errors": []
    }
  ]
}
```


#### Example - transactional email

```
POST /messages
```

##### JSON Parameters

```json
[
    {
        "$email": "someone@somedomain.com",
        "$transaction_id": "4125",
        "$transaction_date": "2016-01-13T04:30:30Z",
        "$transaction_amount": 999,
        "$transaction_currency": "USD",
        "properties": {
            "city": {"S": "San Francisco"},
            "order_delivery_date": {"D": "2016-01-15T02:30:30Z"},
            "order_item_skus": {"SS": ["BP00121312", "BP01283232"]},
            "order_item_prices": {"NS": ["500", "499"]},
            "first_time_customer": {"B": true}
        }
    }
]
```

##### Response

```json
HTTP 1/1.1 200
{
    "request_id": "adsabbc2-12x4-kas1-sd1c-sa12ff5f6acs",
    "success": true,    
    "errors": [],
    "response": [
        {
            "$email": "someone@somedomain.com",
            "message": "accepted",
            "errors": []
        }
    ]
}
```




#### Notes

* Max 50 properties per email.

* Max 10000 emails per API call.

* Max one email per unique $transaction_id.

* The API payload should always be a JSON array (even for a single email request).

#### Error codes

|Code|Message|Description|
|----|-------|-----------|
|1000|Error|Default error.|
|1001|Invalid format|Invalid format of data.|
|1002|Already exists|Property already exists with different data type.|
|1003|Quota exceeded|Property quota exceeded. Max 50 properties per survey.|
|1004|Duplicate request|An email for same transaction_id already sent.|
|1006|Required property missing|One or more required property is missing.|
|1009|Invalid Value|Value is incorrect for a given field.|
|1012|Invalid email type|$transaction_id, $transaction_date, $transaction_currency and $transaction_amount supported only for transactional emails.|
|1013|Invalid key|Provided key is not supported.|


## GET /messages

Used to list emails.

### Query parameters

|Parameter|Required|Requirements|Description|
|---------|--------|------------|-----------|
|start_date|No|YYYY:MM:DD (time assumed midnight) or YYYY:MM:DDTHH:MM:SS. Timezone inferred from survey setting.|Start date.|
|end_date|No|YYYY:MM:DD (time assumed midnight) or YYYY:MM:DDTHH:MM:SS. Timezone inferred from survey setting.|End date.|
|date_filter_type|No|created_at or response_received_at or opened_at|To specify basis of date filter. Default is created_at.|
|page|No|Integer. Min 1. Max 20.|Optional parameter to specify page number. To be used with size parameter.|
|size|No|Integer. Min 10. Max 100.|Optional parameter to specify number of results per page.|
|email|No|email address. Max 75 characters.|Optional parameter to search for a particular email.|
|feedback|No|1 or 0 or -1|An optional filter to retrieve only positive or negative or no feedback. To get only positive feedback specify 1. To get only negative feedback specify -1. To get emails with no feedback specify 0.|
|comments|No|True or false|An optional filter to retrieve only responses with comments. By default, all responses are returned. To get only responses with comments set this parameter to true.|
|comments_search|No|String. Max 50 characters.|An optional filter to search for a particular keyword in comments.|
|sort|No|created_at or response_received_at or opened_at|An optional parameter to sort emails based on creation time or response time. Use negative sign for inverse sort (chronological). By default emails are sorted on creation time.|
|fields|No|$email, $transaction_id, $transaction_date, $transaction_currency, $transaction_amount, $transactional, properties, properties.[property name], $created_at, $project_id, $survey_sent, $feedback, $survey_sent_at, $response_received_at, $opened_at|An optional parameter to get only specific fields in response.|

#### Example

```
GET /messages?pretty
```

##### Response

```json
HTTP 1/1.1 200
{
  "request_id": "c3f1e787-29bf-4f68-9c82-4c8c5ff19c9e",
  "errors": [],
  "response": {
    "total": 2,
    "size": 10,
    "page": 1,
    "data": [
      {
        "$email": "someone@somedomain.com",
        "$transaction_id": "4125",
        "$transaction_date": "2016-01-13T04:30:30Z",
        "$transaction_amount": 999,
        "$transaction_currency": "USD",
        "$transactional": true,
        "$req_id": "adsabbc2-12x4-kas1-sd1c-sa12ff5f6acs",
        "$properties": {
          "city": "San Francisco",
          "order_delivery_date": "2016-01-15T02:30:30Z",
          "order_item_skus": [
            "BP00121312",
            "BP01283232"
          ],
          "order_item_prices": [
            500,
            499
          ],
          "first_time_customer": true
        },
        "$created_at": "2016-01-23T08:00:08.668Z",
        "$project_id": "6",
        "$survey_type": "EMAIL",
        "$survey_sent": false,
        "$survey_picked": true,
        "$survey_picked_at": "2016-01-23T08:00:47.966Z",
        "$feedback": 0,
        "$survey_sent_at": "2017-05-23T07:58:48.418Z",
        "$id": "ja91jd7a9b73c4ef3f07e9f8fd7has71"      },
      {
        "$email": "someone@somedomain.com",
        "$transaction_id": "auto_8763c210-3f8d-11e7-8d5f-c76a54e74366",
        "$transaction_date": "2017-05-23T07:57:55.249Z",
        "$transaction_amount": null,
        "$transaction_currency": null,
        "$transactional": false,
        "$req_id": "8084f80f-197e-4dc5-a3f0-11e10c5e9219",
        "$properties": {},
        "$created_at": "2017-05-23T07:57:55.263Z",
        "$project_id": "6",
        "$survey_type": "EMAIL",
        "$survey_sent": true,
        "$survey_picked": true,
        "$survey_picked_at": "2017-05-23T07:58:47.939Z",
        "$feedback": 0,
        "$survey_sent_at": "2017-05-23T07:58:48.418Z",
        "$id": "29eda2f49b73c4ef3f07e9f8fd7f4ff9"
      }
    ]
  }
}
```
### Message object

|Parameter|Description|
|---------|--------|
|$email|Email address of recipient.|
|$id|id of email.|
|$transaction_id|Mandatory variable for transactional emails.|
|$transaction_date|Mandatory variable for transactional emails.|
|$transaction_amount|Mandatory variable for transactional emails.|
|$transaction_currency|Mandatory variable for transactional emails.|
|$transactional|Whether transactional email or not.|
|$req_id|Request id of POST API request.|
|$created_at|Time of acceptance of POST API request.|
|$project_id|id of survey.|
|$survey_type|Type of email. Currently only email.|
|$survey_sent|Status of email sending.|
|$survey_picked|Status of picking email to send.|
|$survey_picked_at|Time when email was picked to send.|
|$survey_sent_at|Time when email was sent.|
|$feedback|Response received for email. 0 means no response received. 1 means positive response received. -1 means negative response received.|
|$bounce_type|Email bounce type.|
|$bounce_desc|Email bounce description.|
|$bounce_id|Email bounce id.|
|$bounced_at|Time when email bounced.|
|$properties|Properties of email as set during creation.|



#### Notes

* Emails will be listed in reverse chronological order of created_date

* Results are paginated by default with 30 results per page. Use "link" header to find URL of next page.

#### Error codes

|Code|Message|Description|
|----|-------|-----------|
|1001|Invalid format|Invalid format of data.|
|1009|Invalid Value|Value is incorrect for given field.|

## GET /messages/[id]

Used to get a specific email.

### URL format

GET `/messages/[id]`


#### Example

```
GET /messages/29eda2f49b73c4ef3f07e9f8fd7f4ff9
```

##### Response

```json
HTTP 1/1.1 200
{
  "request_id": "348e684e-b65c-400c-9e0c-739d26b0f1bd",
  "success": true,
  "errors": [],
  "response": {
        "$email": "someone@somedomain.com",
        "$transaction_id": "auto_8763c210-3f8d-11e7-8d5f-c76a54e74366",
        "$transaction_date": "2017-05-23T07:57:55.249Z",
        "$transaction_amount": null,
        "$transaction_currency": null,
        "$transactional": false,
        "$req_id": "8084f80f-197e-4dc5-a3f0-11e10c5e9219",
        "$properties": {},
        "$created_at": "2017-05-23T07:57:55.263Z",
        "$project_id": "6",
        "$survey_type": "EMAIL",
        "$survey_sent": true,
        "$survey_picked": true,
        "$survey_picked_at": "2017-05-23T07:58:47.939Z",
        "$feedback": 0,
        "$survey_sent_at": "2017-05-23T07:58:48.418Z",
        "$id": "29eda2f49b73c4ef3f07e9f8fd7f4ff9"
  }
}
```

#### Error codes

|Code|Message|
|----|-------|
|1010|Invalid email id.|