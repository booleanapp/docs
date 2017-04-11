---
title: /Responses
description: 
---

## GET /responses

Used to list user responses

### URL parameters

|Parameter|Required|Requirement|Description|
|---------|--------|-----------|-----------|
|start_date|No|YYYY:MM:DD (time assumed midnight) or YYYY:MM:DDTHH:MM:SS. Timezone inferred from project setting.|The start date to retrieve responses.|
|end_date|No|YYYY:MM:DD (time assumed midnight) or YYYY:MM:DDTHH:MM:SS. Timezone inferred from project setting.|The end date to retrieve responses.|
|page|No|Integer. Min 1. Max 20.|Optional parameter to specify page number. To be used with size parameter.|
|size|No|Integer. Min 10. Max 100.|Optional parameter to specify number of results per page.|
|email|No|email address. Max 75 characters.|Optional parameter to search for a particular email.|
|feedback|No|1 or 0|An optional filter to retrieve only positive or negative feedbacks. By default, both positive and negative feedbacks are returned. To get only positive feedback specify 1. To get only negative feedback specify 0.|
|comments|No|True or false|An optional filter to retrieve only responses with comments. By default, all responses are returned. To get only responses with comments set this parameter to true.|
|keyword|No|String. Max 50 characters.|An optional filter to search for a particular keyword in comments.|
|sort_order|No|ASC or DSC|An optional sort order for the responses based on creation time. The default is asc, which will return responses in chronological order by (oldest first). To get responses in reverse chronological order (newest first), specify desc.|

#### Example

GET `/responses?start_date=2016-08-16&end_date=2016-08-17&size=10`

_Update the response with proper URL later example `https://api.booleanapp.com/v1/responses?start_date=2016-08-16&end_date=2016-08-17&page=1&size=10&feedback=0&comments=true&keyword=bad&sort_order=desc`_

##### Response

```json
HTTP 1/1.1 200
{
  "request_id": "c3f1e787-29bf-4f68-9c82-4c8c5ff19c9e",
  "errors": [],
  "response": {
    "total": 92,
    "size": 10,
    "page": 1,
    "responses": [
      {
        "$response_received_at": "2016-08-16T09:48:14.353Z",
        "$transaction_id": "57b2e132d734a9253df1c49f",
        "$email": "booleanmoron2@bipler.com",
        "$feedback": -1
      },
      {
        "$response_received_at": "2016-08-16T09:56:16.784Z",
        "$transaction_id": "57b2e1cf3421f2947a8023b3",
        "$email": "booleanmoron1@gmail.com",
        "$feedback": 1
      },
      {
        "$response_received_at": "2016-08-16T09:56:20.766Z",
        "$transaction_id": "57b2e1cf41301931cc85faa9",
        "$email": "booleanmoron3@bipler.com",
        "$feedback": 1
      },
      {
        "$response_received_at": "2016-08-16T09:56:25.079Z",
        "$transaction_id": "57b2e1cf90aa4b74ac516397",
        "$email": "booleanmoron2@bipler.com",
        "$feedback": 1
      },
      {
        "$response_received_at": "2016-08-16T09:56:28.559Z",
        "$transaction_id": "57b2e1cfe69022f4993743a3",
        "$email": "booleanmoron1@yahoo.com",
        "$feedback": 1
      },
      {
        "$response_received_at": "2016-08-16T09:56:31.980Z",
        "$transaction_id": "57b2e1cfc3425c58e601ad13",
        "$email": "booleanmoron1@bipler.com",
        "$feedback": 1
      },
      {
        "$response_received_at": "2016-08-16T09:56:38.409Z",
        "$transaction_id": "57b2e1cf712175937989c989",
        "$email": "booleanmoron2@bipler.com",
        "$feedback": -1
      },
      {
        "$response_received_at": "2016-08-16T09:56:46.138Z",
        "$transaction_id": "57b2e1cf40a9db8551a37477",
        "$email": "booleanmoron1@bipler.com",
        "$feedback": 1
      },
      {
        "$response_received_at": "2016-08-16T09:56:54.320Z",
        "$transaction_id": "57b2e1cf96e16b2632760d43",
        "$email": "booleanmoron3@bipler.com",
        "$feedback": 1
      },
      {
        "$response_received_at": "2016-08-16T09:56:59.073Z",
        "$transaction_id": "57b2e1cf17732a9cbbf3842f",
        "$email": "booleanmoron1@yahoo.com",
        "$feedback": -1
      }
    ]
  }
}
```

#### Error codes

|Code|Message|Description|
|----|-------|-----------|
|1001|Invalid format|Invalid format of data|
|1009|Invalid Value|Value is incorrect for given field.|

#### Notes

* Results are paginated by default with 30 results per page. Use "link" header to find URL of next page.

* "$response_received_at" is the timestamp of user response.

* "Feedback" equals to 0 means negative. "Feedback" equals to 1 means positive.
