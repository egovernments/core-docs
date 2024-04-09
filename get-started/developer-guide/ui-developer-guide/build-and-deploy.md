---
description: Building and deploying the digit-ui module
---

# Build & Deploy

Follow the instructions [here](../backend-developer-guide/section-7-build-and-deploy-instructions.md) to set up the job pipeline. Ignore the steps not applicable to the frontend.

{% hint style="info" %}
Instructions here are provided assuming CD/CI has been set up using the DIGIT ci-as-code module.&#x20;
{% endhint %}

<details>

<summary>Build</summary>

Go to the Jenkins build page. Click on digit-ui under the folder path mentioned below. The entire UI module is built as a monolith. Since this module is also part of the same monolith, the entire UI module has to be built and redeployed.\
`frontend/micro-ui/digit-ui/`

![](<../../../.gitbook/assets/image (205).png>)

Click on `Build with parameter`. Select the feature branch name by searching for it in the search box on the right side of the screen. Click on Build.

![](<../../../.gitbook/assets/image (182).png>)

Once the build is successful, open the console output and find the docker image that has been built. Copy the docker image ID.

![](<../../../.gitbook/assets/image (28).png>)



</details>

<details>

<summary>Deploy</summary>

Link:- https://builds.companyname.org/job/deployments/job/deploy-to-dev/build?delay=0sec

![](<../../../.gitbook/assets/image (96).png>)

Copy the docker image IDs from the previous step and paste in the above box. Click on "Build". Once the image is deployed, you will see a message as shown below:

![](<../../../.gitbook/assets/image (41).png>)



</details>





&#x20;

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this website by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
