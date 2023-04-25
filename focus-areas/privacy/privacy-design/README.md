---
description: Proposed Design to support Privacy Principles
---

# Privacy Design

## Overview

Personally Identifiable Information(PII) of every user should be stored in secured form in the data store. Plain access to any user data will be logged along with the purpose for the access.&#x20;

## Goals&#x20;

1. To ensure data privacy, the data should be stored and communicated in encrypted form as much as possible.&#x20;
2. By default, the secure data would be shown in a masked form. Only when the user explicitly requests plain data access it will be revealed in plain form.&#x20;
   * Plain or masked access to the data will be role-based attribute-level access.&#x20;
   * All the access to the secured data will be logged.

## Architecture

There are the following two approaches to secure the data:

1. [Securing data at API Gateway](privacy-through-api-gateway.md)
2. [Securing data at the Owner's Service](privacy-through-user-service.md)

The details of these two approaches are explained in the next two pages. Either of the two architectures can be used to ensure privacy.&#x20;

### Plain/Masked Access

For all secured data, there will be two-level of access - masked and plain data. At first, based on the user's role, the requesting user will get masked values only. Only if the user explicitly requests for plain value will he/she get access to the plain value. The intention to get the plain values will be passed as part of the Request Header. Any plain data access by a user will be logged.&#x20;

The Audit Log will contain the following details:&#x20;

* requesting the user's id,&#x20;
* timestamp,&#x20;
* data access policy used during decryption,&#x20;
* the purpose of the decryption request, and&#x20;
* the list of user ids whose data was decrypted.&#x20;

Based on these audit logs, any user can trace back who has accessed his/her data.&#x20;

## User Consent

Taking the user's consent to use the private data for various purposes could be done at various granular levels. At a higher level, we can store the user's consent in the user service, and based on the user's choice, we can use the data across multiple modules.&#x20;

Further details on Consent Management are discussed in [consent-based-architecture.md](../consent-based-architecture.md "mention").

## User Data Ownership

As we are storing all user data as part of a single user-data-management service, it should provide APIs to enable users to update their data by providing appropriate proof.&#x20;

## Purpose Limitation

Before taking the user's consent, the purpose of the PII data usage should be defined in a precise and concise manner.&#x20;
