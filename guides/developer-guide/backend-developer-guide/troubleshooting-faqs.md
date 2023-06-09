# Troubleshooting FAQs

<details>

<summary>What are the recommended versions of tools used by digit?</summary>

**Answer**\
Git - 2.38.1(latest version)

Java - JDK 8

Intellij - 2022.2.3(latest version)

Kafka - 3.2.0(latest version)

Postman - v9.4(latest version)

Kubectl - 1.25.3(latest version)

Postgres - v10

</details>

<details>

<summary>Which IDE is recommended for DIGIT development?</summary>

**Answer**\
Intellij, Eclipse, VS Code or any other preferred IDE can be used. Make sure that it supports Java development and install the Lombok plugin for the IDE.

</details>

<details>

<summary>What are the tools which make development effortless?</summary>

**Answer**\
[Jsonformatter.org](http://jsonformatter.org) is a lightweight tool which is quite handy when it comes to working with sending postman requests and putting objects to Kafka topics. Another such site is [editor.swagger.io](http://editor.swagger.io) which makes reading/designing APIs a lot easier and understandable. Use Postman to test APIs. Use k9s to work with your Kubernetes clusters.

</details>

<details>

<summary>Is it necessary to get a new auth token every few hours?</summary>

**Answer**\
Auth tokens come with an expire period after which you will have to refresh it by hitting the oauth2 APIs.&#x20;

If you don’t want to refresh auth now and again you can port-forward services and get the same result. There are a couple of things to keep in mind though.&#x20;

1. As there are many services to port forward, you must not mix up port numbers while port forwarding.
2. Port forwarding by-passes the zuul api gateway, hence in this case, when accessing a service directly, for a request to be valid, a user has to send the userInfo JSON inside the RequestInfo object.&#x20;

Sample

```json
"userInfo": {
"id": 24226, 
"uuid": "11b0e02b-0145-4de2-bc42-c97b96264807", 
"userName": "sample_user", 
"roles": [
             {
                 "name": "Citizen", 
                 "code": "CITIZEN"
             }
         ]
}
```

</details>

<details>

<summary>What are our options when we get a bad request response in postman?</summary>

**Answer**

You can disconnect the forwarded port and start port forwarding again with recheck on port numbers. If this doesn’t solve the error, in some cases like adding mdms configuration, you can restart the pod to get the desired output.

</details>



\




\
