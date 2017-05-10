---
title: Key concepts
sidebar: mydoc_sidebar
permalink: key_concepts.html
summary: Definitions of "Project", "Survey", "Transactional surveys", "Non-transactional surveys", "Response" and "Score"
---

## Project

A specific question to ask your users with positive and negative answer options. You can create multiple projects to ask questions about different aspects of your product/service.

## Survey

An individual email sent to a user as part of a project. You will typically send many surveys in a project. There are two kinds of surveys in Boolean - transactional and non-transactional. We have kept this distinction to slightly change the look of survey depending on its type. You can send both kinds in a project.

### Transactional surveys

Transactional surveys are questions you would ask your users about an order/transaction they placed with you. They can only be sent using REST API. Since a user is likely to have placed multiple orders/transactions with your product it is important to identify the specific order/transaction inside the survey. Boolean does this by displaying four properties of the transaction at the top of the survey email - transaction date, transaction amount, transaction currency and transaction number. These four properties are mandatory for sending a transactional survey. The API will reject survey requests which miss any of the four properties.

### Non-transactional surveys

Non-transactional surveys are general questions you would ask your users about your product/service. They can be sent from dashboard and using REST API. There are no required properties. You can use them for asking general feedback on your product/service to your users.

## Response 

A user’s answer to survey. It can be positive or negative. The positive and negative answers are set when creating a project.

## Score

It is the metric for inferring user satisfaction from survey responses. Boolean provide two metrics - “Positive score” and “Boolean score”. “Positive score” is the percentage of positive responses in a project in a time period. “Boolean score” uses a proprietary algorithm to give a rating from -1 to +1 for a project in a time period. The higher the rating the happier are your users. 


