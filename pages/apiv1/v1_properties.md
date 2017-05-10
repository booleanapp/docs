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
|type|No|S or N or D or B or SS or NS|An optional filter to list specific kind of properties - S(string), N(number), D(date), B(boolean), SS(string set), NS(number set)|


#### Example

GET `/properties`

##### Response

```json
HTTP 1/1.1 200
{
  "request_id": "c3f1e787-29bf-4f68-9c82-4c8c5ff19c9e",
  "errors": [],
  "response": {
    "properties_count": 35,
    "data": [
              {
              	"$email": "S",
                "$transaction_id": "S",
                "$transaction_amount": "N",
                "$transaction_currency": "S",
                "$transaction_date": "D",
                "flight_no": "S",
                "origin": "S",
                "destination": "S",
                "sector": "S",
                "aircraft": "S",
                "aircraft_serial_no": "S",
                "ticket_booking_date": "D",
                "ticket_booking_mode": "S",
                "discounted_ticket": "B",
                "website_customer_id": "N",
                "customer_gender": "S",
                "checkin_baggage_weight_KG": "N",
                "preordered_food_skus": "SS",
                "preordered_food_prices_inr": "NS",
                "seat_no": "S",
                "flight_passenger_count": "N",
                "crew_count": "N",
                "captain_id": "S",
                "head_cabin_crew_id": "S",
                "cabin_crew_ids": "SS",
                "checkin_officer_id": "S",
                "boarding_officer_id": "S",
                "boarding_gate": "S",
                "stops": "N",
                "check_in_time": "D",
                "boarding_time": "D",
                "scheduled_departure_time": "D",
                "actual_departure_time": "D",
                "scheduled_arrival_time": "D",
                "actual_arrival_time": "D",
                "arrival_delay_mins": "N"
      }
    ]
  }
}
```

#### Error codes



