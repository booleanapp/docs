---
title: Analyzing responses
sidebar: mydoc_sidebar
permalink: analyze_responses.html
folder: mydoc
---

## Score

We provide two metrics for survey responses.

### Percentage positive

Percentage of positive responses.

### Boolean score

(No of positive responses - No of negative responses)/(No of email opens) * 10. This metric treats email open with no responses as a soft negative response.


## Segmenting responses

You can segment responses using [properties](/docs/send_surveys.html#properties). A segment is created by combining one or more "conditions". A condition is a property based filter for responses.

### Key concepts in segmentation

#### Operator

An operator is a logic function used to create a "condition". The table below lists available operators.

|Operator|Property types|Example "condition"|
|--------|--------------|-------|
|Less than|Number, Date|Cart value less than 500|
|Less than or equal to|Number, Date|Items in cart less than or equal to 3|
|Greater than|Number, Date|Age greater than 21|
|Greater than or equal to|Number, Date|Cart total greater than or equal to 499|
|Exactly equal|Number, String, Boolean|City name exactly equal to “San Francisco”|
|Exactly not equal|Number, String, Boolean|Customer category exactly not equal to “Enterprise”|
|Is set|Number, String, Number set, String set, Date, Boolean|“Mini bar usage” is set|
|Is not set|Number, String, Number set, String set, Date, Boolean|“Web check-in” is not set|
|Contains|String, String set|Product name contains “organic”|
|Contains exactly|String, Number set, String set|Product name contains exactly “farm fresh”|
|Does not contain|String, Number set, String set|Product name does not contain “phone”|
|on|Date|Order placed on 21-10-2012|

#### Value

Value is data of a property. For example, a “city” property can have value “New York City”. 

#### Condition

It is a combination of property, operator and value. For example, “operating system (property) is (operator) Android (value)”.


### Segmenting responses in dashboard

Follow these steps given below to add a condition:
1.	Click the plus icon. You will immediately see a list of all available properties.
2.	Select a property. You will immediately see list of all available operators for the selected property.
3.	Select an operator. You will immediately see a text box or drop down depending on selected operator.
4.	Input a value.

Scores will update immediately after you add a condition. You can repeat above steps for adding multiple conditions. You can remove a condition by clicking the cross icon. You can add a maximum of 5 conditions in dashboard.
 

### Segmenting responses through API

Read [API documentation](/docs/v1_score.html).
