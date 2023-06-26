---
description: >-
  In this tutorial, we will go through the step by step process to setup
  Deployment Job to the Jenkins
---

# Deployment Job Pipeline Setup

### DIGIT-Deployment Jobs:

* You may have doubts about what is deployment jobs? Below we explained about deployment jobs in detail.

### What are deployment jobs?

* Once we build a pipeline using jenkins we need to deploy(to set out) into  a environment. For that we nee deployment jobs. Here, deployment jobs are nothing but the clusters(group of nodes or VM's)which are created using different environments. some of the environments that are present in **DIGIT-DevOps:**

<figure><img src="../../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

* In DIGIT there are so many deployment jobs are there. Go to the following repo to see all the deployment jobs.

```
https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/ci.yaml
```

* Here you can see some of the deployment jobs that are present in DIGIT-DevOps.

```
deploymentJobs:
    - name: dev
      acl: [egovernments*micro-service-dev]
    - name: bihar-prod
      acl: [egovernments*bihar-prod]
    - name: bihar-dev
      acl: [egovernments*bihar-dev]
    - name: bihar-uat
      acl: [egovernments*bihar-uat]
    - name: qa
      acl: [egovernments*micro-service-qa] 
    - name: uat
      acl: [egovernments*micro-service-uat] 
    - name: ukd-dev
      acl: [egovernments*ukd-dev] 
    - name: ukd-prod-sdc
      acl: [egovernments*ukd-prod] 
    - name: ukd-sdc-uat
      acl: [egovernments*ukd-uat]                 
    - name: ci
      acl: [egovernments*micro-service-devops]      
    - name: ukd-dev-sdc
      acl: [egovernments*ukd-dev]
    - name: staging
      acl: [egovernments*staging-qa] 
    - name: nugp-demo
      acl: [egovernments*nugp-team] 
    - name: central-instance
      acl: [egovernments*micro-service-dev,egovernments*micro-service-qa]
```

#### What is acl?

* Access control list (ACL) An access-control list is a list of permissions attached to an aws.
* An ACL specifies which users or system processes can view, create, modify, delete, or otherwise manage objects.
* Simply, ACL is a list of members in team and they can only able to access that job.

#### To deploy new job:

*   [x] Add your **Job name** and **acl** in below path under **deployment jobs:**    in **ci.yaml file.**\
    \
    egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo.yaml

    <figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>
* [x] We already discussed that deployments jobs are nothing but clusters. So, add the **kubeconfigs** of the cluster in the below **ci-secrets.yaml.**

```
https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo-secrets.yaml
```

<figure><img src="../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

* [x] If you are using the DIGIT-DevOps repo's **release** branch for deployment, this step is optional.  Other branches require job-name-specific conditions in seed-deployment-jobs helm/charts/jenkins/values.yaml**.** Add your respective **repo, branch** names

1. **Repo**: To which repository the deployment job be added.
2. **Branch**: Usually master branch.
3. **Helm Directory**: deploy-as-code/helm
4. **Environment**: Add job-name here.

```
{{- else if (eq $job.name "dev") }}            
deployer(repo:'git@github.com:egovernments/iFix-DevOps.git', branch: 'dev', helmDir: 'deploy-as-code/helm', environment: '{{ $job.name }}')""")
      sandbox() 
    }
}
disabled(false)
}
```

\
refer this link`egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/charts/backbone-services/jenkins/values.yam` for more`info`

* [x] To deploy, we should be in **deployer** path. For that go to the below path

```
DIGIT-DevOps/deploy-as-code/deployer
```

* [x] Re-deploy jenkins:

```
go run main.go -c -e ci 'jenkins' 
```

### Deployment Job pipeline:

* [x] Like this deployment jobs can be created in jenkins. Go to **deployments** and switch to any deployment job where you want to deploy in jenkins

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

* [x] Paste the **image id** which you have copied from the builds and click on **build**.

<figure><img src="../../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>
