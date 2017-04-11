---
title: Documentation
description: 
---
# Introduction

## What is Boolean?

Boolean helps you send one question email surveys to your users. Recipients can answer the question with a single click from within their inbox.

## What kind of questions can I ask?

You can ask any question. You have to provide 2 choices for answer. One choice should be positive and other negative.

## How do I get insights from responses?

Our dashboard will show you real time scores on positive and negative responses. You can tag surveys with meta data and use our segmentation feature to slice and dice responses. Using segmentation, you will be able to find deficiencies in your product/service which are causing negative responses.

## Why only one question?

Traditional feedback surveys don’t get many responses because they are too long and specific. Boolean’s one question tremendously reduces the effort to respond resulting in high response rate. You don’t lose the specifics as survey meta data can be analyzed to find deficiencies in your product/service.

## How do I get help?

Please email us at support@booleanapp.com. You can expect a fast reply during (9AM EST to 5PM EST) and (4:30 AM GMT to 11:30AM GMT) on weekdays. We will respond to emails received during weekend on Monday in the order they were received.

# Key Concepts

## Project

A specific question to ask your users with positive and negative answer options. You can create multiple projects to ask questions about different aspects of your product/service.

## Survey

An individual email sent to a user as part of a project. You will typically send many surveys in a project. There are two kinds of surveys in Boolean - transactional and non-transactional. We have kept this distinction to slightly change the look of survey depending on its type. You can send both kinds in a project.

## Transactional surveys

Transactional surveys are questions you would ask your users about an order/transaction they placed with you. They can only be sent using REST API. Since a user is likely to have placed multiple orders/transactions with your product it is important to identify the specific order/transaction inside the survey. Boolean does this by displaying four properties of the transaction at the top of the survey email - transaction date, transaction amount, transaction currency and transaction number. These four properties are mandatory for sending a transactional survey. The API will reject survey requests which miss any of the four properties.

## Non-transactional surveys

Non-transactional surveys are general questions you would ask your users about your product/service. They can be sent from dashboard and using REST API. There are no required properties. You can use them for asking general feedback on your product/service to your users.

## Response

A user’s answer to survey. It can be positive or negative. The positive and negative answers are set when creating a project.

## Score

It is the metric for inferring user satisfaction from survey responses. Boolean provide two metrics - “Positive score” and “Boolean score”. “Positive score” is the percentage of positive responses in a project in a time period. “Boolean score” uses a proprietary algorithm to give a rating from -1 to +1 for a project in a time period. The higher the rating the happier are your users. 

# Sending surveys

It is easy to send surveys in Boolean. It is done in 2 steps:

1. Create project.
2. Send surveys.

## Create project

### Basic project settings

You will need to provide the following minimum settings to create a project. 

#### Company name

Provide the name of your Company. It will be used in the survey email subject. The standard subject of all surveys is “Quick feedback on <product/service name>”. 

#### Company logo

Upload a easily identifiable logo of your product/service. It will be used in the header of survey email. 

#### Survey question

Provide the question to ask your users (max 60 characters).

#### Positive response

Provide the positive answer for your question (max 10 characters). This answer will have a green background in the survey email.

#### Negative response

Provide the negative answer for your question (max 10 characters). This answer will have a red background in the survey email.

### Advanced project settings

These settings are not compulsory. They have good defaults. You can customize them if you want.

#### Project name

A name for your project. It will default to “__project__ __date__”. It can be changed later.

#### Email subject

The default subject is “Quick feedback on __your company name__”. You can change it to “Quick feedback on your __keyword__ with __your company name__”. 
For example, an E-Commerce company use “Quick feedback on your order with abcshoes.com”. For example an Airline company can use “Quick feedback on your flight with abcairlines”.

#### Reply-to email address

Boolean will add this email address to the “reply-to” header of survey email. If any of your users reply to survey email it will be sent to this address. Otherwise by default any reply to survey email will be rejected. We encourage you to add your customer support email address to here to get valuable feedback directly to your support inbox.

#### Time-zone

Select time-zone of your location. It will be used as basis for all dashboard reports. You can change it later. If you and your users are located in different time zones, then we suggest you use your time zone as it will suit your daily schedule. 

#### Send throttle (day)

It is not a good idea sending too many surveys to a single user. So Boolean throttles the number of surveys an individual user (unique email address) gets in a day, week and month. Boolean will ignore any new survey requests for a throttled user. By default, a user will get maximum 1 survey per project per day. You can increase it to 2. 

#### Send throttle (week)

By default, a user will get maximum 2 survey per project per week. You can increase it up to 4.

#### Send throttle (month)

By default, a user will get maximum 3 survey per project per month. You can increase it up to 6.

## Sending surveys

Once a project is created you can immediately start sending surveys. There are 2 ways to send surveys - sending from dashboard, sending through API. Please note that you can send non-transactional surveys only from dashboard.

### Sending non-transactional surveys

You can quickly send non-transactional surveys from within the dashboard. All you need is a list of your user’s email addresses.

1. Go to “send surveys” section.
2. Import email addresses by either pasting them in comma separated format or importing a CSV file. You can import a maximum of 1000 email addresses in both methods. If you are using CSV method make sure all email addresses are in the first column. You can download a sample CSV file from the link provided.
3. You will be shown a preview of emails to which surveys will be sent. Boolean will remove duplicates and emails which have already hit daily/weekly/monthly throttle limits. After verifying the list, you can send the surveys by clicking “send”. Your surveys will be delivered in few minutes.

