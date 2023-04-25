# URL Shortening Service

## Overview <a href="#overview" id="overview"></a>

The URL shortening service is used to shorten long URLs. There may be a requirement when we want to avoid sending very long URLs to the user via SMS, WhatsApp etc. This service compresses the URL.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

1. Prior knowledge of Java/J2EE
2. Prior knowledge of SpringBoot
3. Prior knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

1. Compress long URLs
2. Converted short URLs contain id, which is used by this service to identify and get longer URLs.

| Environment Variable   | Description                                                                   |
| ---------------------- | ----------------------------------------------------------------------------- |
| host.name              | Host name to append in short URL                                              |
| db.persistance.enabled | The boolean flag to store the short URL in database when flag is set as TRUE. |

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

* Deploy the latest version of the URL Shortening service

## API Details <a href="#api-details" id="api-details"></a>

#### a) `POST /egov-url-shortening/shortener` <a href="#a-post-egov-url-shortening-shortener" id="a-post-egov-url-shortening-shortener"></a>

Receive long URLs and converts them to shorter URLs. Shortened URLs contain URLs to the endpoint mentioned next. When a user clicks on shortened URL, the user is redirected to a long URL.

#### b) `GET /{id}` <a href="#b-get-id" id="b-get-id"></a>

This shortened URL contains the path to this endpoint. The service uses the id used in the last endpoint to get the long URL. In response, the user is redirected to the long URL.

## Reference Docs <a href="#reference-docs" id="reference-docs"></a>

### Doc Links <a href="#doc-links" id="doc-links"></a>

| Title                                                                                                                                                           |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Swagger API Contract](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/core-services/master/docs/url-shortening\_contract.yml#!/) |
| [URL Shortening Local Setup](https://github.com/eGovStack/core-services/blob/master/egov-url-shortening/LOCALSETUP.md)                                          |
