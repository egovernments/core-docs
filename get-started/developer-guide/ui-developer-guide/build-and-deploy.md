---
description: Building and deploying the digit-ui module
---

# Build & Deploy

Follow the instructions [here](../backend-developer-guide/section-7-build-and-deploy-instructions.md) to set up the job pipeline. Ignore the steps not applicable to the frontend.

{% hint style="info" %}
Instructions here are provided assuming CD/CI has been set up using the DIGIT ci-as-code module.
{% endhint %}

<details>

<summary>Build </summary>

Method - 1 (Through Jenkins):\
Go to the Jenkins build page. Click on digit-ui under the folder path mentioned below. The entire UI module is built as a monolith. Since this module is also part of the same monolith, the entire UI module has to be built and redeployed.\
`frontend/micro-ui/digit-ui/`

<img src="../../../.gitbook/assets/image (205).png" alt="" data-size="original">

Click on `Build with parameter`. Select the feature branch name by searching for it in the search box on the right side of the screen. Click on Build.

<img src="../../../.gitbook/assets/image (182).png" alt="" data-size="original">

Once the build is successful, open the console output and find the Docker image that has been built. Copy the Docker image ID.

<img src="../../../.gitbook/assets/image (28) (1) (1).png" alt="" data-size="original">



**Method - 2(Recommended through Github actions) :**&#x20;

* Navigate to GitHub Actions\
  ![](<../../../.gitbook/assets/image (556).png>)
* Click on build pipeline\
  ![](<../../../.gitbook/assets/image (557).png>)
* Click on the Run workflow dropdown\
  ![](<../../../.gitbook/assets/image (558).png>)
* Select the branch name and module from the dropdown and hit the Run workflow button
* Once the build is successful, copy the build image name from the summary.

_Note: Make sure the "build.yaml" file is available under the .github/workflows folder._

</details>

<details>

<summary>Deploy</summary>

Link:- https://builds.companyname.org/job/deployments/job/deploy-to-dev/build?delay=0sec

<img src="../../../.gitbook/assets/image (96).png" alt="" data-size="original">

Copy the Docker image IDs from the previous step and paste them in the above box. Click on "Build". Once the image is deployed, you will see a message as shown below:

<img src="../../../.gitbook/assets/image (41) (1).png" alt="" data-size="original">

</details>
