---
description: Asking for, storing, and managing user's consent
---

# Consent Based Architecture

## Overview

It is mandatory to get the user’s consent before using any PII data. We need to store and maintain users’ consent for each uniquely identified user in the system. The consent management service must be associated with DIGIT’s existing user service.

Each microservice will declare any PII data that it is communicating and/or storing. While storing any PII data in persistent storage, it will be held in encrypted form. If the microservice isn't storing or reading any PII data but just communicating the PII data, it will ignore those values and not validate them.&#x20;

## Consent Management

The Consent Management Component of the DIGIT Platform will manage the consent provided by each user for all the different services offered by DIGIT.&#x20;

The consent management service can be implemented in multiple stages based on the granularity of the consent being requested:

1. When asking for consent to use PII data across all DIGIT services at the time of onboarding: Here, we get the user's consent to use the PII data across all the DIGIT services. Implicitly, this is the way consent management has been implemented in DIGIT.&#x20;
2. Asking for consent only when a user starts using a particular municipal service: Here, we are segregating the use cases based on the different municipal services. The consent management service will have to store the services that the user has consented to. It will also provide a way using which users can revoke their consent.&#x20;
3. Asking for consent even more fine-grained level than the municipal service: This is an extension of the above approach where we ask for user's consent even for core and business services. This might make the system more confusing for the end-user than is necessary so we should re-evaluate this approach before implementing it.&#x20;
