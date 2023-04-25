# Development Environment Setup

Run the Kafka and PostgreSQL on the development machine and re-use other services from the DIGIT dev environment.&#x20;

The following tools are required for development:

i) **Install Git**&#x20;

[Git for windows](https://git-scm.com/download/win)

[Git for linux](https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-18-04-quickstart)

ii) **Install JDK8**

[JDK8 for windows](https://www.java.com/download/ie\_manual.jsp)

[JDK8 for linux](https://tecadmin.net/install-oracle-java-8-ubuntu-via-ppa/)

iii) **Install IDE** - For creating SpringBoot/Java applications we recommend using IntelliJ IDE. IntelliJ can be downloaded from the following links -

[IntelliJ for windows](https://www.jetbrains.com/idea/download/#section=windows)

[IntelliJ for linux](https://www.jetbrains.com/idea/download/#section=linux)

Install the Lombok plugins for IntelliJ as we use Lombok annotations in this module.

iv) **Install Kafka** (version 3.2.0 which is the latest version) - To install and run Kafka locally, follow the following links -

[Kafka for windows](https://dzone.com/articles/running-apache-kafka-on-windows-os)

[Kafka for linux](https://tecadmin.net/install-apache-kafka-ubuntu/)

v) **Install Postman** - To install postman, follow the following links -

[Postman for windows](https://www.postman.com/downloads/)

[Postman for linux](https://dl.pstmn.io/download/latest/linux64)

vi) **Install Kubectl** - Kubectl is the tool that we use to interact with services deployed on our sandbox environment.

[https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/)

[https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)

vii) **Install aws-iam-authenticator** - (if the DIGIT development environment is in AWS) - [https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html)

viii) **Install PostgreSQL v10 locally**

ix) **Add configuration** - Post installation of kubectl, you need to add the following configuration in the  Kubernetes config file to allow access to resources present in our sandbox environment.  Kubernetes config file is usually present in the user's home directory (which varies from OS to OS).&#x20;

For example, on a Mac, it is present at:

&#x20;`/Users/xyz/.kube/config`&#x20;

Once the config file is created, add the following content to it.

{% hint style="info" %}
Note that you will have to replace the placeholder keys and tokens in the below snippet with your AWS-specific keys. Please contact your system administrator for help with this.
{% endhint %}

```
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUN5RENDQWJDZ0F3SUJBZ0lCQURBTkJna3Foa2lHOXcwQkFRc0ZBREFWTVJNd0VRWURWUVFERXdwcmRXSmwKY201bGRHVnpNQjRYRFRJd01EVXhNekV6TlRReE5sb1hEVE13TURVeE1URXpOVFF4Tmxvd0ZURVRNQkVHQTFVRQpBeE1LYTNWaVpYSnVaWFJsY3pDQ0FTSXdEUVlKS29aSWh2Y05BUUVCQlFBRGdnRVBBRENDQVFvQ2dnRUJBTkJyClN6aHJjdDNORE1VZVF5TENTYWhwbEgyajJ1bkdYSWk1QThJZjF6OTgwNEZpSjZ6OS9qUHVpY3FjaTB1VURJQnUKS3hjdVFJRkozMG1MRWg3RGNiQlh2dDRnUlppZWtlZzVZNGxDT2NlTWZFZkFHY01KdDE1RVVCUFVzdlYyclRMcQp6a0ovRzVRUUFXMmhwREJLaFBoblZJTktYN1YzOU9tMUtuTklTbllPWERsZ1g3dW9Wa3I1OFhzREFHWEVsdC9uClpyc3laM2pkMWplWS8rMXlQQzlxbkorT0QwZlRQVGdCV1hMQlFwMHZKdHVzNE1JV2JLdkhlcUZ5eWtGd2V5MmoKSzk5eU1Yb0oraUpCaFJvWGllU3ZrNnFYdG44S2l4bVJtOXZPQk1hcWpuNkwwTjc3UWNCNjVRaHNKb0tWKzBiMQp5VVpJTHVTWWVTY0Yra3h6TzFVQ0F3RUFBYU1qTUNFd0RnWURWUjBQQVFIL0JBUURBZ0trTUE4R0ExVWRFd0VCCi93UUZNQU1CQWY4d0RRWUpLb1pJaHZjTkFRRUxCUUFEZ2dFQkFNdnF3THl6d2RUL05OWlkvanNzb0lmQmIyNDgKZ3oxSHRuSXJ4UGhaY3RrYjBSMExxeTYzRFZBMFNSN0MrWk90aTNNd3BHMkFSVHVzdG1vYm9HV3poUXlXRk16awpVMVNIZSt6S3poeGcweUpjUjliZnlxM1ZtQVVCZlQyTVV5cVl2OVg0aWxpbmV0SURQaFBuWnlPMERQTHJITGoyCkcxZy8vWmZYbmFCT2k3dlZLSXFXUUR6RlltWGkwME9vOEVoalVyMU5sQ3FISnF1dUo3TlRWQWk1cXA0Qm1xWU8KUTBrbTVxTVVHbG9ZdkNmN1lHQWREWTVnWGg4dzFVMVdaNWNub0Q4WWc3aEtlSjRMRzRram1adlNucGZrS3VxNApiVDdUSjEwUEZlWFJkek8xa2FkQ3VMQSttUlg3OEd5WEw0UTZnOFdPUlhOVDYzdXN3MnlpMXVVN1lMTT0KLS0tLS1FTkQgQ0VSVElGSUNBVEUtLS0tLQo=
    server: https://3201E325058272AA0990C04346DA6E82.yl4.ap-south-1.eks.amazonaws.com
  name: eks_egov-dev
contexts:
- context:
    cluster: eks_egov-dev
    namespace: egov
    user: eks_egov-dev
  name: dev
current-context: dev
kind: Config
preferences: {}
users:
- name: eks_egov-dev
  user:
    exec:
      apiVersion: client.authentication.k8s.io/v1alpha1
      args:
      - token
      - -i
      - egov-dev
      command: aws-iam-authenticator
      env:
      - name: AWS_ACCESS_KEY
        value: {AWS_ACCESS_KEY_PLACEHOLDER}
      - name: AWS_SECRET_ACCESS_KEY
        value: {AWS_SECRET_ACCESS_KEY_PLACEHOLDER}
      - name: AWS_REGION
        value: {AWS_REGION_PLACEHOLDER}
```

Once the config file is created, access the pods running in the environment by typing:

`kubectl get pods`

This will list all the pods in the dev environment.&#x20;

{% hint style="info" %}
**In case you run into an error stating “Error: You must be logged in to the server (Unauthorized)”, add sudo before the command. For example, “sudo kubectl get pods”. That should resolve the error.**
{% endhint %}

