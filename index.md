---
title: Getting started with Boolean
keywords:
tags:
sidebar: mydoc_sidebar
permalink: index.html
---

## What is Boolean?

Boolean is a service for sending single question email surveys. The survey format consists of one question and two predetermined answers. Recipients can respond by clicking one of the answers from within their inbox.

## How is it different?

Boolean surveys get high response rate compared to traditional surveys as it asks only one question.

## Features:
	
### Customizable look of survey

#### Brand logo

It is displayed at the top of the email.

#### Brand name

It is used as “sender name” of the email.

#### Email subject

The default subject is “Quick feedback on _brand name_”. You can change it to “Feedback on _keyword_ with _keyword_”. E.g. “Feedback on order with abcstores.com

#### Reply-to email

By default, survey recipients will not be able to reply to survey email. You can allow replies by providing a reply-to email address. All replies will be sent to this email directly from recipients’ inbox.

### Real time dashboard

You can see response data in real time in our dashboard. “Boolean score” is based on an algorithm which uses additional signals like email opens to give a score between -10 and 10. The higher the number the more positive feedback you got from your users.

### Segmentation

You can segment responses using properties to find patterns in negative response. Read more about segmentation [here](/docs/analyze_responses.html#segmenting-responses).


### Throttling

You can prevent a single survey recipient from getting too many surveys by capping the surveys he/she can receive in a day, week or month. By default, a single recipient will receive a maximum of 1 per day, 2 per week and 4 per month.

### RESTful API

You can use our RESTful API to fully automate your survey workflow. Read API reference [here](/docs/v1_introduction.html).

### Comments

After a survey recipient gives a response we give him/her an option to give comments. You can see all these comments in the dashboard.

### Easy unsubscribing

We add an unsubscribe link in the footer of survey email. Clicking this link will unsubscribe the recipient (email address) from all future emails from an account. You can unsubscribe recipients from specific surveys using our [API](/docs/v1_unsubscribes.html). Recipients can also opt out of Boolean surveys through link in our website.

### Scheduling

By default, all surveys are sent out immediately on request. You can change this behavior by specifying a time in future. Please refer [API docs](/docs/v1_surveys.html) for more information.

