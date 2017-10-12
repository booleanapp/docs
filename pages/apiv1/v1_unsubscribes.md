---
title: POST /unsubscribes
sidebar: mydoc_sidebar
permalink: v1_unsubscribes.html
---

## POST /unsubscribes

Used to unsubscribe emails. You can only unsubscribe emails which have previously sent surveys.


### JSON parameters

| Parameter | Required | Requirement| Description|
|-----------|----------|------------|------------|
|$email| Yes| email address. Max 75 characters.|Email address to be unsubscribed.|

#### Example

```
POST /unsubscribes?pretty
```

##### JSON Parameters

```json

[
    {
        "$email": "someone@gmail.com"
    },
    {
        "$email": "someonegmail.com"
    }
]
```

##### Response

```json
{
  "request_id": "54bca0c6-33d8-4447-8189-9a09642f9c42",
  "response": [
    {
      "$email": "someone@gmail.com",
      "message": "success",
      "errors": []
    },
    {
      "$email": "ranjith2bipler.com",
      "message": "failure",
      "errors": [
        {
          "code": 1000,
          "message": "Error. \"&#x24;email\" must be a valid email",
          "field": "$email"
        }
      ]
    }
  ]
}
```

#### Error codes

|Code|Message|Description|
|----|-------|-----------|
|1001|Invalid data|Invalid format of data.|
|1005|Email doesn't exist|This email has no previously sent surveys.|
|1007|Email already unsubscribed|Email was unsubscribed in a previous API request.|
|1008|Error while checking email exists|Email validation failed due to internal server error.|
