---
description: Steps to bootstrap DIGIT
---

# Bootstrap DIGIT

#### Topics covered:

* [Steps to Bootstrap DIGIT](bootstrap-digit.md#steps-to-bootstrap)
* [Assess deployment](bootstrap-digit.md#digit-deployment-assessment)
* [Destroy the cluster](bootstrap-digit.md#destroy-the-cluster)

## Overview

Post-deployment, the application can now be accessed from the configured domain. This page provides the bootstrapping steps.

## Bootstrapping Steps

To try out employee login, let us create a sample tenant, city, and user to log in and assign the LME employee role through the seed script.

1. Perform the [kubectl port-forwarding](https://phoenixnap.com/kb/kubectl-port-forward) of the **egov-user** service running from the Kubernetes cluster to your localhost. This provides access to egov-user service and allows users to interact with the API directly.

```
kubectl port-forward svc/egov-user 8080:8080 -n egov
Output:
Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
```

2\. Seed the sample data

* Ensure the Postman is installed to run the following seed data API. if not, [Install postman](https://www.postman.com/downloads/canary/) on your local machine.
*   Import the following Postman collection into the Postman and run it. This contains the seed data that enables sample test users and localisation data.

    [DIGIT Bootstrap](https://raw.githubusercontent.com/egovernments/DIGIT-DevOps/quickstart/deploy-as-code/bootstrap\_scripts/seed\_data.json)

![](<../../.gitbook/assets/image (203).png>)

![](<../../.gitbook/assets/image (83).png>)

3. Execute the below commands to test your local machine's Kubernetes operations through kubectl.

```
#get the pods running in the cluster
kubectl get pods -n egov

Output:

NAME                                                    READY   STATUS    RESTARTS   AGE
citizen-79cf89659c-8glf4                                1/1     Running   0          14d
egov-accesscontrol-78b78dddb9-tfbkf                     1/1     Running   0          21d
egov-enc-service-574cd7b5b5-hmhh4                       1/1     Running   0          36d
egov-idgen-84954b565b-xsnqj                             1/1     Running   0          45d
egov-indexer-5f5fbb6f4b-58rtm                           1/1     Running   0          43d
egov-localization-6cc5977bb9-gm7f9                      1/1     Running   0          27d
egov-mdms-service-65d6d65d8c-t85d9                      1/1     Running   0          21d
egov-user-6676968d76-8n6t6                              1/1     Running   0          29d
egov-workflow-v2-5cdb96bcf5-dcgmf                       1/1     Running   0          36d
employee-749464fbfb-tptlh                               1/1     Running   0          14d
nginx-ingress-controller-b9678869c-mkslb                1/1     Running   0          49d
pgr-services-b9f4ffdbf-5h5kd                            1/1     Running   0          38d
zuul-788bf8cd8b-9nxfl                                   1/1     Running   0          41d


#Delete the pods so that it gets restarted automatically

kubectl delete pods zuul-788bf8cd8b-9nxfl egov-workflow-v2-5cdb96bcf5-dcgmf pgr-services-b9f4ffdbf-5h5kd -n egov

Output:

pod "zuul-788bf8cd8b-9nxfl" deleted
pod "egov-workflow-v2-5cdb96bcf5-dcgmf" deleted
pod "pgr-services-b9f4ffdbf-5h5kd" deleted
```

You have successfully completed the DIGIT Infra, deployment setup and installed a DIGIT - PGR module.

Use the below link in the browser -

```
digit.try.com/employee
```

Use the below credentials to login into the complaint section

* Username: GRO
* Password: eGov@4321
* City: CITYA

## DIGIT Deployment Assessment

By now we have successfully completed the DIGIT setup on the cloud, use the URL you mentioned in your env.yaml.&#x20;

Eg: https://mysetup.digit.org and create a grievance to ensure the PGR module deployed is working fine. Refer to the below product documentation for the steps.

**Credentials:**

1. Citizen: You can use your default mobile number (9999999999) to sign in using the default Mobile OTP 123456.
2. Employee: Username: **GRO** and password: **eGov@4321**

{% embed url="https://urban.digit.org/products/modules/public-grievances-and-redressal/pgr-user-manual" %}

Post grievance creation and assignment of the same to LME, capture the screenshot of the same and share it to ensure your setup is working fine. Post validation, the PGR functionality shares the API response of the following request to assess the correctness of successful DIGIT PGR Deployment.

## Conclusion

All done, we have successfully created infra on the cloud, deployed DIGIT, bootstrapped DIGIT, performed a transaction on PGR and finally destroyed the cluster.
