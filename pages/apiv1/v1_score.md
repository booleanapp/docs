---
title: GET /scores
sidebar: mydoc_sidebar
permalink: v1_score.html
folder: 
---

## GET /scores

Used to get survey response aggregates.

### URL parameters

|Parameter|Required|Requirements|Description|
|---------|--------|------------|-----------|
|start_date|No|YYYY:MM:DD (time assumed midnight) or YYYY:MM:DDTHH:MM:SS. Timezone inferred from survey setting.|Start date.|
|end_date|No|YYYY:MM:DD (time assumed midnight) or YYYY:MM:DDTHH:MM:SS. Timezone inferred from survey setting.|End date.|
|interval|No|Day or Week or Month|Default is Day.|
|where|No|string|Segmentation conditions.|

#### "where" expression Format

##### Single

* property["property name"] (operator) (value)

##### Multiple

* (property["property name"] (operator) (value)) and (property["property name"] (operator) (value)) and (property["property name"] (operator) (value))
* (property["property name"] (operator) (value)) or (property["property name"] (operator) (value)) or (property["property name"] (operator) (value))


#### Supported operators

|Property type|Operator|Operator notation|Example|
|-------------|-----|--------|-------|----------|-----|
|Number, Number set|less than|<|property["refund_amount"] < 500|
|Number, Number set|less than or equal to|<=|property["refund_amount"] <= 500|
|Number, Number set|greater than|>|property["refund_amount"] > 500|
|Number, Number set|greater than or equal to|>=|property["refund_amount"] >= 500|
|Number, Number set|exactly equal|==|property["refund_amount"] == 500|
|Number, Number set|is set|isset|property["refund_amount"] isset|
|Number, Number set|is not set|isnotset|property["refund_amount"] isnotset|
|String, String set|contains|contain|property["name"] contain "john"|
|String, String set|exactly equal|==|property["name"] == "Joe John"|
|String, String set|is set|isset|property["name"] isset|
|String, String set|is not set|isnotset|property["name"] isnotset|
|Boolean|equal to|is|property["new_customer"] is true|
|Boolean|is set|isset|property["new_customer"] isset|
|Boolean|is not set|isnotset|property["new_customer"] isnotset|
|Date|less than|<|property["delivery_date"] < 2016-02-26|
|Date|less than or equal to|<=|property["delivery_date"] <= 2016-02-26|
|Date|more than|>|property["delivery_date"] > 2016-02-26|
|Date|more than or equal to|>=|property["delivery_date"] >= 2016-02-26|
|Date|on|==|property["delivery_date"] == 2016-02-22|
|Date|is set|isset|property["delivery_date"] isset|
|Date|is not set|isnotset|property["delivery_date"] isnotset|


#### Notes

* Operators for "Number Set" and "String Set" apply on individual items in the set.

* Operator "contains" for string and string set supports partial and full word matches. It is case insensitive.

* Operator "exactly equal" for string and string set supports only exact matches. It is case sensitive.

* Combination of "and" and "or" cannot be used in a single expression.

* Add a space before and after operator.

* When aggregating by month/week the first day of the month/week will represent the month/week. If the start date is in the middle of month/week then data will be provided for partial month/week, but label in API response will be of first day of month/week.

* Following formats are allowed for date properties: YYYY:MM:DD (time assumed midnight) or YYYY:MM:DDTHH:MM:SS. Timezone will be inferred from survey setting.


#### Example

```
GET /scores?pretty
```

##### Response

```json
HTTP1/1.1 200
{
  "request_id": "1e439af1-503b-4d97-a32e-4267faaa818f",
  "success": true,
  "errors": [],
  "response": {
    "positive_score": null,
    "boolean_score": null,
    "positive_responses": 0,
    "negative_responses": 0,
    "has_score": false,
    "data": [
      {
        "interval_date": "2017-05-24T00:00:00+05:30",
        "epoch": 1495564200,
        "positive_responses": 0,
        "negative_responses": 0,
        "positive_score": null,
        "boolean_score": null,
        "has_score": false
      },
      {
        "interval_date": "2017-05-25T00:00:00+05:30",
        "epoch": 1495650600,
        "positive_responses": 0,
        "negative_responses": 0,
        "positive_score": null,
        "boolean_score": null,
        "has_score": false
      }
    ]
  }
```

#### Example
 
```
GET /scores?start_date=2017-05-24&end_date=2017-05-25&where=(property["city"] == "San Francisco")&pretty
```

##### Response

```json
HTTP1/1.1 200
{
  "request_id": "012e4acd-7ff1-4c5a-b6b4-e18ddddb4294",
  "success": true,
  "errors": [],
  "response": {
    "positive_score": 100,
    "boolean_score": 10,
    "positive_responses": 1,
    "negative_responses": 0,
    "has_score": true,
    "data": [
      {
        "interval_date": "2017-05-24T00:00:00+05:30",
        "epoch": 1495564200,
        "positive_responses": 1,
        "negative_responses": 0,
        "positive_score": 100,
        "boolean_score": 10,
        "has_score": true
      },
      {
        "interval_date": "2017-05-25T00:00:00+05:30",
        "epoch": 1495650600,
        "positive_responses": 0,
        "negative_responses": 0,
        "positive_score": null,
        "boolean_score": null,
        "has_score": false
      }
    ]
  }
}
```

#### Example
 
```
GET /scores?start_date=2017-05-24&end_date=2017-05-25&where=(property["city"] == "San Francisco" and property["first_time_customer"] is false)&pretty
```

##### Response

```json
HTTP1/1.1 200
{
  "request_id": "e6f7e00f-a91f-4d71-b768-3fdc63f2b853",
  "success": true,
  "errors": [],
  "response": {
    "positive_score": 100,
    "boolean_score": 10,
    "positive_responses": 1,
    "negative_responses": 0,
    "has_score": true,
    "data": [
      {
        "interval_date": "2017-05-24T00:00:00+05:30",
        "epoch": 1495564200,
        "positive_responses": 1,
        "negative_responses": 0,
        "positive_score": 100,
        "boolean_score": 10,
        "has_score": true
      },
      {
        "interval_date": "2017-05-25T00:00:00+05:30",
        "epoch": 1495650600,
        "positive_responses": 0,
        "negative_responses": 0,
        "positive_score": null,
        "boolean_score": null,
        "has_score": false
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