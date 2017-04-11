---
title: /Unsubscribes
description: 
---

## POST /unsubscribes

Used to unsubscribe an email through API.

### JSON parameters

| Parameter | Required | Requirement| Description|
|-----------|----------|------------|------------|
|$email| Yes| email address. Max 75 characters.|Email address which needs to be unsubscribed from client’s feedback emails.|

#### Example

POST `https://api.booleanapp.com/v1/unsubscribes`

##### JSON Parameters

```json

[
    {
        "$email": "ranjith@bipler.com"
    },
    {
        "$email": "ranjith2bipler.com"
    }
]
```

##### Response

```json
HTTP1/1.1 200
{
    "request_id": "qzbuypp-okpzgzx-zcurvnt-eartoui",
    "response": [
        {
            "$email": "ranjith@bipler.com",
            "message": "success",
            "errors": []
        },
        {
            "$email": "ranjith2bipler.com",
            "message": "failure",
            "errors": [
                {
                    "code": 1001,
                    "field": "email",
                    "message": "Wrong email format"
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
|1005|Email doesn’t exist|The email is not available in database.|
|1007|Email already unsubscribed|Email was unsubscribed in a previous API request.|
|1008|Error while checking email exists|Email validation failed due to internal server error.|
