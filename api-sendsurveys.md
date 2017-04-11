---
title: /Sendsurveys
description: 
---

## POST /sendsurveys

Used to send surveys

### Query parameters

|Parameter|Required|Requirements|Description|
|---------|--------|------------|-----------|
|transaction|No|"yes" or "no"|Transactional surveys will have transaction information (identifier, date amd amount) prominenty displayed in survey email. Some JSON parameters in payload are mandatory for transactional surveys. If this query parameter is not provided then the survey will be assumed to be transactional.|


### JSON parameters

|Parameter|Required|Requirements|Description|
|---------|--------|------------|-----------|
|$email|Yes|email address. Max 75 characters.|Email address of recipient|
|properties|No|Dictionary/map|Property name and data type once set cannot be changed. If you try to send a wrong data type for an existing property your survey request will be rejected. You can use any UTF-8 string that doesn’t begin with "$" to name your properties. Spaces and hyphens are not allowed between characters of the name. Underscore is allowed. Spaces before and after the name will be automatically removed. Your property names cannot be longer than 255 characters. Data type needs to be defined along with property name in each API request.
|$transaction_id|No|String, max 50 characters|The unique identification number of the transaction. Mandatory for transactional surveys.|
|$transaction_date|No|YYYY-MM-DDTHH:MM:SSZ (UTC time) or YYYY-MM-DDTHH:MM:SSZ±00:00 (local time with UTC offset) or 1474698657 (epoch) |Time of transaction. Mandatory for transactional surveys.|
|$transaction_amount|No|Number (double). Max 9999999999|Transaction amount paid by customer. Mandatory for transactional surveys.|
|$transaction_currency|No|INR, USD, EUR, JPY, GBP or CNY|Currency. Mandatory for transactional surveys.|
|$send_at|No|YYYY-MM-DDTHH:MM:SSZ (UTC time) or YYYY-MM-DDTHH:MM:SSZ±00:00 (local time with UTC offset) or 1474698657 (epoch) |Use this for scheduling survey for a later time|
|$delay|No|Seconds|Use this to delay sending of survey. By default surveys are sent with few minutes|

### Property data types

|Property type|Notation|Data limits|
|-------------|--------|-----------|
|String|S|Max 255 characters|
|Number|N|Max 9999999999|
|Date|D|YYYY-MM-DDTHH:MM:SSZ (UTC time) or YYYY-MM-DDTHH:MM:SSZ±00:00 (local time with UTC offset) or 1474698657 (epoch). Pleast note that time zone specification is mandatory for date properties.|
|Boolean|B|true or false|
|String set|SS|Max 20 items in array, each string max 255 characters|
|Number set|NS|Max 20 items in array, each number max 9999999999|



#### Example

POST `/sendsurveys`

##### JSON Parameters

```json
[
    {
        "$email": "test1@test.com",
        "$transaction_id": "1231",
        "$transaction_date": "2016-01-13T04:30:30Z",
        "$transaction_amount": 1222,
        "$transaction_currency": "INR",
        "properties": {
            "city": {"S": "chennai"},
            "order_delivery_date": {"D": "2016-01-13T04:30:30Z"},
            "order_item_skus": {"SS": ["BP00121312", "BP01283232"]},
            "order_item_prices": {"NS": ["1203", "1231"]},
            "first_time_customer": {"B": true}
        }
    }
]
```

##### Response

```json
HTTP 1/1.1 200
{
    "request_id": "rezhpxd-caisogk-yefbbdx-mqoeigi",
    "response": [
        {
            "$email": "test1@test.com",
            "message": "accepted",
            "errors": []
        }
    ]
}
```

#### Example

POST `/sendsurveys`

##### JSON Parameters

```json
[
    {
        "$email": "test1@test.com",
        "$transaction_id": "1231",
        "$transaction_date": "2016-01-13T04:30:30Z",
        "$transaction_amount": 1222,
        "$transaction_currency": "INR",
        "properties": {
            "city": {"S": "chennai"},
            "order_delivery_date": {"D": "2016-01-13"},
            "order_item_skus": {"SS": ["BP00121312", "BP01283232"]},
            "order_item_prices": {"NS": ["1203", "1231"]},
            "first_time_customer": {"B": "not"}
        }
    }
]
```

##### Response

