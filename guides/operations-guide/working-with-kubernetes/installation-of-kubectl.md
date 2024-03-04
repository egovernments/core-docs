---
description: >-
  Kubectl is a command line tool that you use to communicate with the Kubernetes
  API server.
---

# Installation of Kubectl



* **Kubernetes** also known as K8s, is an open-source system for automating deployment, scaling, and management of containerized applications.**kubectl**, allows you to run commands against Kubernetes clusters.
* If you want to study about kubernetes in detail, open [Kubernetes](https://kubernetes.io/docs/concepts/overview/)

### Why kubectl is using in DIGIT?

There are some other tools like kubelet along with kubectl. kubectl is the command-line interface (CLI) tool for working with a Kubernetes cluster. Kubelet is the technology that applies, creates, updates, and destroys containers on a Kubernetes node.But the only difference is, using kubectl the developer can interacts with kubernetes cluster. So we are using kubectl in DIGIT.

{% hint style="info" %}
Note: If you are using AWS as service to create cluster, You must use a `kubectl` version that is within one minor version difference of your Amazon EKS cluster control plane. For example, a `1.23` `kubectl` client works with Kubernetes `1.22`, `1.23`, and `1.24` clusters
{% endhint %}

### To know kubernetes is installed:

```
kubectl version
```

### To install or update kubectl:

#### In Windows:

* Download the kubectl [latest release v1.25.0](https://dl.k8s.io/release/v1.25.0/bin/windows/amd64/kubectl.exe).\
  or if you have **curl** installed use this command:

```
curl.exe -LO "https://dl.k8s.io/release/v1.25.0/bin/windows/amd64/kubectl.exe"
```

{% hint style="info" %}
If you want to download kubectl desired version just replace the version in above command with your version name
{% endhint %}

* To download **curl** follow the page and proceed the download with curl [https://www.wikihow.com/Install-Curl-on-Windows](https://www.wikihow.com/Install-Curl-on-Windows)
* Append or prepend the `kubectl` binary folder to your `PATH` environment variable. To perform this, complete the following steps:&#x20;

<!---->

* [ ] 1.Open the **kubectl.exe** folder in files and copy that folder.

<figure><img src="../../../.gitbook/assets/Screenshot from 2022-12-06 09-14-29.png" alt=""><figcaption></figcaption></figure>

* [ ] 2.Create a new folder in **Local Disk(C:)** with name **Kube.**

<figure><img src="../../../.gitbook/assets/Screenshot from 2022-12-06 10-09-26.png" alt=""><figcaption></figcaption></figure>

* [ ] 3\. Paste the **kubectl.exe** folder there.
* [ ] 4\. Open **windows** option Search for **Advanced system settings**&#x20;

<figure><img src="../../../.gitbook/assets/Screenshot from 2022-12-06 10-18-49.png" alt=""><figcaption></figcaption></figure>

* [ ] 5\. Click on **Environmental variables** and then **System variables>Path>add** and add your path name i.e `c:\kube`
* [ ] 6\. Save it.

<figure><img src="../../../.gitbook/assets/Screenshot from 2022-12-06 10-19-05.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/Screenshot from 2022-12-06 12-47-16.png" alt=""><figcaption></figcaption></figure>

* Once you install `kubectl`, you can verify its version with the following command:

```
kubectl version --short --client
```

### To install kubectl in linux:

* Open the below link to install kubectl in linux:\
  [https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)

### To install kubectl in MacOs:

* Open the below link to install kubectl in macos:\
  [https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/](https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/)
