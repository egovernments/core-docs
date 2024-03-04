---
description: Steps to model requirements for workflows, user stories
---

# Model Requirements

## Overview

This document provides details on how to model the requirements for workflows, user stories and process indicators.&#x20;

## **Steps - Model the Service Process Workflow**

Given the requirements document from your business analyst, create a process model that looks as follows. It captures who (role) does what (activity) in what sequence to accomplish the outcome.&#x20;

![Workflow diagram for  birth certificate registration](<../../.gitbook/assets/image (305).png>)

Start by identifying the users. The users could be citizens, vendors or employees. It is important to identify the roles the users are playing e.g. in the above the citizen is the "Applicant", Vendor is the "Verifier" and the Head of Department is the "Approver".&#x20;

{% hint style="info" %}
**DIGIT Concepts**

**Tenant - DIGIT** is a hierarchical multi-tenant system. The state can be a tenant. Departments can be the next-level tenant. So Punjab can be a tenant denoted by pb. The education department can be denoted by pb.education.&#x20;

**Role -** Role can be configured to provide a set of access to the user. The "Approver" Role allows users to approve or reject the application but does not allow the user to edit the application.&#x20;

**User -** When a user is created in DIGIT, they are mapped to tenant and role. So they have access only to those data that belong to that Tenant and can perform only those activities as defined in the role.&#x20;

**Workflow -** Workflow is defined as a set of states e.g. New, Submitted, Verified, Approved. At each stage, different roles can perform different actions e.g. Verifier can verify an application only when the application is in the "Submitted" state. Abstracting workflows allows DIGIT to configure different workflows for different tenants. For instance, if Jalandhar wants to configure additional roles and steps in the Birth Certificate process (as compared to Amritsar) then it will be possible to do so.&#x20;
{% endhint %}

For each role draw a swim lane (grey horizontal bar in the above diagram) which contains all the activities (boxes and rhombus). The activities should ideally be expressed in a "Verb Noun" pattern e.g. pay charges, verify application and so on.&#x20;

### **Elaborate Activities**

Activities can be elaborated in two ways - as a user story or a use case. User Stories are an informal way of expressing what the user wants e.g. “As a \[persona], I \[want to], \[so that].”&#x20;

_As an Applicant, I want to be able to provide enter the form as quickly as possible. I want to know the process and when the certificate will be available to me._&#x20;

Use Case is a more formal way of capturing exact steps and alternate flows the user can follow e.g.&#x20;

_The Applicant logs into the system by entering the user name and password. The applicant then enters the following fields - child's name, mother's name, father's name, date of birth, and place of birth. All these fields are mandatory._&#x20;

If you are following an agile process then the user story-based approach works fine. Agile also works well when you are not clear about the end outcome and want to iterate. However, if you are clear about what you want and also want to avoid too much back & forth communication between the product and engineering team during development with predictable outcomes then go with the use case-based approach.&#x20;

### **Elaborate Process Performance Indicators**

Identify the process performance indicators that an administrator may want to see to monitor and identify areas of improvement. For example, the administrator may want to see the following metrics and compare them over various time periods and administrative hierarchies.

1. Number of applications
2. Number of applications by status
3. Average time to deliver the applications
4. Average time by status
5. Average feedback
6. Number of complaints
7. Number of complaints by status
8. Average time to resolve complaints
9. Number of reopened complaints
