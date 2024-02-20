---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Build & Deploy Flutter Web Application

## Overview

This page runs you through the steps to build the web application and deploy in respective environment.

## Steps

Follow the instructions [here](../../backend-developer-guide/section-7-build-and-deploy-instructions.md) to set up the job pipeline. Ignore the steps not applicable to the front end.

{% hint style="info" %}
Instructions here are provided assuming CD/CI has been set up using the DIGIT ci-as-code module.
{% endhint %}

Before setting up the job pipeline, make sure each project has a docker folder in the root folder of the project. The cirrusci flutter docker tag must be mentioned for building the application through Jenkins. Check the image below for reference.

![](<../../../../.gitbook/assets/image (1).png>)

The global assets inside the .env file should be loaded from the environment assets.&#x20;

{% hint style="info" %}
**Note:** The global assets file needs to be in JSON format for Flutter
{% endhint %}

Follow the sample config added in yaml files of the respective environment to load the global assets of works\_shg\_app.

dev yaml file : [works-dev.yaml](https://github.com/egovernments/DIGIT-DevOps/blob/digit-works/deploy-as-code/helm/environments/works-dev.yaml)

```
works-shg-app:
  custom-js-injection: |
    sub_filter.conf: "
      sub_filter  '<head>' '<head>
      <script src=https://works-dev.digit.org/works-dev-asset/worksGlobalConfig.json type=text/javascript></script>';"
```

Congrats!!! We are now ready to build and deploy the application on the web.

<details>

<summary>Build</summary>

Go to the Jenkins [build](https://builds.digit.org/job/builds/) page. Click on your project to build under the folder path mentioned below.&#x20;

For reference, if works\_shg\_app need to be build, Go to path\
[digit-works/job/frontend/job/works-shg-app/](https://builds.digit.org/job/builds/job/digit-works/job/frontend/job/works-shg-app/)

![](<../../../../.gitbook/assets/image (22).png>)

Click on `Build with parameter`. Select the feature branch name by searching for it in the search box on the right side of the screen. Click on Build.

![](<../../../../.gitbook/assets/image (2).png>)

Once the build is successful, open the console output and find the docker image that has been built. Copy the docker image ID.

![](<../../../../.gitbook/assets/image (14).png>)



</details>

<details>

<summary>Deploy</summary>

Go to the Jenkins [deployments](https://builds.digit.org/job/deployments/) page. Click on the desired environment you want to deploy the build

For reference, Let's deploy the works-shg-app build that was created to works-dev env.

Path ref: [https://builds.digit.org/job/deployments/job/deploy-to-works-dev/](https://builds.digit.org/job/deployments/job/deploy-to-works-dev/)

![](<../../../../.gitbook/assets/image (10).png>)

Copy the docker image IDs from the previous step and paste in the above box. Click on "Build". Once the image is deployed, you will see a message as shown below:

![](<../../../../.gitbook/assets/image (16).png>)



</details>

