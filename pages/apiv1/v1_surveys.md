---
title: POST,GET /surveys
sidebar: mydoc_sidebar
permalink: v1_surveys.html
---

## POST /surveys

Used to send surveys

### Query parameters

|Parameter|Required|Requirements|Description|
|---------|--------|------------|-----------|
|transactional|No|"true" or "false"|Use "false" for non-transactional surveys. If this query parameter is not provided then the survey will be assumed to be transactional. Transactional surveys will have transaction information (identifier, date amd amount) prominenty displayed in survey email.|


### JSON parameters

|Parameter|Required|Requirements|Description|
|---------|--------|------------|-----------|
|$email|Yes|email address. Max 75 characters.|Email address of recipient|
|properties|No|Dictionary/map|Property name and data type once set cannot be changed. If you try to send a wrong data type for an existing property your survey request will be rejected. You can use any UTF-8 string which satisfies [the criteria](#custom-property-criteria). Data type needs to be defined along with property name in each API request.
|$transaction_id|No|String, max 50 characters|The unique identification number of the transaction. Mandatory for transactional surveys.|
|$transaction_date|No|YYYY-MM-DDTHH:MM:SSZ (UTC time) or YYYY-MM-DDTHH:MM:SSZÂ±00:00 (local time with UTC offset) or 1474698657 (epoch) |Time of transaction. Mandatory for transactional surveys.|
|$transaction_amount|No|Number (double). Max 9999999999|Transaction amount paid by customer. Mandatory for transactional surveys.|
|$transaction_currency|No|INR, USD, EUR, JPY, GBP or CNY|Currency. Mandatory for transactional surveys.|
|$send_at|No|YYYY-MM-DDTHH:MM:SSZ (UTC time) or YYYY-MM-DDTHH:MM:SSZÂ±00:00 (local time with UTC offset) or 1474698657 (epoch) |Use this for scheduling survey for a later time|
|$delay|No|Seconds|Use this to delay sending of survey. By default surveys are sent with few minutes|

### Custom Property Criteria
A custom property name should satisfy the following:

  - The custom property should start with an alphanumeric character.
  - The length of the name should be between `2` and `75`.
  - Limited special characters are allowed in the name. These are `_`, `$`. Spaces are not allowed anywhere in the property name.

Some valid property names - `addressLine1`, `customer_name`, `a1`.

Illegal property names - `$cust_prop`, `_cust_prop`, `#address`, `a`, `some_bizzare_and_extremely_long_custom_property_name_which_exceeds_75_characters`,
`cust&prop`, `cust(prop)`, `cust prop`.

### Property data types

|Property type|Notation|Data limits|
|-------------|--------|-----------|
|String|S|Max 255 characters|
|Number|N|Max 9999999999|
|Date|D|YYYY-MM-DDTHH:MM:SSZ (UTC time) or YYYY-MM-DDTHH:MM:SSZÂ±00:00 (local time with UTC offset) or 1474698657 (epoch). Pleast note that time zone specification is mandatory for date properties.|
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
    "errors": [],
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
    "errors": [],
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
    "errors": [],
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
    "errors": [],
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
|1012|Invalid survey type|$transaction_id, $transaction_date, $transaction_currency and $transaction_amount supported only for transactional surveys.|
|1013|Invalid key|Provided key is not supported|


## GET /surveys

Used to list all surveys

### Query parameters

|Parameter|Required|Requirements|Description|
|---------|--------|------------|-----------|
|start_date|No|YYYY:MM:DD (time assumed midnight) or YYYY:MM:DDTHH:MM:SS. Timezone inferred from project setting.|The start date to retrieve responses.|
|end_date|No|YYYY:MM:DD (time assumed midnight) or YYYY:MM:DDTHH:MM:SS. Timezone inferred from project setting.|The end date to retrieve responses.|
|date_filter_type|No|created_at or response_received_at or opened_at|To specify basis of date filter. by default created_at will be used.|
|page|No|Integer. Min 1. Max 20.|Optional parameter to specify page number. To be used with size parameter.|
|size|No|Integer. Min 10. Max 100.|Optional parameter to specify number of results per page.|
|email|No|email address. Max 75 characters.|Optional parameter to search for a particular email.|
|feedback|No|1 or 0 or -1|An optional filter to retrieve only positive or negative or no feedback. To get only positive feedback specify 1. To get only negative feedback specify -1. To get surveys with no feedback specify 0.|
|comments|No|True or false|An optional filter to retrieve only responses with comments. By default, all responses are returned. To get only responses with comments set this parameter to true.|
|comments_search|No|String. Max 50 characters.|An optional filter to search for a particular keyword in comments.|
|sort|No|created_at or response_received_at or opened_at|An optional parameter to sort surveys based on creation time or response time. Use negative sign for inverse sort (chronological). By default surveys are sorted on created_at.|
|fields|No|$email, $transaction_id, $transaction_date, $transaction_currency, $transaction_amount, $transactional, properties, properties.[property name], $created_at, $project_id, $survey_sent, $feedback, $survey_sent_at, $response_received_at, $opened_at|An optional parameter to get only specific fields in response.|

#### Example

GET `https://api.booleanapp.com/v1/surveys?start_date=2016-08-16&end_date=2016-08-17&page=1&size=10&feedback=0&comments=true&comments_search=bad&sort_order=response_received_at`

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
          "$id": "b7b1852d3c4184e43c2452399a783b0f",
          "$email": "booleanmail@gmail.com",
          "$transaction_id": "57b2e9e2696614f122030a1d",
          "$transaction_date": "2014-07-20T07:15:47.000Z",
          "$transaction_currency": "INR",
          "$transaction_amount": 5407.05,
          "properties": {
            "flight_no": "QS 116",
            "origin": "MAA",
            "destination": "MAA",
            "sector": "East",
            "aircraft": "Airbus A320neo",
            "aircraft_serial_no": "VN-A123",
            "ticket_booking_date": "2015-11-25T02:54:40.000Z",
            "ticket_booking_mode": "Airport counter",
            "discounted_ticket": true,
            "website_customer_id": 99851266,
            "customer_gender": "male",
            "checkin_baggage_weight_KG": 19,
            "preordered_food_skus": [
              "SD235",
              "GH624",
              "GH123"
            ],
            "preordered_food_prices_inr": [
              250,
              450,
              250
            ],
            "seat_no": "21b",
            "flight_passenger_count": 59,
            "crew_count": 7,
            "captain_id": "AKF",
            "head_cabin_crew_id": "C-WDS",
            "cabin_crew_ids": [
              "C-IDJ",
              "C-WOA",
              "C-TUI",
              "C-QLI"
            ],
            "checkin_officer_id": "CH-ASW",
            "boarding_officer_id": "CH-ASD",
            "boarding_gate": "7a",
            "stops": 2,
            "check_in_time": "2016-07-30T03:43:40.000Z",
            "boarding_time": "2016-02-28T12:10:55.000Z",
            "scheduled_departure_time": "2014-06-21T01:27:35.000Z",
            "actual_departure_time": "2016-05-03T01:22:32.000Z",
            "scheduled_arrival_time": "2014-01-13T09:38:20.000Z",
            "actual_arrival_time": "2016-04-06T10:44:37.000Z",
            "arrival_delay_mins": 28
          },
          "$created_at": "2016-08-16T10:24:36.741Z",
          "$project_id": "1234",
          "$survey_sent": true,
          "$feedback": -1,
          "$survey_sent_at": "2016-08-16T10:25:06.959Z",
          "$response_received_at": "2016-08-16T10:28:01.268Z",
          "$opened_at": "2016-08-16T10:28:01.268Z"
      },
      {
          "$id": "1241852d3cas4e43c2452399a783b0f",
          "$email": "booleanmmail@yahoo.com",
          "$transaction_id": "57b2e9e2a925748ceb6b2ca5",
          "$transaction_date": "2016-04-18T06:45:02.000Z",
          "$transaction_currency": "INR",
          "$transaction_amount": 4241.99,
          "properties": {
            "flight_no": "QS 122",
            "origin": "MAA",
            "destination": "IXL",
            "sector": "West",
            "aircraft": "Airbus A320neo",
            "aircraft_serial_no": "F-GHQA",
            "ticket_booking_date": "2016-06-05T05:28:39.000Z",
            "ticket_booking_mode": "Website",
            "discounted_ticket": false,
            "website_customer_id": 83189225,
            "customer_gender": "male",
            "checkin_baggage_weight_KG": 8,
            "preordered_food_skus": [
              "SD123",
              "TH235",
              "TH342"
            ],
            "preordered_food_prices_inr": [
              120,
              450,
              120
            ],
            "seat_no": "5b",
            "flight_passenger_count": 122,
            "crew_count": 5,
            "captain_id": "OPS",
            "head_cabin_crew_id": "C-TUI",
            "cabin_crew_ids": [
              "C-QPM",
              "C-TND",
              "C-QOJ",
              "C-PLA"
            ],
            "checkin_officer_id": "CH-ASD",
            "boarding_officer_id": "CH-TWD",
            "boarding_gate": "8b",
            "stops": 0,
            "check_in_time": "2015-06-27T01:43:45.000Z",
            "boarding_time": "2015-09-04T06:30:34.000Z",
            "scheduled_departure_time": "2014-09-04T04:09:57.000Z",
            "actual_departure_time": "2016-02-27T01:09:12.000Z",
            "scheduled_arrival_time": "2015-03-10T06:50:17.000Z",
            "actual_arrival_time": "2014-08-09T02:03:13.000Z",
            "arrival_delay_mins": 16
          },
          "$created_at": "2016-08-16T10:24:36.791Z",
          "$project_id": "1234",
          "$survey_type": "EMAIL",
          "$survey_sent": false,
          "$feedback": 0,
          "$survey_sent_at": null,
          "$response_received_at": null,
          "$opened_at": null
      }
    ]
  }
}
```


#### Notes

* Surveys will be listed in reverse chronological order of created_date

* Results are paginated by default with 30 results per page. Use "link" header to find URL of next page.

#### Error codes

|Code|Message|Description|
|----|-------|-----------|
|1001|Invalid format|Invalid format of data|
|1009|Invalid Value|Value is incorrect for given field.|

## GET /surveys/[id]

Used to get a specific survey

#### Example

GET `https://api.booleanapp.com/v1/surveys/b7b1852d3c4184e43c2452399a783b0f`

