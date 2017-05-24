---
title: GET /properties
sidebar: mydoc_sidebar
permalink: v1_properties.html
---

## GET /properties

Used to list properties set for a project

### URL parameters

|Parameter|Required|Requirement|Description|
|---------|--------|-----------|-----------|
|type|No|S or N or D or B or SS or NS|An optional filter to list specific kind of properties - S(string), N(number), D(date), B(boolean), SS(string set), NS(number set).|


#### Example

```
GET /properties
```

##### Response

```json
HTTP 1/1.1 200
{
  "request_id": "18e79cec-ea78-4596-b5fb-135af8024f8a",
  "success": true,
  "errors": [],
  "response": {
    "properties_count": 10,
    "data": [
      {
        "$email": "S",
        "$transaction_id": "S",
        "$transaction_amount": "N",
        "$transaction_currency": "S",
        "$transaction_date": "D",
        "city": "S",
        "first_time_customer": "B",
        "order_delivery_date": "D",
        "order_item_prices": "N",
        "order_item_skus": "S"
      }
    ]
  }
}
```



