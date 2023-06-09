# Using The Generic GET & POST SMS Gateway Interface

## Overview&#x20;

To use the generic GET/POST SMS gateway, first, configure the service application properties sms.provider.class=Generic

This will set the generic interface to be used. This is the default implementation, which can work with most SMS providers. The generic implementation supports below -

* GET or POST-based API
* Supports query params, form data, JSON body

## Configuration Details

To configure the URL of the SMS provider use sms.provider.url property.

To configure the HTTP method use configure the sms.provider.requestType property to either GET or POST.

To configure form data or json api set sms.provider.contentType=application/x-www-form-urlencoded or sms.provider.contentType=application/json respectively.

To configure which data needs to be sent to the API set the below property:

* sms.config.map={'uname':'$username', 'pwd': '$password', 'sid':'$senderid', 'mobileno':'$mobileno', 'content':'$message', 'smsservicetype':'unicodemsg', 'myParam': '$extraParam' , 'messageType': '$mtype'}
* sms.category.map={'mtype': {'\*': 'abc', 'OTP': 'def'\}}
* sms.extra.config.map={'extraParam': 'abc'}

sms.extra.config.map is not used currently and is only kept for custom implementation which requires data that does not need to be directly passed to the REST API call. sms.config.map is a map of parameters and their values.

Special variables that are mapped -

* $username maps to sms.provider.username
* $password maps to sms.provider.password
* $senderid maps to sms.senderid
* $mobileno maps to mobileNumber from kafka fetched message
* $message maps to the message from the kafka fetched message
* $\<name> any variable that is not from above list, is first checked in sms.category.map and then in application.properties and then in the environment variable with full upper case and \_ replacing -, space or .

So if you use sms.config.map={'u':'$username', 'p':'password'}. Then the API call will be passed \<url>?u=<$username>\&p=password

### Message Success or Failure <a href="#message-success-or-failure" id="message-success-or-failure"></a>

Message success delivery can be controlled using the below properties

* sms.verify.response (default: false)
* sms.print.response (default: false)
* sms.verify.responseContains
* sms.success.codes (default: 200,201,202)
* sms.error.codes

If you want to verify some text in the API call response set sms.verify.response=true and sms.verify.responseContains to the text that should be contained in the response.

### Blacklisting or Whitelisting Numbers <a href="#blacklisting-or-whitelisting-numbers" id="blacklisting-or-whitelisting-numbers"></a>

It is possible to whitelist or blacklist phone numbers to which the messages should be sent. This can be controlled using the below properties:

* sms.blacklist.numbers
* sms.whitelist.numbers

Both of them can be given a separate list of numbers or number patterns. To use patterns use X for any digit match and \* for any number of digits match.

sms.blacklist.numbers=5\*,9999999999,88888888XX will blacklist any phone number starting with 5, or the exact number 9999999999 and all numbers starting from 8888888800 to 8888888899

### Prefixing <a href="#prefixing" id="prefixing"></a>

Few 3rd parties require a prefix of 0 or 91 or +91 with the mobile number. In such a case you can use the sms.mobile.prefix to automatically add the prefix to the mobile number coming in the message queue.
