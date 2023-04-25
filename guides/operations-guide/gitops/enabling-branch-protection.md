---
description: >-
  You can create branch protection rule, such as requiring an approving review
  or passing status checks for all pull requests merged into the protected
  branch.
---

# Enabling Branch protection:

### Creating a branch inside repository:

* Go to the repository and click on **new branch.**

<figure><img src="../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

* Here I have created a branch named **DIGIT**
* After, go to that branch in the same repository.

<figure><img src="../../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

### Creating branch protection rule:

* Branch protection rule states that, how to manage the branch restrictions/permissions in GitHub.

NOTE : You must have admin access orelse you have to be a codeowner to make these changes for branch restrictions/permissions.

* Open https://github.com and choose any repository.Go to the main page. Click on **settings.**

<figure><img src="../../../.gitbook/assets/image (188).png" alt=""><figcaption></figcaption></figure>

* Click on **branches**

<figure><img src="../../../.gitbook/assets/image (122).png" alt=""><figcaption></figcaption></figure>

* If you click on the **Edit** rules you can able to see the rules which are applied for that branch.you should follow the rules when ever you are going to made any changes to that branch and pushing it.
* If you want to create new branch protection rule click on **Add Rule.**

<figure><img src="../../../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>



The common restrictions we are following to merge branches are :

1.Requires pull request

2.Requires approvals from CODE OWNERS

* Only the **CODE OWNERS** can have access to merge and makes changes to these rules.