### Sending transactional and non-transactional surveys through API

Read [API documentation](/api/).

### Properties

You can add data about user’s unique interaction with your product/service as “properties” of a survey. Boolean supports six different types of properties - Number, String, Number set, String set, Date and Boolean. The table below explains each type of property.

|Property type|Examples|
|-------------|--------|
|Number|Order amount, visit count, page views|
|String|Customer name, Item name, City|
|Number set|Order item prices, Delivery zip codes|
|String set|Order item names, Delivery city names|
|Boolean|Returning customer (Yes or No)|
|Date|Order date, delivery date|

Properties can be set while sending surveys through API. You can send a maximum of 50 unique properties per project. Adding properties will allow you to segment responses and find reasons for negative feedback. Please read [API documentation](/api/) for detailed guide on sending properties.

### Unsubscribes

A user can opt to stop receiving surveys from a project by clicking unsubscribe link in the email. We have provided this feature to protect users from unwanted email. Unsubscribing is at project level. You can’t re-subscribe an unsubscribed user. Be considerate with the number of surveys you send out to each user. Use “throttling” project setting judiciously. You can also unsubscribe users through API.

# Analyzing responses

## Score

Boolean provides two metrics for analyzing responses at the project level - “Positive score” and “Boolean score”. Both these metrics attempt to capture overall satisfaction of your users. 

## Positive score

It is the percentage of positive responses in a time period. You can see this score for all projects in the dashboard page. Once inside a project you can see it in the “score” page. The score page will also have a graph to show the trend of positive score in current week. You can also get this score through API.

## Boolean score

It is rating from -1 to +1 derived from count of positive responses, negative responses and no responses (and email not opened) and no responses (and email opened). We have created this metric because “Positive score” can be misleading at times. For example, if you sent 1000 surveys and got only 10 responses which were all positive you will see a positive score of 100%. This is misleading as majority of your users didn’t give a response. A user opting to not give a response can be treated as a signal of his/her dissatisfaction. “Boolean score” incorporates this signal in its calculation of rating. Since Boolean knows when a survey is delivered or opened by user it can use a “no response” as a signal with confidence.
You can see this score for all projects in the dashboard page. Once inside a project you can see it in the “score” page. You can also get this score through API.

## Segmenting responses

You can segment responses to see variations in scores across different combinations of properties. You will be able to find segments which have lower scores compared to overall average. Some aspects of your product/service in these segments are probably causing bad experience to your users. You can improve these aspects and come back to check for improvement in scores. This the true power of Boolean’s one question surveys. High volume user feedback combined with segmentation will give you valuable ideas to improve your product/service.

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

1. Click the plus icon. You will immediately see a list of all available properties.
2. Select a property. You will immediately see list of all available operators for the selected property.
3. Select an operator. You will immediately see a text box or drop down depending on selected operator.
4. Input a value.

Scores will update immediately after you add a rule. You can repeat above steps for adding multiple rules. You can remove a rule by clicking the cross icon. You can add a maximum of 5 rules.

#### Top hits segmentation

Sometimes you would like to compare scores of most popular values for property. For example, E-commerce company would like to compare scores of its 10 most popular delivery cities. Boolean’s “Top hits segmentation” feature can do this automatically for you. Just select the relevant property from the “Top hits segmentation” drop down. The graph will automatically update with score trends of top 10 values of selected property. The values are selected based on number of responses they received. This feature saves you lot of time as the alternative would be to find top 10 values manually, create a filter for each value, record it’s score and compare. When using this feature, you don’t even need to know the top values for a property! 

### Segmenting responses through API

Read API documentation.

### Comments

Users can give textual feedback if they wish after giving a survey response. Boolean provides a place for this in the response “thank you” page. You can view all user comments in the “comments” page of a project. We encourage you to regularly read this section to find out unique/rare user experiences which are otherwise missed in the response analysis. You can also get comments through API.

### Statistics

You can find reports on surveys sent, surveys throttled, response rate and open rate in the “statistics” page of a project. You can also get statistics through API.

# Managing Account

## General settings

You can change your name, company name, email address and password in the “General” section of account page. 

## Credits

You need to buy credits to send surveys. One credit is worth one survey email. Once bought your credits never expire. Boolean deducts credits in small batches when sending surveys. You will not be charged for throttled surveys. You will be charged for surveys which bounced. When your credits run out surveys requests will be rejected.

### Buying credits

You can easily buy credits using credit/debit card in the “accounts” section. Follow these steps:

1. Choose a credits pack. 
2. Choose to enable or disable auto-renewal of credits. You if you enable Boolean will automatically re-order your chosen credit pack when you exhaust 90% of credits. You can disable auto-renew later if you change your mind.
3. Give your credit/debit card details. You can opt to save your card for future purchases. You can delete it later if you change your mind. It is mandatory to save card if you choose to auto-renew credits. We use Stripe to store your card details.
4. Complete purchase.

In case your credit card is charged and transaction failed please contact us at support@booleanapp.com. We will promptly complete the order or issue you a full refund.









