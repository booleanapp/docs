---
title: Sending surveys
sidebar: mydoc_sidebar
permalink: send_surveys.html
---

It is easy to send surveys in Boolean. It is done in 2 steps:
1.	Create project.
2.	Send surveys.

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

A name for your project. It will default to “<project> <date>”. It can be changed later.

#### Email subject

The default subject is “Quick feedback on <your company name>”. You can change it to “Quick feedback on your <keyword> with <your company name>”. 
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
1.	Go to “send surveys” section.
2.	Import email addresses by either pasting them in comma separated format or importing a CSV file. You can import a maximum of 1000 email addresses in both methods. If you are using CSV method make sure all email addresses are in the first column. You can download a sample CSV file from the link provided.
3.	You will be shown a preview of emails to which surveys will be sent. Boolean will remove duplicates and emails which have already hit daily/weekly/monthly throttle limits. After verifying the list, you can send the surveys by clicking “send”. Your surveys will be delivered in few minutes.


### Sending transactional and non-transactional surveys through API

Read API documentation.

## Properties

You can add data about user’s unique interaction with your product/service as “properties” of a survey. Boolean supports six different types of properties - Number, String, Number set, String set, Date and Boolean. The table below explains each type of property.

|Property type|Examples|
|-------------|--------|
|Number|Order amount, visit count, page views.|
|String|Customer name, Item name, City|
|Boolean|Returning customer (Yes or No)|
|Date|Order date, delivery date|

Properties can be set while sending surveys through API. You can send a maximum of 50 unique properties per project. Adding properties will allow you to segment responses and find reasons for negative feedback. Please read API documentation for detailed guide on sending properties.

## Unsubscribes

A user can opt to stop receiving surveys from a project by clicking unsubscribe link in the email. We have provided this feature to protect users from unwanted email. Unsubscribing is at project level. You can’t re-subscribe an unsubscribed user. Be considerate with the number of surveys you send out to each user. Use “throttling” project setting judiciously. You can also unsubscribe users through API.