```json
HTTP 1/1.1 200
{
    "request_id": "jnepqph-lllicpc-seunxpg-qutsywe",
    "response": [
        {
            "$email": "test3@test.com",
            "message": "failure",
            "errors": [
                {
                    "code": 1001,
                    "field": "order_delivery_date",
                    "message": "Date should be in ISO 8601 format or epoch"
                },
                {
                    "code": 1001,
                    "field": "first_time_customer",
                    "message": "Boolean value should be either true or false"
                }
            ]
        }
    ]
}
```

#### Example

POST `/sendsurveys`

##### JSON parameters

```json
[
    {
        "$email": "test1@test.com",
        "$transaction_id": "1235",
        "$transaction_date": "2016-01-13T04:30:30Z",
        "$transaction_amount": 1222,
        "$transaction_currency": "INR",
        "properties": {
            "city": {"S": "chennai"},
            "order_delivery_date": {"D": "2016-01-13T04:30:30Z"},
            "order_item_skus": {"SS": ["BP00121312", "BP01283232"]},
            "order_item_prices": {"NS": ["1203", "1231"]},
            "first_time_customer": {"B": true}
        }
    },
    {
        "$email": "test2@test.com",
        "$transaction_id": "1236",
        "$transaction_date": "2016-01-13T04:30:30Z",
        "$transaction_amount": 1499,
        "$transaction_currency": "INR",
        "properties": {
            "city": {"S": "chennai"},
            "order_delivery_date": {"D": "2016-01-13T04:30:30Z"},
            "order_item_skus": {"SS": ["BP00121312", "BP01283232"]},
            "order_item_prices": {"NS": ["1203", "1231"]},
            "first_time_customer": {"B": true}
        }
    },
    {
        "$email": "test3@test.com",
        "$transaction_id": "1237",
        "$transaction_date": "2016-01-13T04:30:30Z",
        "$transaction_amount": 1599,
        "$transaction_currency": "INR",
        "properties": {
            "city": {"S": "chennai"},
            "order_delivery_date": {"D": "2016/02/01"},
            "order_item_skus": {"SS": ["BP00121312", "BP01283232"]},
            "order_item_prices": {"NS": ["1203", "1231"]},
            "first_time_customer": {"B": "random"}
        }
    }
]
```

##### Response

```json
HTTP1/1.1 200
{
    "request_id": "kpbnvsw-lcipenh-dazprqd-jzlwstr",
    "response": [
        {
            "$email": "test1@test.com",
            "message": "accepted",
            "errors": []
        },
        {
            "$email": "test2@test.com",
            "message": "accepted",
            "errors": []
        },
        {
            "$email": "test3@test.com",
            "message": "failure",
            "errors": [
                {
                    "code": 1001,
                    "field": "order_delivery_date",
                    "message": "Date should be in ISO 8601 format with UTC time zone"
                },
                {
                    "code": 1001,
                    "field": "first_time_customer",
                    "message": "Boolean value should be either true or false"
                }
            ]
        }
    ]
}
```

#### Example

POST `/sendsurveys?transaction=no`

##### JSON Parameters

```json
[
    {
        "$email": "test1@test.com",
        "properties": {
            "city": {"S": "Bangalore"},
            "order_delivery_date": {"D": "2015-01-13T04:30:30Z"},
            "order_item_skus": {"SS": ["AP00121412", "BP01283901"]},
            "order_item_prices": {"NS": ["9203", "8231"]},
            "first_time_customer": {"B": false}
        }
    }
]
```

##### Response

```json
HTTP 1/1.1 200
{
    "request_id": "rezhpxd-caisogk-yefbbdx-mqoeigi",
    "response": [
        {
            "$email": "test1@test.com",
            "message": "accepted",
            "errors": []
        }
    ]
}
```


#### Notes

* Max 50 properties per project.

* Max 10000 surveys per API call.

* Max 10 API calls per sec.

* Surveys are usually sent within few minutes of accepting.

* If same survey is requested again, a "duplicate request" error will be returned. A unique survey is identified by combination of project_id and transaction_id.

* Please check "message" and "errors" parameters for surveys which were not processed. These need to be tried again.

* If an API request has more than 50 properties, then 1003 error will be returned.

* The API payload should always be a JSON array (even for a single survey request).

#### Error codes

|Code|Message|Description|
|----|-------|-----------|
|1000|Error|Default error|
|1001|Invalid format|Invalid formt of data|
|1002|Already exists|Property already exists with different data type|
|1003|Quota exceeded|Property quota exceeded. Max 50 properties per project|
|1004|Duplicate request|A survey for same transaction_id was already sent|
|1006|Required property missing|One or more required property is missing|
|1009|Invalid Value|Value is incorrect for given field.|
