---
description: >-
  This doc will cover how you can set up the tracing on existing environments
  either with help of go lang script or Jenkins deployment jobs.
---

# Jaeger Tracing Setup

The Jaeger tracing system is an open-source tracing system for microservices, and it supports the OpenTracing standard.



## Pre-reads

[https://www.jaegertracing.io/docs](https://www.jaegertracing.io/docs/1.39/)\
[OAuth2-Proxy Setup](https://core.digit.org/guides/operations-guide/oauth2-proxy-setup)\


## Pre-requisites <a href="#prerequisites" id="prerequisites"></a>

* DIGIT uses [golang](https://golang.org/doc/install#download) (required v1.13.3) automated scripts to deploy the builds onto Kubernetes - [Linux](https://golang.org/dl/go1.13.3.linux-amd64.tar.gz) or [Windows](https://golang.org/dl/go1.13.3.windows-amd64.msi) or [Mac](https://golang.org/dl/go1.13.3.darwin-amd64.pkg)
* All DIGIT services are packaged using helm charts[ ![](https://helm.sh/img/favicon-152.png)Installing Helm](https://helm.sh/docs/intro/install/)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) is a CLI to connect to the kubernetes cluster from your machine
* [Install Visualstudio](https://code.visualstudio.com/download) IDE Code for better code/configuration editing capabilities
* Git
* [OAuth2-Proxy Setup](https://core.digit.org/guides/operations-guide/oauth2-proxy-setup)

## Jaeger Tracing Glossary <a href="#jaeger-tracing-glossary" id="jaeger-tracing-glossary"></a>

Agent – A network daemon that listens for spans sent over User Datagram Protocol.

Client – The component that implements the OpenTracing API for distributed tracing.

Collector – The component that receives spans and adds them into a queue to be processed.

Console – A UI that enables users to visualize their distributed tracing data.

Query – A service that fetches traces from storage.

Span – The logical unit of work in Jaeger, which includes the name, starting time and duration of the operation.

Trace – The way Jaeger presents execution requests. A trace is composed of at least one span.

## Jaeger Deployment <a href="#jaeger-deployment" id="jaeger-deployment"></a>

1. Add below Jaeger configs in your env config file (eg. qa.yaml, dev.yaml and, etc…)

```
 jaeger:
  host: ""
  port: ""
  sampler-type: ""
  sampler-param: ""
  collector:
    samplingConfig: |
      {
        "service_strategies": [
          {
            "service": "tl-services",
            "type": "probabilistic",
            "param": 0.5
          },
          {
            "service": "tl-calculator",
            "type": "probabilistic",
            "param": 0.5
          },
          {
            "service": "report-service",
            "type": "probabilistic",
            "param": 0.5
          },
          {
            "service": "pt-services-v2",
            "type": "probabilistic",
            "param": 0.5
          },
          {
            "service": "pt-calculator-v2",
            "type": "probabilistic",
            "param": 0.5
          },
          {
            "service": "collection-services",
            "type": "probabilistic",
            "param": 0.2
          },
          {
            "service": "billing-service",
            "type": "probabilistic",
            "param": 0.2
          },
          {
            "service": "egov-data-uploader",
            "type": "probabilistic",
            "param": 0.2
          },
          {
            "service": "egov-hrms",
            "type": "probabilistic",
            "param": 0.5
          },
          {
            "service": "rainmaker-pgr",
            "type": "probabilistic",
            "param": 0.5
          }
        ],
        "default_strategy": {
          "type": "probabilistic",
          "param": 0.05
        }
      }
```

2\. You can deploy the Jaeger using one of the below methods.

* Deploy using go lang
* `go run main.go deploy -e <environment_name> -c 'jaeger'`
* Deploy using Jenkin’s respective deployment jobs

![](<../../../.gitbook/assets/image (80).png>)

you can connect to the Jaeger console at [https://\<your\_domin\_name>/tracing/](https://egov-micro-qa.egovernments.org/tracing/search)

![](<../../../.gitbook/assets/image (213).png>)

Look at the box on the left-hand side of the page labelled **Search.** The first control, a chooser, lists the services available for tracing, click the chooser and you’ll see the listed services.

Select the service and click the **Find Traces** button at the bottom of the form. You can now compare the duration of traces through the graph shown above. You can also filter traces using “Tags” section under “Find Traces”. For example, Setting the “error=true” tag will filter out all the jobs that have errors.

![](<../../../.gitbook/assets/image (82).png>)

To view the detailed trace, you can select a specific trace instance and check details like the time taken by each service, errors during execution and logs.

## Additional Instructions

If due for some reason you are not able to access the tracing dashboard from your sub-domain, You can use the below command to access the tracing dashboard.

```
kubectl port-forward svc/jaeger-query 8080:80
```

**Note**: port 8080 is for local access, if you are utilizing the 8080 port you can use the different port as well.

To access the tracing hit the browser with this **localhost:8080** URL.

## **Reference Docs**

{% embed url="https://medium.com/velotio-perspectives/a-comprehensive-tutorial-to-implementing-opentracing-with-jaeger-a01752e1a8ce" %}

{% embed url="https://www.scalyr.com/blog/jaeger-tracing-tutorial/" %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
