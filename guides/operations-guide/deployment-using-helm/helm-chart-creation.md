# Helm chart creation

### What is Helm chart?

* &#x20;It is basically a set of templates and a file containing variables used to fill these templates based on the custom values and configurations.
* we can create helm charts on our own. For that we have to use the command `helm create <chart name>`. It will create a create a directory with files and some other directories. Those files are required to create helm chart.

### Creating helm chart:

* We already discussed about how what is repository. Now we are going to create helm chart in **DIGIT-DevOps** repository which is one of the repository in **eGovernments Foundation**.
* For that we need to clone that repository into local machine. Use the below commands to clone the repository in terminal or command prompt.

```
git clone https://github.com/egovernments/DIGIT-DevOps.git
```

* After cloning, go to helm directory and create helm chart there. **cd** command helps to change the directory

```
cd DIGIT-DevOps/tree/master/deploy-as-code/helm/charts/
```

```
helm create gowtham-helmchart
```

* Finally helm creates a directory with the following layout

<figure><img src="../../../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>

* **chart.yaml:** This is where you'll put the information related to your chart. That includes the chart version, name, and description so you can find it if you publish it on an open repository.&#x20;
* **values.yaml:** Like we saw before, this is the file that contains defaults for variables.
* **Templates(dir)**: This is the place where we are storing manifest files. Everything here will be passed on and created in kubernetes.
* &#x20;**charts**: If your chart depends on another chart you own, or if you don't want to rely on Helm's default library (the default registry where Helm pull charts from), you can bring this same structure inside this directory.
