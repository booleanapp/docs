---
title: Sending surveys
sidebar: mydoc_sidebar
permalink: send_surveys.html
---

## Create survey

### Basic survey settings

Provide the following minimum settings to create a survey. 

#### Sender name
	
Provide a name to use for sender name of email.

#### Sender logo

Provide a logo to add to the top of email. 

#### Survey question

Provide the survey question (max 60 characters).

#### Positive answer

Provide a positive answer (max 10 characters).

#### Negative answer

Provide a negative answer (max 10 characters).

### Advanced survey settings

These settings are not mandatory. They have good defaults.

#### Survey name

A name for your survey.

#### Email subject

The default subject is “Quick feedback on _sender name_”. You can change it to “Feedback on _keyword_ with _keyword_”. E.g. “Feedback on order with abcstores.com"

#### Reply-to email address

Provide an email address to add to "reply-to" header of email. If not provided any reply to email will be rejected.

#### Time-zone

Select time-zone of for use in dashboard reports.

#### Send throttle (day)

Max number of emails a recipient will recieve in a day. Default is 1. 

#### Send throttle (week)

Max number of emails a recipient will recieve in a week. Default is 2. 

#### Send throttle (month)

Max number of emails a recipient will recieve in a week. Default is 3. 

## Sending surveys

Surveys can be sent through the dashboard or the API.

### Sending surveys through dashboard

#### Copy paste email addresses

1.	Go to “send surveys” section.
2.	Copy paste emails in comma separated format (max 1000 emails).
3.	You will be shown a preview of emails to which surveys will be sent. We will remove duplicates and emails which have already hit daily/weekly/monthly throttle limits. After verifying the list, you can send the surveys by clicking “send”.

#### Send surveys by importing emails through CSV file

This method allows you to add properties for each email.
1.	Go to “send surveys” section.
2. 	Click the "upload" button to select CSV file from your computer (max 1000 emails).
3. 	We will validate the upload file for data errors. After successful validation you will see a "send surveys" button. Click the button to send surveys.

Some points to remember for CSV file:
1. The first row should contain header for each column. Only email column is mandatory.
2. Each property column's header should have property type and property name. For e.g. a string property "city" will should header as "S:city".
3. Refer to [property data guidelines](/docs/v1_messages.html#property-data-types) for each property to fix validation errors. 
4. When a string property has number value use quotes.


### Sending surveys through API

Read [API documentation](/docs/v1_messages.html).

## Properties

Add properties to each recipient to segment responses. We support six different types of properties - Number, String, Number set, String set, Date and Boolean. You can add maximum of 50 unique properties per survey.

|Property type|Examples|
|-------------|--------|
|Number|Order amount, visit count, page views.|
|Number set|Item prices, room prices.|
|String|Customer name, item name, City|
|String set|Screen names, product names|
|Boolean|Returning customer (Yes or No)|
|Date|Order date, delivery date|


### Auto captured properties

We capture the following properties of survey response automatically.

|Property name|Example|
|-------------|--------|
|response_device|Apple iphone 7|
|response_os|iOS 9.3.5|
|response_browser|Mobile Safari 9|


## Unsubscribes

Recipients can opt-out of receiving surveys from an account by clicking unsubscribe link in footer of email. They can also opt-out of Boolean surveys completely using the opt-out form in our website. You can unsubscribe recipients from specific surveys in your account using the [API](/docs/v1_unsubscribes.html). 

## Send limits

We have setup limits on sending surveys to curb abuse. "Free" accounts have a limit of 100 surveys per hour and 500 surveys per day. "Pro" accounts have a limit of 1000 surveys per hour and 5000 surveys per day. Please contact us at support@booleanapp.com to request increase in limit.
