---
title: GET /score
sidebar: mydoc_sidebar
permalink: v1_score.html
folder: 
---

## GET /score

Used to get customer satisfaction scores.

### URL parameters

|Parameter|Required|Requirements|Description|
|---------|--------|------------|-----------|
|start_date|Yes|YYYY:MM:DD (time assumed midnight) or YYYY:MM:DDTHH:MM:SS. Timezone inferred from project setting.|The start of the date range for which to get score.|
|end_date|Yes|YYYY:MM:DD (time assumed midnight) or YYYY:MM:DDTHH:MM:SS. Timezone inferred from project setting.|The end of the date range for which to get score.|
|interval|No|Day or Week or Month|Method to group scores. Default grouping is by day.|
|where|No|string|Filter on combination of any custom properties. You can apply combination of filters from various properties using an expression.|
|on|No|string|Aggregation on a single propertyâ€™s values. Format â€“ property["property name"]. Top 5 aggregations will be provided.|

#### "where" expression Format

##### Single

* property["property name"] (operator) (variable)

##### Multiple

* (property["property name"] (operator) (variable)) and (property["property name"] (operator) (variable)) and (property["property name"] (operator) (variable))
* (property["property name"] (operator) (variable)) or (property["property name"] (operator) (variable)) or (property["property name"] (operator) (variable))


#### Supported operators

