---
title: Sending surveys
sidebar: mydoc_sidebar
permalink: send_surveys.html
---

## Create survey

### Basic survey settings

You will need to provide the following minimum settings to create a survey. 

#### Sender name
	
Provide a name for your product/service. It is used in email sender name, subject and “alt text” of logo in email. Default email subject is “Quick feedback on _sender name_”. 

#### Sender logo

Upload a easily identifiable logo of your product/service. It will be used in the header section of survey email. 

#### Survey question

Provide the question to ask your users (max 60 characters).

#### Positive answer

Provide the positive answer for your question (max 10 characters). This answer will have a green background in the survey email.

#### Negative answer

Provide the negative answer for your question (max 10 characters). This answer will have a red background in the survey email.

### Advanced survey settings

These settings are not compulsory. They have good defaults.

#### Survey name

A name for your survey. It will default to survey date_. It can be changed later.

#### Email subject

The default subject is “Quick feedback on _sender name_”. You can change it to “Feedback on _keyword_ with _keyword_”. E.g. “Feedback on order with abcstores.com

#### Reply-to email address

Boolean will add this email address to the “reply-to” header of survey email. If any of your users reply to survey email it will be sent to this address. Otherwise by default any reply to survey email will be rejected. We encourage you to add your customer support email address to here to get valuable feedback directly to your support inbox.

#### Time-zone

Select time-zone of your location. It will be used as basis for all dashboard reports. You can change it later. If you and your users are located in different time zones, then we suggest you use your time zone as it will suit your daily schedule. 

#### Send throttle (day)

It is not a good idea sending too many emails to a single user in the same survey. So Boolean throttles the number of emails an individual user (unique email address) gets in a day, week and month. Boolean will ignore any new survey requests for a throttled user. By default, a user will get maximum 1 email per survey per day. You can increase it to 2. 

#### Send throttle (week)

By default, a user will get maximum 2 emails per survey per week. You can increase it up to 4.

#### Send throttle (month)

By default, a user will get maximum 3 emails per survey per month. You can increase it up to 6.

## Sending surveys

Once a survey is created you can immediately start sending survey emails. There are 2 ways to send surveys - sending from dashboard, sending through API.

### Sending surveys from dashboard

You can quickly send non-transactional surveys from within the dashboard. All you need is a list of your user’s email addresses. 
1.	Go to “send surveys” section.
2.	Import email addresses by either pasting them in comma separated format (max 1000 emails).
3.	You will be shown a preview of emails to which surveys will be sent. Boolean will remove duplicates and emails which have already hit daily/weekly/monthly throttle limits. After verifying the list, you can send the surveys by clicking “send”. Your surveys will be delivered in few minutes.


### Sending surveys through API

Read [API documentation](/docs/v1_messages.html).

## Properties

You can add key-value pair meta data about as “properties” of a survey. Boolean supports six different types of properties - Number, String, Number set, String set, Date and Boolean. The table below explains each type of property.

|Property type|Examples|
|-------------|--------|
|Number|Order amount, visit count, page views.|
|Number set|Item prices, room prices.|
|String|Customer name, item name, City|
|String set|Screen names, product names|
|Boolean|Returning customer (Yes or No)|
|Date|Order date, delivery date|


Properties are set while sending surveys through API. You can send a maximum of 50 unique properties per survey. Adding properties will allow you to segment responses and find reasons for negative feedback. Please read API documentation for detailed guide on sending properties.

## Unsubscribes

A user can opt to stop receiving emails from a survey by clicking unsubscribe link in the email. We have provided this feature to protect users from unwanted email. Unsubscribing is at survey level. You can’t re-subscribe an unsubscribed user. Be considerate in the number of emails you send out to a user in a single survey. Use “throttling” survey setting judiciously. You can also unsubscribe users through API.

