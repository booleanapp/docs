---
title: Analyzing responses
sidebar: mydoc_sidebar
permalink: analyze_responses.html
folder: mydoc
---

## Score

Boolean provides two metrics for analyzing responses at the project level - “Positive score” and “Boolean score”.
### Percentage positive

It is the percentage of positive responses in a time period. You can see this score for all projects in the dashboard page. Once inside a project you can see it in the “score” page. The score page will also have a graph to show the trend of positive score in current week. You can also get this score through API.

### Boolean score

It is a rating from -10 to +10 derived from the formula (count of positive responses - count of negative responses)/(count of survey opens) * 10. We have created this metric because “Positive score” can be misleading at times. For example, if you sent 1000 surveys and got only 10 responses which were all positive you will see a positive score of 100%. This is misleading as majority of your users didn’t give a response. A user opting to not give a response can be treated as a signal of his/her dissatisfaction. “Boolean score” incorporates this signal in its calculation of rating.

## Segmenting responses

You can segment responses to see variations in scores across different combinations of properties. Segments are created through combinations of property conditions. You will be able to find segments which have lower scores compared to overall average. Some aspects of your product/service in these segments are probably causing bad experience to your users. You can improve these aspects and come back to check for improvement in scores. This the true power of Boolean’s one question surveys. High volume user feedback combined with segmentation will give you valuable ideas to improve your product/service.

### Key concepts in segmentation

#### Operator

An operator is a logic function used with properties. The table below lists available operators and allowed property types.

|Operator|Property types|Example|
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

#### Rule

A rule is a logical condition used to validate responses. It is a combination of property, operator and value. For example, “operating system (property) is (operator) Android (value)”. A successful validation is called a “hit” and a failed validation is called a “miss”. One or more rules together form a “filter”. A response will pass a filter if one or more rules is a “hit”.

#### Association

An association defines how multiple rules are used together in filtering responses. In “AND” aggregation a response will pass the filter if all the rules are a hit. In “ANY” aggregation a response will pass the filter it at least one of the rules is a hit.

### Segmenting responses in dashboard

You create a segment by using a filter for responses. You need to select an “association” and add one or more rules to create a filter.

Follow these steps given below to add a rule:
1.	Click the plus icon. You will immediately see a list of all available properties.
2.	Select a property. You will immediately see list of all available operators for the selected property.
3.	Select an operator. You will immediately see a text box or drop down depending on selected operator.
4.	Input a value.

Scores will update immediately after you add a rule. You can repeat above steps for adding multiple rules. You can remove a rule by clicking the cross icon. You can add a maximum of 5 rules.
 

### Segmenting responses through API

Read [API documentation](/docs/v1_score.html).

## Comments

Users can give textual feedback if they wish after giving a survey response. Boolean provides a place for this in the response “thank you” page. You can view all user comments in the “comments” page of a project. We encourage you to regularly read this section to find out unique/rare user experiences which are otherwise missed in the response analysis. You can also get comments through API.

## Statistics

You can find reports on surveys sent, surveys throttled, response rate and open rate in the “statistics” page of a project. You can also get statistics through API.