##### Response

```json
HTTP 1/1.1 200
{
  "request_id": "c3f1e787-29bf-4f68-9c82-4c8c5ff19c9e",
  "errors": [],
  "response": {
          "$id": "b7b1852d3c4184e43c2452399a783b0f",
          "$email": "booleanmail@gmail.com",
          "$transaction_id": "57b2e9e2696614f122030a1d",
          "$transaction_date": "2014-07-20T07:15:47.000Z",
          "$transaction_currency": "INR",
          "$transaction_amount": 5407.05,
          "properties": {
            "flight_no": "QS 116",
            "origin": "MAA",
            "destination": "MAA",
            "sector": "East",
            "aircraft": "Airbus A320neo",
            "aircraft_serial_no": "VN-A123",
            "ticket_booking_date": "2015-11-25T02:54:40.000Z",
            "ticket_booking_mode": "Airport counter",
            "discounted_ticket": true,
            "website_customer_id": 99851266,
            "customer_gender": "male",
            "checkin_baggage_weight_KG": 19,
            "preordered_food_skus": [
              "SD235",
              "GH624",
              "GH123"
            ],
            "preordered_food_prices_inr": [
              250,
              450,
              250
            ],
            "seat_no": "21b",
            "flight_passenger_count": 59,
            "crew_count": 7,
            "captain_id": "AKF",
            "head_cabin_crew_id": "C-WDS",
            "cabin_crew_ids": [
              "C-IDJ",
              "C-WOA",
              "C-TUI",
              "C-QLI"
            ],
            "checkin_officer_id": "CH-ASW",
            "boarding_officer_id": "CH-ASD",
            "boarding_gate": "7a",
            "stops": 2,
            "check_in_time": "2016-07-30T03:43:40.000Z",
            "boarding_time": "2016-02-28T12:10:55.000Z",
            "scheduled_departure_time": "2014-06-21T01:27:35.000Z",
            "actual_departure_time": "2016-05-03T01:22:32.000Z",
            "scheduled_arrival_time": "2014-01-13T09:38:20.000Z",
            "actual_arrival_time": "2016-04-06T10:44:37.000Z",
            "arrival_delay_mins": 28
          },
          "$created_at": "2016-08-16T10:24:36.741Z",
          "$project_id": "1234",
          "$survey_sent": true,
          "$feedback": -1,
          "$survey_sent_at": "2016-08-16T10:25:06.959Z",
          "$response_received_at": "2016-08-16T10:28:01.268Z",
          "$opened_at": "2016-08-16T10:28:01.268Z"
  }
}
```

#### Error codes

|Code|Message|Description|
|----|-------|-----------|
|1010|Invalid survey id|