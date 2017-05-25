---
title: Getting started with Boolean
keywords:
tags:
sidebar: mydoc_sidebar
permalink: index.html
---

## What is Boolean?

Boolean is a service for sending single question surveys. The survey format consists of one question and two predetermined answers. Surveys are sent by email. Recipients can respond by clicking one of the answers from within their inbox.

## How is it useful?

Traditional surveys don’t get many responses because their long. Even the minimal responses they get don’t have legitimacy due to low response percentage. Boolean solves this problem. In Boolean you can ask only one question in a survey. Users will love you for not troubling them with a long and boring survey. They will respond in huge numbers. The one question you ask can be anything related to your product or service. We encourage you to ask a general feedback question. E.g. “How was your experience ordering with us?” Answer - “Good” or “Bad”.

## How do I get insights from responses?

You might want to know why survey recipients are giving positive or negative response. Boolean’s segmentation feature will give you the likely answer. You can use this feature by sending key-value pair meta data with every survey request. You can later segment responses using this meta data. This way you could pin point the finer aspects of your product or service which is contributing to positive or negative response. Read more about segmentation [here](/docs/analyze_responses.html#segmenting-responses).


## Features:
	
### Fully customizable

You can customize the following aspects of survey:

#### Brand logo

This is the image which appears above the question.

#### Brand name

This is used in “sender name” of email and “alt text” of brand logo.

#### Email subject

The default subject is “Quick feedback on _brand name_”. You can change it to “Feedback on _keyword_ with _keyword_”. E.g. “Feedback on order with abcstores.com

#### Reply-to email

By default, survey recipients will not be able to reply to survey email. You can allow replies by providing a reply-to email address. All replies will be sent to this email directly from recipients’ inbox.

### Real time dashboard

You can see response data in real time in our dashboard. “Boolean score” is based on an algorithm which uses additional signals like email opens to give a score between -10 and 10. The higher the number the more positive feedback you got from your users.

### Segmentation

Read more about segmentation [here](/docs/analyze_responses.html#segmenting-responses).

### High quality inbox delivery

We work with high quality email delivery partners to make sure your surveys are delivered fast and reach the “primary” inbox.

### Throttling

You can prevent a single survey recipient from getting too many surveys by capping the surveys he/she can receive in a day, week or month. By default, a single recipient will receive a maximum of 1 per day, 2 per week and 4 per month.

### RESTful API

You can use our RESTful API to fully automate your survey workflow. Read API reference [here](/docs/v1_introduction.html).

### Comments

After a survey recipient gives a response we give him/her an option to give comments. You can see all these comments in the dashboard.

### Easy unsubscribing

We add an unsubscribe link in the footer of survey email. Clicking this link will unsubscribe the recipient (email address) from all future surveys in the project. You can also unsubscribe recipients using our [API](/docs/v1_unsubscribes.html). Please note that unsubscribe is at project level.

### Scheduling

By default, all surveys are sent out immediately on request. You can change this behavior by specifying a time in future. Please refer [API docs](/docs/v1_surveys.html) for more information.

