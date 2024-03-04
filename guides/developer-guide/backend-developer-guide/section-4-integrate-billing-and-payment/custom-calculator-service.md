---
description: Information on creating a custom calculator service
---

# Custom Calculator Service

## Overview

This calculator service integrates with the core platform's billing service & generates a demand. A bill can be fetched based on the demand and presented to the user. This page provides details about creating a custom calculator service.

## Details

Code for the custom calculator service is [here](https://github.com/egovernments/DIGIT-OSS/tree/master/tutorials/backend-developer-guide/btr-calculator). A separate API spec is written for the calculator service.

A calculator service typically has three APIs:

1. \_calculate - This API returns the calculation for a given service application.
2. _getbill or_ createbill - Creates and returns the bill associated with a particular application.
3. \_search - to search for calculations.

The birth registration service calls the \_calculate API to generate a demand for birth registration charges.
