# Integrate URL Shortener Service

## Overview&#x20;

This page runs through the steps involved in integrating the URL shortening service.

## Steps

Utility code to talk to the URL shortener resides here:

```
/utils/UrlShortenerUtil.java
```

Add the following properties in application.properties for integration -

```
#url shortner
egov.url.shortner.host=https://dev.digit.org
egov.url.shortner.endpoint=/egov-url-shortening/shortener
```