|Property type|Operator|Operator notation|Example|Expression|Notes|
|-------------|-----|--------|-------|----------|-----|
|Number, Number set|less than|<|"$transaction_amount" less than 500|property["$transaction_amount"] < 500|
|Number, Number set|less than or equal to|<=|"$transaction_amount" less than 500|property["$transaction_amount"] <= 500|
|Number, Number set|greater than|>|"$transaction_amount" more than 500|property["$transaction_amount"] > 500|
|Number, Number set|greater than or equal to|>=|"$transaction_amount" more than 500|property["$transaction_amount"] >= 500|
|Number, Number set|exactly equal|==|"$transaction_amount" exactly equal to 500|property["$transaction_amount"] == 500|
|Number, Number set|is set|isset|"invoice_amount" is captured|property["invoice_amount"] isset|
|Number, Number set|is not set|isnotset|"invoice_amount" is not captured|property["invoice_amount"] isnotset|
|string, String set|contains|contain|"Hotel_Name" property contains the word "Taj"|property["Hotel_Name"] contain "Taj"|Supports partial and full word matches. Case insensitive|
|string, String set|exactly equal|==|"Hotel_Name" is exactly "Vivanta by Taj"|property["Hotel_Name"] == "Vivanta byTaj"|Only exact matches. Case sensitive.|
|string, String set|is set|isset|"App_Install_Source" is set|property["App_Install_Source"] isset|
|string, String set|is not set|isnotset|"App_Install_Source" is not set|property["App_Install_Source"] isnotset|
|Boolean|equal to|is|"CoD" equals to "true"|property["CoD"] is true|
|Boolean|is set|isset|"CoD" property is captured|property["CoD"] isset|
|Boolean|is not set|isnotset|"CoD" property is not captured|property["CoD"] isnotset|
|Date|less than|<|"$transaction_date" earlier than 2016-02-26|property["$transaction_dateâ€™â€™] < 2016-02-26|
|Date|less than or equal to|<=|"$transaction_date" earlier than or on 2016-02-26|property["$transaction_dateâ€™â€™] <= 2016-02-26|
|Date|more than|>|"$transaction_date" older than 2016-02-26|property["$transaction_date"] > 2016-02-26|
|Date|more than or equal to|>=|"$transaction_date" older than or on 2016-02-26|property["$transaction_date"] >= 2016-02-26|
|Date|on|==|"$transaction_date" on 2016-02-22|property[""$transaction_date"] == 2016-02-22|
|Date|is set|isset|"$transaction_date" is captured|property[""$transaction_date"] isset|
|Date|is not set|isnotset|"$transaction_date" is not captured|property[""$transaction_date"] isnotset|


#### Notes

* Operators for "Number Set" and "String Set" apply on individual items in the set.

* Combination of "and" and "or" cannot be used in an expression.

* Add a space before and after operator.

* Only 2 variables are available for â€œbooleanâ€ operator â€“ true and false.

* Use IS0 8601 format for date properties.

* Use double quotes on string and date values. Donâ€™t use quotes on number and boolean values.

* When aggregating by month/week the first day of the month/week will represent the month/week. If the start date is in the middle of month/week then data will be provided for partial month/week, but label in API response will be of first day of month/week.

* Maximum 5 conditions in "where" expression.

* Conflicting expressions will give 422 response. For e.g. property["$transaction_amount"] > 500 and property["$transaction_amount"] < 400.

* "contain" and "setcontain" operators cannot search characters separated by special characters. E.g. "Airbus A320-200" will not be a hit for keywords "Airbus A320" and "A320-200".

* Following formats are allowed for date properties: YYYY:MM:DD (time assumed midnight) or YYYY:MM:DDTHH:MM:SS. Timezone will be inferred from your project setting.

* Nested expressions are in beta.

#### Example

GET `/score?start_date=2016-08-15&end_date=2016-08-17&interval=day`

##### Response

```json
HTTP1/1.1 200
{
  "request_id": "446d229b-4904-43a4-be81-e8854421721d",
  "errors": [],
  "response": {
    "positive_score": 65.22,
    "boolean_score": 3.04,
    "positive_responses": 12,
    "negative_responses": 13,
    "has_score": true,
    "data": [
    {
      "interval_date": "2016-08-15T00:00:00Z",
      "epoch": 1471219200,
      "positive_score": null,
      "boolean_score": null,
      "positive_responses": null,
      "negative_responses": null,
      "has_score": false
    },
    {
      "interval_date": "2016-08-16T00:00:00Z",
      "epoch": 1471305600,
      "positive_score": 65.22,
      "boolean_score": 3.04,
      "positive_responses": 12,
      "negative_responses": 13,
      "has_score": true
    },
    {
      "interval_date": "2016-08-17T00:00:00Z",
      "epoch": 1471392000,
      "positive_score": null,
      "boolean_score": null,
      "positive_responses": null,
      "negative_responses": null,
      "has_score": false
    }
    ]
  }
}
```

#### Example

GET `/score?start_date=2016-08-01&end_date=2016-08-30&interval=month&where=(property["ticket_booking_mode"] contain "Airport" and property["discounted_ticket"] is false)`

##### Response

```json
HTTP1/1.1 200
{
  "request_id": "8aa91a6d-79c4-4fc7-831e-c93bfb198f2a",
  "errors": [],
  "response": {
      "positive_score": 78.57,
      "boolean_score": 5.71,
      "positive_responses": 12,
      "negative_responses": 42,
      "has_score": true,
      "data": [
      {
      "interval_date": "2016-08-01T00:00:00Z",
      "epoch": 1470009600,
      "positive_score": 78.57,
      "boolean_score": 5.71,
      "positive_responses": 12,
      "negative_responses": 42,
      "has_score": true
      }
    ]
  }
}
```

#### Example

GET `/score?start_date=2016-08-01&end_date=2016-08-30&interval=month&where=(property["flight_passenger_count"] > 81 or property["ticket_booking_mode"] contain "Airport")`

##### Response

```json
HTTP1/1.1 200
{
  "request_id": "77e9160c-e7c4-4ddd-af74-84655cbe9d7c",
  "errors": [],
  "response": {
      "positive_score": 67.05,
      "boolean_score": 3.57,
      "positive_responses": 15,
      "negative_responses": 19,
      "has_score": true,
      "data": [
      {
      "interval_date": "2016-08-01T00:00:00Z",
      "epoch": 1470009600,
      "positive_score": 67.05,
      "boolean_score": 3.57,
      "positive_responses": 15,
      "negative_responses": 19,
      "has_score": true
      }
    ]
  }
}
```

#### Example

GET `/score?start_date=2016-08-01&end_date=2016-08-30&interval=month&where=(property["ticket_booking_mode"] == "Airport counter" and property["boarding_officer_id"] isset and property["captain_id"] == "PFA")`

##### Response

```json
HTTP1/1.1 200
{
  "request_id": "72ce18be-d114-4882-9441-538a24f04826",
  "errors": [],
  "response": {
      "positive_score": 0.00,
      "boolean_score": -10.00,
      "positive_responses": 0,
      "negative_responses": 6,
      "has_score": true,
      "data": [
      {
      "interval_date": "2016-08-01T00:00:00Z",
      "epoch": 1470009600,
      "positive_score": 0.00,
      "boolean_score": -10.00,
      "positive_responses": 0,
      "negative_responses": 6,
      "has_score": true
      }
    ]
  }
}
```

#### Example

GET `/score?start_date=2016-08-01&end_date=2016-08-30&interval=month&where=(property["flight_passenger_count"] > 81 and property["ticket_booking_mode"] contain "Airport" and property["discounted_ticket"] is false and property["ticket_booking_date"] < "2016-01-13T07:57:53" and property["preordered_food_skus"] setcontain "GH123" and property["preordered_food_prices_inr"] setcontain 120)`

##### Response

```json
HTTP1/1.1 200
{
  "request_id": "2542cba7-58b6-4d5a-897a-084ed8d8da0e",
  "errors": [],
  "response": {
      "positive_score": 100.00,
      "boolean_score": 10.00,
      "positive_responses": 9,
      "negative_responses": 6,
      "has_score": true,
      "data": [
      {
      "interval_date": "2016-08-01T00:00:00Z",
      "epoch": 1470009600,
      "positive_score": 100.00,
      "boolean_score": 10.00,
      "positive_responses": 9,
      "negative_responses": 6,
      "has_score": true
      }
    ]
  }
}
```