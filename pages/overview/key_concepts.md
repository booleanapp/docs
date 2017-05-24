---
title: Key concepts
sidebar: mydoc_sidebar
permalink: key_concepts.html
---

## Project

A survey and all its parameters - survey question, predefined answers, logo, email subject, reply-to email address, timezone and throttle limits.

## Survey

An individual email sent as part of a project. You will typically send many surveys in a project. There are two kinds of surveys in Boolean - transactional and non-transactional. You can send both kinds in a project.

### Transactional surveys

Transactional surveys are questions about an order/transaction. You can required to provide four properties of the transaction while sending survey - transaction date, transaction amount, transaction currency and transaction number. These properties will be prominently displayed in the header of survey email. It will increase the legitimacy of the survey for the recipient. Transactional surveys can only be sent using API.

### Non-transactional surveys

Non-transactional surveys are general questions you would ask your users about your product/service. They can be sent from dashboard and using API.

## Response 

The recipient's answer to survey question. He/she can select from one of 2 predefined answers.

## Score

These are the metrics in Boolean for aggregating responses. There are two metrics - “Percentage positive” and “Boolean score”. “Positive score” is the percentage of positive responses. “Boolean score” uses an algorithm which uses additional signals like email opens to give a rating from -10 to +10. The higher the rating the happier are your users. 


